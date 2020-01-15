---
layout: default
title: Annoucing a challenge in breaking the ECDH PSI
parent: Blogs
nav_order: 989
---

# Annoucing a challenge in breaking the ECDH PSI


## Introduction of PSI (private set intersection)

Alice has a set $A={A_1, A_2, .... A_m}$, Bob has a set $B={B_1, B_2, .... B_n}$. 
They want to figure out the intersect set $A \bigcap B$ without leaking the other elements which are not in the intersection. 
This is well know as the Private Set Intersection problem.

## Introduction of ECDH PSI

The ECDH PSI algorithm is possibly the simplest among all the PSI algorithms. It works like this:

1. Alice and Bob agree on an EC curve, and each choose a secret key s_a and s_b.
2. Alice  and Bob hash the elements in $A,B$ to the EC curve. Let the new set be $PA,PB$.
3. Alice mask $PA$ with her secret key: $ Mask(PA_i) = PA_i*s_a $, and send ${PA_i*s_a}_{i=1,..m}$ to Bob.
4. Bob mask $PB$ with his secret key: $ Mask(PB_i) = PB_i*s_b $, and send ${PB_i*s_b}_{i=1,..n}$ to Alice.
5. Alice mask ${PB_i*s_b}_{i=1,..n}$ with her secret key, obtaining ${PB_i*s_b*s_a}_{i=1,..n}$, and send them back to Bob.
6. Bob mask ${PA_i*s_a}_{i=1,..m}$ with his secret key, obtaining ${PA_i*s_a*s_b}_{i=1,..m}$, and send them back to Alice.
7. Alice locally compare ${PA_i*s_a*s_b}_{i=1,..m}$ with ${PB_i*s_b*s_a}_{i=1,..n}$. For example if $A_2 = B_3$, she will find
$PA_2*s_a*s_b = PB_3*s_b*s_a $ as well.



Due to some subtle cryptographic issues, this algorithm is semi-honest, but not maliciously secure. 

The most interesting thing arises here: Does there really exist a solid malicious attack against this protocol which is only semi-honest?



## Task

Design a solid attack which allows Bob to succesfully recover at least one element from 
Alice's list which is not in the intersection.

Click contact for a $2000 reward if you find one !
