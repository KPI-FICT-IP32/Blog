---
layout: post
title:  "Lecture 8. Subnets. Test preparations."
date:   2016-04-14 08:30:00 +0200
categories: kpi_s06_networks
---
# Subnets
IANA organization is responsible for distributing IPv4 addresses. It used to be a single organization, but nowadays it has transformed into group of organizations:

- ARIN (North America)
- APNIC (Asia)
- AFRINIC (Africa)
- RIPENCC (Europe)
- ACNIC (Australia))

## Splitting network into subnets:

Given: `193.175.16.0 / 24`

In binary format: `11000001.10101111.000100000.00000000 / 24`

Assume, we want to make `n=2` subnets:

Increase network part by _]log<sub>2</sub>n[ = 1_ : `11000001.10101111.000100000.0 | 0000000 / 25`

Now we can have 2 subnets. Here they are:

- `11000001.10101111.000100000.0 | 0000000 / 25`
- `11000001.10101111.000100000.1 | 0000000 / 25`

Rewrite addresses in decimal:

- `193.175.16.0 / 25`
- `193.175.16.128 / 25`

Assume, we want to split `193.175.16.128 / 25` into `n = 4` subnets:

Increase network part by _]log<sub>2</sub>n[ = 2_ : `11000001.10101111.000100000.100|00000 / 27`

Now we can have 4 subnets. Here they are:

- `11000001.10101111.000100000.100 | 00000 / 27`
- `11000001.10101111.000100000.101 | 00000 / 27`
- `11000001.10101111.000100000.110 | 00000 / 27`
- `11000001.10101111.000100000.111 | 00000 / 27`

Rewrite addresses in decimal:

- `193.175.16.128 / 27`
- `193.175.16.160 / 27`
- `193.175.16.192 / 27`
- `193.175.16.224 / 27`

## Planning network
Given: 

- 193.175.16.0 / 24
- Five departments:

    |DPT|PCS| prefix | network |
    |---|---|--------|---------|
    |A  |27 |        |         |
    |B  |100|        |         |
    |C  |15 |        |         |
    |D  |4  |        |         |
    |E  |30 |        |         |


1. Determine subnet prefixes according to number of PCs:

    |DPT|PCS| prefix | network |
    |---|---|--------|---------|
    |A  |27 | /27    |         |
    |B  |100| /25    |         |
    |C  |15 | /27    |         |
    |D  |4  | /29    |         |
    |E  |30 | /29    |         |

    > **TODO:** _Describe this process_

2. Split network into subnets:

    > **TODO:** _Describe this process_

3. Assign subnets to department

    > **TODO:** _Describe this process_


# Test preparations

## Task 1

### Task Description

**Given:** `177.250.13.246 / 28`

**Find:** Network, Netmask, Broadcast address, 1st and last host IP in network:

### Solution

1. Write down IP in binary form: `101110001.11111010.00001011.11110110`
2. Determine host and network parts: `101110001.11111010.00001011.1111 | 0110`
3. Net: fill host part with zeros: `101110001.11111010.00001011.1111 | 0000`
4. Netmask: fill network part with ones and host part with zeros: `111111111.11111111.11111111.1111 | 0110`
5. Broadcast: fill host part with ones: `101110001.11111010.00001011.1111 | 1111`
6. First available IP: `101110001.11111010.00001011.1111 | 0001`
7. Last available IP: `101110001.11111010.00001011.1111 | 1110`

Finally transform binary results to decimal:

1. Net: `177.250.13.240`
2. Netmask: `255.255.255.240`
3. Broadcast: `177.250.13.255`
4. First available IP: `177.250.13.241`
5. Last available IP: `177.250.13.254`
6. Total IP addresses available: 2 <sup>(32 - 28)</sup> - 2 = 14

## Task 2. Split network into subnets.

> **NOTE:** I'm not sure, I got it right. Please correct me if I made a mistake, otherwise remove this note if you can.

### Task Description

**Given:** 
- `10.1.14.0 / 24`
- departments:

    |dpt| PCs | prefix | subnet |
    |---|-----|--------|--------|
    | 1 | 13  |        |        |
    | 2 | 120 |        |        |
    | 3 | 15  |        |        |
    | 4 | 61  |        |        |
    | 5 | 2   |        |        |

**To do:** Divide to subnets and assign subnets.


### Solution

1. Determine prefixes. I.E. For 120:
    - Keep in mind that you have to add 2 to number of PCs, as one address will be used as network address and other one will be used for broadcast.
    - Nearest bigger power of two is 128.
    - _log<sub>2</sub>128 = 7_
    - prefix = 32 - 7 = 25

    |dpt| PCs | prefix | subnet |
    |---|-----|--------|--------|
    | 1 | 13  | /28    |        |
    | 2 | 120 | /25    |        |
    | 3 | 15  | /28    |        |
    | 4 | 61  | /26    |        |
    | 5 | 2   | /30    |        |

2. Divide net into subnets:
    - 10.1.14.0 / 25
    - 10.1.14.128 / 25
        - 10.1.14.128 / 26
        - 10.1.14.192 / 26
            - 10.1.14.192 / 28
            - 10.1.14.208 / 28
            - 10.1.14.224 / 28
            - 10.1.14.240 / 28
                - 10.1.14.240 / 30
                - 10.1.14.244 / 30
                - 10.1.14.248 / 30
                - 10.1.14.252 / 30

3. Assign subnets:

    |dpt| PCs | prefix | subnet           |
    |---|-----|--------|------------------|
    | 1 | 13  | /28    | 10.1.14.192 / 28 |
    | 2 | 120 | /25    | 10.1.14.0 / 25   |
    | 3 | 15  | /28    | 10.1.14.208 / 28 |
    | 4 | 61  | /26    | 10.1.14.128 / 26 |
    | 5 | 2   | /31    | 10.1.14.240 / 30 |

