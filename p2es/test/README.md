# Overview

This image is based on the [pierky/pmacct](https://hub.docker.com/r/pierky/pmacct/) Docker image that, in turn, is based on the master branch of [pmacct](https://github.com/pmacct/pmacct). It is used to have a quick-and-dirt brand new setup of [pmacct-to-elasticsearch](https://github.com/pierky/pmacct-to-elasticsearch).

A fake ElasticSearch server is simulated using the Python built-in SimpleHTTPServer, some traffic is generated using a ping to 8.8.8.8 and finally the pmacctd daemon is executed. It is configured to run a plugin that sends its output to pmacct-to-elasticsearch.

# Disclaimer

This image has been created with the only purpose of being used in a "playground", for labs and interoperability tests. It does not implement any security best practice. Use it at your own risk.

# How to use this image

```
cd p2es/test/
docker build -t pierky/p2es-test -f Dockerfile .
docker run -it --rm pierky/p2es-test
```

Expected result:

```
PING 8.8.8.8 (8.8.8.8): 56 data bytes
INFO ( default/core ): Promiscuous Mode Accounting Daemon, pmacctd 1.7.0-git (20170705-00)
...
64 bytes from 8.8.8.8: icmp_seq=0 ttl=58 time=10.305 ms
INFO ( plugin1/print ): JSON: setting object handlers.
Serving HTTP on 0.0.0.0 port 9200 ...
INFO ( default/core ): link type is: 113
64 bytes from 8.8.8.8: icmp_seq=1 ttl=58 time=9.781 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=58 time=9.649 ms
...
INFO ( plugin1/print ): *** Purging cache - START (PID: 12) ***
INFO ( plugin1/print ): *** Purging cache - END (PID: 12, QN: 2/2, ET: 0) ***
127.0.0.1 - - [05/Jul/2017 16:26:26] code 404, message File not found
127.0.0.1 - - [05/Jul/2017 16:26:26] "HEAD /example-2017-07-05 HTTP/1.1" 404 -
127.0.0.1 - - [05/Jul/2017 16:26:26] code 501, message Unsupported method ('PUT')
127.0.0.1 - - [05/Jul/2017 16:26:26] "PUT /example-2017-07-05 HTTP/1.1" 501 -
127.0.0.1 - - [05/Jul/2017 16:26:26] code 404, message File not found
127.0.0.1 - - [05/Jul/2017 16:26:26] "HEAD /example-2017-07-05 HTTP/1.1" 404 -
2017-07-05 16:26:26,456 ERROR Error while creating index example-2017-07-05: An error
occurred while creating index example-2017-07-05 from template
/etc/p2es/new-index-template.json: error unknown
```

# Author

Pier Carlo Chiodi - https://pierky.com

Blog: https://blog.pierky.com Twitter: [@pierky](https://twitter.com/pierky)

