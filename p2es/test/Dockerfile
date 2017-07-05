FROM pierky/pmacct

MAINTAINER Pier Carlo Chiodi <pierky@pierky.com>

RUN apt-get install -y python-pip
RUN apt-get install -y git

RUN pip install pmacct-to-elasticsearch
RUN mkdir /etc/cron.d
RUN cd /usr/local/src/ && \
	git clone https://github.com/pierky/pmacct-to-elasticsearch.git && \
	cd pmacct-to-elasticsearch/ && \
	./install -F

# pmacctd.conf:
# - output: /var/lib/pmacct/plugin1.json
# - trigger: /etc/p2es/triggers/plugin1
# - interval: 5 seconds
ADD pmacctd.conf /etc/pmacct/pmacctd.conf

# plugin1.conf:
# - ElasticSearch (fake) URL: http://localhost:9200
# - input: /var/lib/pmacct/plugin1.json
ADD plugin1.conf /etc/p2es/plugin1.conf

RUN ln -s /etc/p2es/triggers/default_trigger /etc/p2es/triggers/plugin1

# 1. run a web server that simulates ElasticSearch (just to avoid
#    timeouts on the p2es side)
# 2. run a ping to do some traffic in order to have pmacctd to log something
# 3. run pmacctd in foreground to see what happens
# Expected result:
#   PING 8.8.8.8 (8.8.8.8): 56 data bytes
#   INFO ( default/core ): Promiscuous Mode Accounting Daemon, pmacctd 1.7.0-git (20170705-00)
#   ...
#   64 bytes from 8.8.8.8: icmp_seq=0 ttl=58 time=10.305 ms
#   INFO ( plugin1/print ): JSON: setting object handlers.
#   Serving HTTP on 0.0.0.0 port 9200 ...
#   INFO ( default/core ): link type is: 113
#   64 bytes from 8.8.8.8: icmp_seq=1 ttl=58 time=9.781 ms
#   64 bytes from 8.8.8.8: icmp_seq=2 ttl=58 time=9.649 ms
#   ...
#   INFO ( plugin1/print ): *** Purging cache - START (PID: 12) ***
#   INFO ( plugin1/print ): *** Purging cache - END (PID: 12, QN: 2/2, ET: 0) ***
#   127.0.0.1 - - [05/Jul/2017 16:23:26] code 404, message File not found
#   127.0.0.1 - - [05/Jul/2017 16:23:26] "HEAD /example-2017-07-05 HTTP/1.1" 404 -
#   127.0.0.1 - - [05/Jul/2017 16:23:26] code 501, message Unsupported method ('PUT')
#   127.0.0.1 - - [05/Jul/2017 16:23:26] "PUT /example-2017-07-05 HTTP/1.1" 501 -
#   127.0.0.1 - - [05/Jul/2017 16:23:26] code 404, message File not found
#   127.0.0.1 - - [05/Jul/2017 16:23:26] "HEAD /example-2017-07-05 HTTP/1.1" 404 -
#   2017-07-05 16:23:26,456 ERROR Error while creating index example-2017-07-05: An error
#   occurred while creating index example-2017-07-05 from template
#   /etc/p2es/new-index-template.json: error unknown

CMD python -m SimpleHTTPServer 9200 & ;; \
	ping 8.8.8.8 &>/dev/null & ;; \
	pmacctd -f /etc/pmacct/pmacctd.conf
