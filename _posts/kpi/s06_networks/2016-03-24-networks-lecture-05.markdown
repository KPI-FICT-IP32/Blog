---
layout: post
title:  "Lecture 5. Application level protocols. Telnet. SSH. HTTP. DNS"
date:   2016-03-24 08:30:00 +0200
categories: kpi_s06_networks
---

DHCP, FTP are text protocols

## Telnet
Was developed for remote access to other device's console.
Uses client-server architecture

All logins, passwords data are passed in unencrypted way.

## SSH
Secure SHell

Was developed for remote access to other device's console.
Uses client-server architecture

All logins, passwords data are passed encrypted.

## HTTP
HyperText Transfer Protocol

Client-server architecture

```
Client  Webserver
  [L]-------[S]
```

HTTP protocol up to version 1.1 (inclusive) is text protocol.
HTTP 2.0 is binary

HTTP request according to protocol consists of 3 parts

- Request string (mandatory)
    Request string consists of

    | Request type | Resource identifier| Protocol version |
    |--------------|--------------------|------------------|
    | GET/POST/PUT/PATCH/DELETE/...| in general it is URI | i.e HTTP/1.1|

    Example request string: `GET http://google.com.ua/ HTTP/1.1`
- Request headers (optional)
- message body (optional)

HTTP protocol is stateless. Hence workaround is required to store state. Such workaround is called `Cookies`.
Cookies are passed as request headers. Usually they are encoded in base64

## DNS
Domain Name Service

This protocol is used to resolve request url into actual IP address.

Domain name system is a distributed structure.
On the top of this structure root domain-name server is placed. This one knows how to resolve top level of domain name.
On the next level first-level domain servers are placed. They "know" where to find second-level domain servers and so on and so forth.

```
                   [root (.)]
          +------+----+---+------+-----+
        [com]   [ua]    [edu]  [org]  [io] ...
       +--+--+
       |     |
     [vk]   [github]...

```

Fully qualified domain name ends with dot: `fiot.kpi.ua.`

Domain name is resolved from end to beginning. DNS server delegates request to the corresponding lower-level DNS server.

If we want to open `mlp.wikia.com`:

1. DNS resolution request to DNS server to associate domain name with IP address.
    1.1 request [.] for `mlp.wikia.com`. response [com] DNS server
    1.2 request [com] for `mlp.wikia.com`. response [wikia.com] DNS server
    1.3 request [wikia.com] for `mlp.wikia.com`. response [mlp.wikia.com] IP address

### Types of DNS records:

- A. Domain name is associated with IP:
    ```foto IN A 77.77.77.77```
- PTR associates IP address with domain name. **in-addrarpa**.
    (77.47.128.130)

```
    in-addrarpa
     |  .... \ ...
    77
     |
    47
     |
    128
     |
    130
```

- TXT.
- SOA. (Self-off authority). Describes DNS server responsibilities (authority)
- NS. 
    ```kpi.ua IN NS ...```
- MX (Mail eXchange).

DNS lookup can be either interactive (DNS Server delegates to another DNS server) or recursive (Server recursively searches for response without delegating)

### NOTE
`nslookup` tool =)

## Mail Protocols:

```
      SMTP           IMAP/POP3
 [L]------------[S]-------------[PC]
 sender      mail server       receiver

```

### IMAP
This one is used to receive emails. This protocol is newer than POP3.

### POP3
This one is used to receive emails

### SMTP
This protocol is used to send email
