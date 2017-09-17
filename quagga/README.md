# Tag `1.1.1`

This image is based on the 1.1.1 version of [Quagga](http://www.nongnu.org/quagga/). It `EXPOSE`s port 179 and mounts host's directory `./quagga` in the container's `/etc/quagga` directory; here the `quagga.conf` is used to give Quagga's `bgpd` the startup configuration and `log` is used by the daemon to write its log.

It has been created to run live tests for the ARouteServer project: https://github.com/pierky/arouteserver

# Tag `1.1.0-large-bgp-comm`

This image is based on the 1.1.0 version of [Quagga](http://www.nongnu.org/quagga/) and on the BGP Large Communities [patch](https://bugzilla.quagga.net/show_bug.cgi?id=875) by Keyur Patel and Job Snijders. It `EXPOSE`s port 179 and mounts host's directory `./quagga` in the container's `/etc/quagga` directory; here the `quagga.conf` is used to give Quagga's `bgpd` the startup configuration and `log` is used by the daemon to write its log. The `bgp.updates` and `bgp.routes` files are used by `bgpd` to write `dump bgp updates` and `dump bgp routes` commands output.

It has been created to run a playground to test BGP Large Communities: https://github.com/pierky/bgp-large-communities-playground

# Disclaimer

These images have been created with the only purpose of being used in a "playground", for labs and interoperability tests. They don't implement any security best practice. Use them at your own risk.

# How to use this image

Put the [Quagga startup config](http://www.nongnu.org/quagga/docs/docs-info.html#BGP) into `quagga/quagga.conf`...

```
# mkdir quagga
# vim quagga/quagga.conf
```

... then run the image in detached mode (`-d`) with the local `quagga` directory mounted in `/etc/quagga`:

```
# docker run -d -v `pwd`/quagga:/etc/quagga:rw pierky/quagga:1.1.1
```

You can verify that `log` gets populated: `cat quagga/log`.

Run `docker ps` to get the running container's ID (`80d9a33d7a01` in the example below), then use it to connect to the Quagga's terminal via telnet (port 2605, password `test`):

```
# docker exec -it 80d9a33d7a01 telnet 127.0.0.1 2605
Trying 127.0.0.1...
Connected to 127.0.0.1.
Escape character is '^]'.

Hello, this is Quagga (version 1.1.0).
Copyright 1996-2005 Kunihiro Ishiguro, et al.


User Access Verification

Password:
QuaggaBGPD> enable
QuaggaBGPD#
```

# Author

Pier Carlo Chiodi - https://pierky.com

Blog: https://blog.pierky.com Twitter: [@pierky](https://twitter.com/pierky)

