### ISC BIND9 Container (Stable: 9.11.1_xx) built on top of Alpine

This container is a super small (~5MB compressed pull, and only ~9MB
when extracted) FULL version of ISC BIND9.

It is ideal for a quick master, slave, recursive server/resolver, RPZ
"dns firewall", or just about any other purpose you can use bind for.

# Security - always on the latest stable release!
This container will _always_ be up to date on the latest
stable+patched version, usually within 24 hours of it being available
in Alpine.

# Required "DATA" directory - for named.conf and zone data:
This container assumes you have a "/DATA" folder with with your container specific data.
You can change that folder (and sub-folders) as needed, but make sure you update the "-v" mounts for the run.

Specifically, you need to have these directories/paths:
```
1.) [ *REQUIRED* ]
In your "/DATA/etc/bind" directory, a file "named.conf", which acts as an entry point to your configs

2.) [ *REQUIRED* ]
A "/DATA/var/cache/bind" directory for all of the master or slave zones. If it's for slave zones, it will populate automatically and you can leave it blank.
```


# How to run a BIND ("named") Docker Container?

```
docker run --name=dns-master01 \
-it -d \
--dns=8.8.8.8 --dns=8.8.4.4 \
-p 53:53/udp -p 53:53 \
-v /DATA/etc/bind:/etc/bind \
-v /DATA/var/cache/bind:/var/cache/bind \
tcely/bind:edge
```
