# Tag `latest`

This image is based on the master branch of [OpenBGPD Portable](https://github.com/openbgpd-portable/). It `EXPOSE`s port 179 and mounts host's directory `./bgpd` in the container's `/etc/bgpd` directory; here the `bgpd.conf` is used to give `bgpd` the startup configuration.

# Tag `7.3`

This image is based on the 7.3 version of [OpenBGPD Portable](https://github.com/openbgpd-portable/).

It has been created to run live tests for the ARouteServer project: https://github.com/pierky/arouteserver

# Tag `7.2`

This image is based on the 7.2 version of [OpenBGPD Portable](https://github.com/openbgpd-portable/).

It has been created to run live tests for the ARouteServer project: https://github.com/pierky/arouteserver

# Tag `7.1p0`

This image is based on the 7.1 version of [OpenBGPD Portable](https://github.com/openbgpd-portable/).

It has been created to run live tests for the ARouteServer project: https://github.com/pierky/arouteserver

# Tag `7.0p0`

This image is based on the 7.0 version of [OpenBGPD Portable](https://github.com/openbgpd-portable/).

It has been created to run live tests for the ARouteServer project: https://github.com/pierky/arouteserver

# Tag `6.9p0-patches`

This image is based on the 6.9p0 version of [OpenBGPD Portable](https://github.com/openbgpd-portable/) with some patches applied:

- *issue23-rtr.patch*: RTR protocol: Invalid argument and RTR session not coming up ([issue #23 on GitHub](https://github.com/openbgpd-portable/openbgpd-portable/issues/23) and ["bgpd, fix RTR connect"](https://marc.info/?l=openbsd-tech&m=162004696829635&w=2) post on openbsd-tech)

- *issue21-rde_evaluate_all_withdrawal.patch*: withdrawal of 2nd best route with `rde evaluate all` ([issue #21 on GitHub](https://github.com/openbgpd-portable/openbgpd-portable/issues/21) and ["bgpd fix for rde evaluate all"](https://marc.info/?l=openbsd-tech&m=162011500326166&w=2) post on openbsd-tech)

- *issue21-rde_evaluate_all_reload.patch*: advertisement of 2nd best routes on reload with `rde evaluate all` ([issue #21 on GitHub](https://github.com/openbgpd-portable/openbgpd-portable/issues/21) and ["bgpd better reload behaviour"](https://marc.info/?l=openbsd-tech&m=162021735205669&w=2) post on openbsd-tech)

- *issue21-rde_evaluate_all_withdrawal_post_reload.patch* withdrawal of 2nd best routes after a reload with `rde evaluate all` ([issue #21 on GitHub](https://github.com/openbgpd-portable/openbgpd-portable/issues/21) and ["bgpd fix for rde evaluate all"](https://marc.info/?l=openbsd-tech&m=162072314804091&w=2) post on openbsd-tech)

- *rtr-non-blocking-connect.patch* non blocking `connect()` call for RTR session establishment () (["bgpd behaviour when RTR endpoint is not available"](https://marc.info/?l=openbgpd-users&m=161997334304946&w=2) post on openbgpd-users and ["bgpd, non-blocking rtr connect"](https://marc.info/?l=openbsd-tech&m=162005636502085&w=2) post on openbsd-tech)

It has been created to run live tests for the ARouteServer project: https://github.com/pierky/arouteserver

# Tag `6.9p0`

This image is based on the 6.9p0 version of [OpenBGPD Portable](https://github.com/openbgpd-portable/).

It has been created to run live tests for the ARouteServer project: https://github.com/pierky/arouteserver

# Tag `6.8p1`

This image is based on the 6.8p1 version of [OpenBGPD Portable](https://github.com/openbgpd-portable/).

It has been created to run live tests for the ARouteServer project: https://github.com/pierky/arouteserver

# Tag `6.7p0`

This image is based on the 6.7p0 version of [OpenBGPD Portable](https://github.com/openbgpd-portable/).

It has been created to run live tests for the ARouteServer project: https://github.com/pierky/arouteserver

# Tag `6.6p0`

This image is based on the 6.6p0 version of [OpenBGPD Portable](https://github.com/openbgpd-portable/).

It has been created to run live tests for the ARouteServer project: https://github.com/pierky/arouteserver

# Tag `6.5p1`

This image is based on the 6.5p1 version of [OpenBGPD Portable](https://github.com/openbgpd-portable/).

It has been created to run live tests for the ARouteServer project: https://github.com/pierky/arouteserver

# Disclaimer

These images have been created with the only purpose of being used in a test environment, for labs and interoperability tests. They do not implement any security best practice. Use them at your own risk.

# How to use the `latest` image

Put the [OpenBGPD](https://man.openbsd.org/bgpd.conf.5) configuration into `bgpd/bgpd.conf`...

```
# mkdir bgpd
# vim bgpd/bgpd.conf
```

... then run the image in detached mode (`-d`) with the local `bgpd` directory mounted in `/etc/bgpd`:

```
# docker run -d -v `pwd`/bgpd:/etc/bgpd:rw pierky/openbgpd
```

# Author

Pier Carlo Chiodi - https://pierky.com

Blog: https://blog.pierky.com Twitter: [@pierky](https://twitter.com/pierky)

