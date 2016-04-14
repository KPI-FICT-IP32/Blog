---
layout: post
title:  "Lecture 8. Subnets. Test preparations."
date:   2016-04-14 08:30:00 +0200
categories: kpi_s06_networks
---

IANA organization is responsible for distributing IPv4 addresses. It used to be a single organization, but nowadays it has transformed into group of organizations:

- ARIN (North America)
- APNIC (Asia)
- AFRINIC (Africa)
- RIPENCC (Europe)
- ACNIC (Australia))

# Splitting network into subnets:
Given: 193.175.16.0 / 24

In binary format:

- 11000001.10101111.000100000.00000000 / 24

Assume, we want to make `n=2` subnets:

Increase network part by one (`1 = log(base=2, arg=n) )

- 11000001.10101111.000100000.0|0000000 / 25

Now we can have 2 subnets. Here they are:

- 11000001.10101111.000100000.0|0000000 / 25
- 11000001.10101111.000100000.1|0000000 / 25

Rewrite addresses in decimal:

- 193.175.16.0 / 25
- 193.175.16.128 / 25

Assume, we want to split `193.175.16.128` / 25 into 4 subnets:

Increase network part by two (`2 = log(base=2, arg=n) )

- 11000001.10101111.000100000.100|00000 / 27

Now we can have 4 subnets. Here they are:

- 11000001.10101111.000100000.100|00000 / 27
- 11000001.10101111.000100000.101|00000 / 27
- 11000001.10101111.000100000.110|00000 / 27
- 11000001.10101111.000100000.111|00000 / 27

Rewrite addresses in decimal:

- 193.175.16.128 / 27
- 193.175.16.160 / 27
- 193.175.16.192 / 27
- 193.175.16.224 / 27

# Planning network
Given: 193.175.16.0 / 24

Five departments:

|DPT|PCS| prefix | network |
|---|---|--------|---------|
|A  |27 |        |         |
|B  |100|        |         |
|C  |15 |        |         |
|D  |4  |        |         |
|E  |30 |        |         |

## Step 1. Determine subnet prefixes according to number of PCs:

_TODO_: Describe this process

|DPT|PCS| prefix | network |
|---|---|--------|---------|
|A  |27 | /27    |         |
|B  |100| /25    |         |
|C  |15 | /27    |         |
|D  |4  | /29    |         |
|E  |30 | /29    |         |

## Step 2. Split network into subnets:

_TODO_: Describe this process


## Step 3. Assign subnets to department

_TODO_: Describe this process


# Test preparations

## Task 1
Given: `177.250.13.246 / 28

Find: Network, Netmask, Broadcast address, 1st and last host IP in network:

1. Write down IP in binary form: `101110001.11111010.00001011.11110110`
2. Determine host and network parts: `101110001.11111010.00001011.1111|0110`
3. Net: fill host part with zeros: `101110001.11111010.00001011.1111|0000`
4. Netmask: fill network part with ones: `111111111.11111111.11111111.1111|0110`
5. Broadcast: fill host part with ones: `101110001.11111010.00001011.1111|1111`
6. First available IP: `101110001.11111010.00001011.1111|0001`
7. Last available IP: `101110001.11111010.00001011.1111|1110`

Transform ino binary

## Task 2

Given: 10.1.14.0 / 24

| 1 | 13  |||
| 2 | 120 |||
| 3 | 15  |||
| 4 | 61  |||
| 5 | 2   |||

Divide to subnets and assign subnets.

1. Determine prefixes. For 120:
  - Nearest bigger power of two is 128.
  - log(2, 128) = 7
  - prefix = 32 - 7 = 25

| 1 | 13  | /28 ||
| 2 | 120 | /25 ||
| 3 | 15  | /28 ||
| 4 | 61  | /26 ||
| 5 | 2   | /30 ||

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

| 1 | 13  | /28 | 10.1.14.192 / 28 |
| 2 | 120 | /25 | 10.1.14.0 / 25   |
| 3 | 15  | /28 | 10.1.14.208 / 28 |
| 4 | 61  | /26 | 10.1.14.128 / 26 |
| 5 | 2   | /31 | 10.1.14.240 / 30 |

