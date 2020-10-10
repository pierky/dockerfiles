# ARouteServer docker image

A Docker image to easily start playing with ARouteServer. It's based on the latest release of Ubuntu, and offers a clean environment where users can start experimenting with the tool.

The only external dependency needed by ARouteServer is also installed: `bgpq3`.

To use it:

```
$ docker run -it --rm pierky/arouteserver
root@6a29b8be4376:/# arouteserver --help
root@6a29b8be4376:/# arouteserver setup
root@6a29b8be4376:/# arouteserver configure
root@6a29b8be4376:/# arouteserver bird --ip-ver 4 -o /root/bird4.conf
```

This will generate a BIRD IPv4 configuration file using the suggested configuration and some example clients.

## Tag `latest`

The image is built on top of the latest release of ARouteServer.

# Author

Pier Carlo Chiodi - https://pierky.com

Blog: https://blog.pierky.com Twitter: [@pierky](https://twitter.com/pierky)

