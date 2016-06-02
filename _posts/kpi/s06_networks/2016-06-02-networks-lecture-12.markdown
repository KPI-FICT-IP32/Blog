---
layout: post
title:  "Lecture 12. Cool stuff"
date:   2016-05-12 08:30:00 +0200
categories: kpi_s06_networks
---

# DHCP

```
        [ ] DHCP
         |
         |
       [===]----------(+)----{ INTERNET }
       / | \
      /  |  \
   [ ]  [ ]  [ ]
```

As we know, DHCP requests do not pass through third-layer devices.
But what if we have a topology like this? 

```
           DHCP  [ ]---[===]---[ ] WEB
                         / 
                        /
       [===]---------1(+)----{ INTERNET }
       / | \            2 
      /  |  \            \
   [ ]  [ ]  [ ]        [===]
                        / | \
                       /  |  \
                    [ ]  [ ]  [ ]
```

To handle this we could use own DHCP server for each subnetwork, which is extremely inconvenient and expensive (A lot of subnets == A lot of expensive server hardware). How can we handle this?

- Setup **DHCP Relay** on router ports 1 and 2!!!
- Setup default gateway for router

Now the router will repack BROADCAST DHCP requests into UNICAST requests and pass them to DHCP server.

- Setup IP pools for DHCP server:

```json
{ 
    "pool1": {
        "for network": "192.168.1.0/24",
        "def gateway": "192.168.1.254",
        ...
    },
    "pool2": {
        "for network": "192.168.2.0/24",
        "def gateway": "192.168.2.254",
        ...
    },
    ...
}
```

And voila! If you did everything correctly, your DHCP server will serve to several subnets as well as it does to one!

> If your DHCP server goes down, your whole network goes down. To handle this you may want to configure **DHCP Failover**


# NAT

IPv4 has too little IP addresses to assign to devices. There are even much less public addresses. However there are a lot of devices, which need to have an IP address. So how can we workaround this?

```
        [ ] DHCP
         |
         |              77.47.10.1
       [===]------.254(+)------------{ INTERNET }
       / | \                              |
     .1  .2 .3                          [   ] WEB
   [ ]  [ ]  [ ]                          vk.com (1.1.1.1)

   192.168.1.0/24
```

NAT stands for Network Address Translation. There are 3 Types of NAT:

- Static
- Dynamic
- Masquarade

## Static NAT

If router recieves request to Internet from 192.168.1.1 then it translates address to 77.47.11.1 We'll have the following header:

| Source     | Dest    | Data |
|------------|---------|------|
| 77.47.11.1 | 1.1.1.1 | Data |

When router recieves request from outer (like 1.1.1.1) to 77.47.11.1 it translates destination IP to corresponding Internal address (192.168.1.1)

All translations are saved in NAT table.

Static NAT is not really good, because it requires to have public address for each device.
## Dynamic NAT

Instead of setting correspondence between addresses it sets correspondence between pools of addresses and public address. If several requests from pool are received, they are translated in sequential order.

## Masquarade NAT (PAT)

**PAT** stands for Port Address Translation.

All requests from (i.e. .254) port of router are translated into one public IP address.
I.E. we are sending request from .1 PC:

|    |SRC        |DST    |
|IP  |192.168.1.1|1.1.1.1|
|Port|33101      |80     |

Then we'll have the following record in NAT table:

|Local IP   |Local Port|Global IP |Global Port| DST IP| DST Port|
|-----------|----------|----------|-----------|-------|---------|
|192.168.1.1|33101     |77.47.10.1|20001      |1.1.1.1|       80|

If router will recieve another request (even to the same resource) from 192.168.1.2 during request it'll add another record to NAT table and perform a corresponding substitute

|Local IP   |Local Port|Global IP |Global Port| DST IP| DST Port|
|-----------|----------|----------|-----------|-------|---------|
|192.168.1.1|33101     |77.47.10.1|20001      |1.1.1.1|       80|
|192.168.1.2|54104     |77.47.10.1|20002      |1.1.1.1|       80|

When response is recieved, corresponding record will be deleted from table.

> What happens inside NAT stays inside NAT. No internal activity is visible from outside.

But what if we **need** to access some internal resource from outside? **Port Forwarding** is used for that. You configure NAT so it translates all incoming requests to specific port (i.e. 8080) to specific device (i.e. 192.168.1.3)

# Firewall

Firewall is used to filter requests according to some rules. I.E. you may drop all requests to 8080 port both incoming and outcoming.

# Interestings

You can use [Wireshark][wireshark] to discover and explore your network traffic. This application allows you to analyse incoming and outcoming packages. Have fun =)

[wireshark]: https://www.wireshark.org/
