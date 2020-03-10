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
This is well known as the Private Set Intersection problem.

## Introduction of ECDH PSI

The ECDH PSI algorithm is possibly the simplest among all the PSI algorithms. It works like this:

1. Alice and Bob agree on an EC curve, and each choose a secret key $s_a$ and $s_b$. In this challenge let it be Curve25519, and $s_a$ and $s_b$ are chosen according to the secret key specification of Curve215519.
2. Alice  and Bob hash the elements in $A,B$ to the EC curve. Let the new set be $PA,PB$.
3. Alice masks $PA$ with her secret key: $ Mask(PA_i) = PA_i\cdot s_a $, and sends ${PA_i\cdot s_a} (i=1,...m)$ to Bob.
4. Bob masks $PB$ with his secret key: $ Mask(PB_i) = PB_i \cdot s_b $, and sends ${PB_i\cdot s_b} (i=1,...n)$ to Alice.
5. Alice masks $PB_i \cdot s_b (i=1,...n) $ with her secret key, obtaining $PB_i \cdot s_b \cdot s_a (i=1,...n)$, and sends them back to Bob.
6. Bob masks $PA_i \cdot s_a (i=1,...m)$ with his secret key, obtaining $PA_i \cdot s_a \cdot s_b (i=1,...m)$, and sends them back to Alice.
7. Alice locally compares ${PA_i \cdot s_a \cdot s_b} (i=1,...m)$ with ${PB_i \cdot s_b \cdot s_a} (i=1,...n)$, and finds out the intersection. For example if $A_2 = B_3$, she will find
$PA_2 \cdot s_a \cdot s_b = PB_3 \cdot s_b \cdot s_a $ as well.

We have deployed several successful commercial use cases on billions of data with our collaborators using the above algorithm (using Curve25519). But due to some subtle cryptographic issues, this algorithm is (arguably) semi-honest, but not maliciously secure.

The most interesting thing arises here: Does there really exist a solid malicious attack against this protocol which is only semi-honest?



## Task

Design a solid attack which allows Bob to succesfully recover at least one element from 
Alice's list which is not in the intersection. ~~Note that the target of this challenge is to find some vulnerablities which only exist in semi-honest protocols, so "attacks" such as "Can Bob add some elements to his list which he does not actually own" is not in this scope, because they also exist for malicious protocols.~~

### UPDATE

We received valuable suggestions for the above note: 
>The attack of "Bob add some elements to his list which he does not actually own" does not hold for maliciously-secure protocols, because Bob must commit to his input.

We admit that this is right. Theoretically, altering input **before the protocol begin** is not considered as a malicious behavior, while altering input **after the protocol begin** is indeed malicious. This is because in simulation proof, we use the "input" to build the "ideal world". So we change the restriction to a more well-defined one as follows:

Note that the target of this challenge is to find some vulnerabilities in data confidentiality rather than integrity or usability, so these kinds of attacks are not considered:
  1. "Attacks" that reach the same result by honestly using some other inputs. 
  >Example: Bob change his input to some other $B'$ **after the protocol begin**. This is a malicious behavior and Bob may recover elements of $B'$ from the victim. But Bob could reach the same result by setting his input to $B'$ **before the protocol begin** and act honestly. Thus this kind of attack is not what we need. 
  2. "Attacks" that lead to fairness problem. 
  >Example: Bob (partially) send some garbage in Step 6.   
  3. Combining 1 and 2.
  >Example: Bob change his input to some other $B'$ **after the protocol begin**, and send garbage in Step 6. Bob could reach the same result by setting his input to $B'$ **before the protocol begin** and send garbage.

Click Menu -> About us-> Contact for a $2000 reward if you find one !
