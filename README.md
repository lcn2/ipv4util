# ipv4util

* ipv4addr - extract IPv4 addresses from files

* ipv4print - print a range of IPv4 addresses

* ipv4range - convert a range of IPv4 addrs into a set of address CIDR blocks

* ipv4sort - extract IPv4 addresses from files in sorted order


# To install

```sh
sudo make install
```


# Examples


## ipv4addr - extract IPv4 addresses from files

Extract all IPv4 addresses from /etc/hosts

```sh
$ /usr/local/bin/ipv4addr /etc/hosts
127.0.0.1
255.255.255.255
10.50.25.1
10.50.25.7
192.168.2.1
192.168.2.13
...
```


## ipv4print - print a range of IPv4 addresses

Print IPv4 addresses between 192.168.1.252 and 192.168.2.8:

```sh
$ /usr/local/bin/ipv4print 192.168.1.252 192.168.2.8
192.168.1.252
192.168.1.253
192.168.1.254
192.168.1.255
192.168.2.0
192.168.2.1
192.168.2.2
192.168.2.3
192.168.2.4
192.168.2.5
192.168.2.6
192.168.2.7
192.168.2.8
```

Print IPv4 addresses in the 10.20.30.40/29 CIDR block:

```sh
$ /usr/local/bin/ipv4print 10.20.30.40/29
10.20.30.40
10.20.30.41
10.20.30.42
10.20.30.43
10.20.30.44
10.20.30.45
10.20.30.46
10.20.30.47
```


## ipv4range - convert a range of IPv4 addrs into a set of address CIDR blocks

Convert the IPv4 range 192.168.1.252 to 192.168.2.8 into CIDR blocks:

```sh
/usr/local/bin/ipv4range 192.168.1.252 192.168.2.8
192.168.1.252/30
192.168.2.0/29
192.168.2.8/32
```

Convert the IPv4 range 10.20.30.40 to 10.30.50.70 into CIDR blocks:

```sh
/usr/local/bin/ipv4range 10.20.30.40 - 10.30.50.70
10.20.30.40/29
10.20.30.48/28
10.20.30.64/26
10.20.30.128/25
10.20.31.0/24
10.20.32.0/19
10.20.64.0/18
10.20.128.0/17
10.21.0.0/16
10.22.0.0/15
10.24.0.0/14
10.28.0.0/15
10.30.0.0/19
10.30.32.0/20
10.30.48.0/23
10.30.50.0/26
10.30.50.64/30
10.30.50.68/31
10.30.50.70/32
```


## ipv4sort - extract IPv4 addresses from files in sorted order

Given this `/etc/hosts` file:

```
##
# Host Database
#
# localhost is used to configure the loopback interface
# when the system is booting.  Do not change this entry.
##
127.0.0.1	localhost localhost.localdomain localhost4 localhost4.localdomain4 kubernetes.docker.internal
255.255.255.255	broadcasthost

# important external addresses

10.50.25.1	gw.isp.example.net
10.50.25.7	dns.isp.example.net ntp.isp.example.net dns ntp

# local special hosts

192.168.2.1	host0.mydomain.example.com host0
192.168.2.13	host1.mydomain.example.com host1
```

Extract the IPv4 addresses from `/etc/hosts` in sorted order:

```sh
$ /usr/local/bin/ipv4sort -e /etc/hosts
10.50.25.1
10.50.25.7
127.0.0.1
192.168.2.1
192.168.2.13
255.255.255.255
```

Extract the IPv4 addresses from `/var/log/http/access.log`, printing only the unique IPv4 addresses in sorted order:

```sh
$ /usr/local/bin/ipv4sort -e /var/log/http/access.log
10.12.0.4
10.14.1.2
10.14.1.3
10.14.15.62
10.15.0.1
10.89.170.186
10.189.106.114
...
```


# To use


## ipv4addr - extract IPv4 addresses from files

```
/usr/local/bin/ipv4addr [-h] [-V] [file ...]

    -h              print help and exit
    -V              print version and exit

    [file ...]	    process data in file(s) (def: read stdin)

ipv4addr version: 1.6.1 2025-03-28
```


## ipv4print - print a range of IPv4 addresses

```
/usr/local/bin/ipv4print [-h] [-v lvl] [-V] [-o] dot.ed.ivp4.addr [ignored] dot.ed.ipv4.addr
/usr/local/bin/ipv4print [-h] [-v lvl] [-V] [-o] dot.ed.ivp4.addr/CIDR

    -h              print help and exit
    -v lvl          verbose / debug level
    -V              print version and exit

    -o              using open range, address range stops 1 short of high

    dot.ed.ivp4.addr    starting IPv4 address
    [ignored]           igonored optional arg
    dot.ed.ipv4.addr    ending IPv4 address

    NOTE: When given 3 args, the 2nd arg is ignored.

    dot.ed.ivp4.addr/CIDR   IPv4 address and CIDR block

ipv4print version: 1.6.1 2025-03-28
```


## ipv4range - convert a range of IPv4 addrs into a set of address CIDR blocks

```
/usr/local/bin/ipv4range [-h] [-v lvl] [-V] [-o] dot.ed.ivp4.addr [ignored] dot.ed.ipv4.addr

    -h              print help and exit
    -v lvl          verbose / debug level
    -V              print version and exit

    -o              using open range, address range stops 1 short of high

    dot.ed.ivp4.addr    starting IPv4 address
    [ignored]           igonored optional arg
    dot.ed.ipv4.addr    ending IPv4 address

    NOTE: When given 3 args, the 2nd arg is ignored.

ipv4range version: 1.6.1 2025-03-28
```


## ipv4sort - extract IPv4 addresses from files in sorted order

```
/usr/local/bin/ipv4sort [-h] [-V] [-d] [-e] [-w] [-u] [file ...]

    -h              print help and exit
    -V              print version and exit

    -d		    misc debugging
    -e		    just extract IP addresses and sort them (no -w)
    -w		    keep the whole line, sort on 1st IP address (default unless -e)
    -u		    keep only unique lines

    [file ...]	    process data in file(s) (def: read stdin)

ipv4sort version: 1.6.1 2025-03-28
```


# Reporting Security Issues

To report a security issue, please visit "[Reporting Security Issues](https://github.com/lcn2/ipv4util/security/policy)".
