---
layout: default
title: Pegasus explained 
parent: Blogs
nav_order: 988
---


# Pegasus: Bridging Polynomial and Non-polynomial evaluations in Homomorphic Encryption 

This blog is partly translated from this post: [推动全同态加密功能提速64倍，阿里安全双子座实验室这项技术被世界顶会收录！](https://zhuanlan.zhihu.com/p/340690021).

Recently, Alibaba has made an important step in extending fully homomorphic encryption (FHE) schemes. The work [Pegasus: Bridging Polynomial and Non-polynomial evaluations in Homomorphic Encryption](https://eprint.iacr.org/2020/1606) was accepted to IEEE Symposium on Security and Privacy (S&P). This is the first time that a Chinese company publish a first-author paper in the conference. This blog will try to describe the rough idea of Pegasus.

## Obstacles in deploying fully homomorphic encryption

Fully homomorphic encryption (FHE) can perform arbitrary calculations on ciphertexts without decryption, and has been viewed as the "Holy Grail" of cryptography. 

One of its potential use case is collaborative data analytics: Assume that data owner A needs to cooperate with data owner B, but considering data privacy issues, both A & B do not want to reveal their raw data to each other. FHE could be the solution: B can use FHE to encrypt his data and then send it to A, so that A can complete the calculations without touching the original data content of B. Finally, A gives the encrypted results to B, who decrypts and reveal the final result. In this way, we make the data "usable but not visible", and both parties' data privacy could be protected.

However, FHE still faces many obstacles in real applications. At present, FHE schemes could be divided into two subtypes: schemes such as CKKS/BGV/BFV (denoted as type A) only support polynomial calculations such as addition and multiplication, and it is difficult to effectively support non-polynomial calculations such as division and square-roots; other schemes such as TFHE/FHEW (denoted as type B) can support arbitrary calculations, but their performance is significantly weaker than type A.


Schemes | Computing polynomials | Computing non-polynomials |
----                | ---           | ---          
Type A  |  Efficient, SIMD support  | In-expressible, Approximated  
 Type B |  Not efficient, no SIMD support | Expressible 



## Having the best of both worlds


"In actual applications, both polynomial and non-polynomial operations are required. These problems are difficult to solve with a single FHE scheme." said Wen-jie, senior algorithm engineer at Alibaba Gemini Lab. Wen-jie's main research interest lies in FHE and other privacy-enhancing techniques. He graduated from University of Tsukuba with a PhD degree, and joined Gemini Lab in 2019. Wen-jie has contributed to many well-known open source FHE libraries including HElib and SEAL.

Wen-jie and his colleagues proposed "Pegasus", a new solution that can efficiently convert between Type A and Type B FHE schemes without decryption. Users can use Type A schemes (like the horse form) when polynomial calculations are needed, and switch to Type B schemes (like the flying form) when they need to do non-polynomial calculations.

![](https://raw.githubusercontent.com/Alibaba-Gemini-Lab/Alibaba-Gemini-Lab.github.io/master/docs/pr.png)

The "Pegasus" paper follows the blueprints of a previous paper "[Chimera](https://eprint.iacr.org/2018/758)", with the efficiency drastically improved. Taking the commonly used operation "Sigmoid" in machine learning as an example, Pegasus not only speeds up the evaluations by 64 times, but also reduces the volume of the conversion key by two orders of magnitudes (~100GB to ~1GB), which can significantly reduce the cost of key transmission and memory usage.

Cheng Hong, director of Cryptography and Privacy at Gemini Lab, explained the motivation for the birth of the "Pegasus": "In Alibaba's next-generation security architecture, we focus on building stable and reliable security technology with solid guarantees. Cryptography is one of such kind of techniques that has provable security based on mathematics".

## Broader impact

Privacy-enhancing computing has begun to gain recognition these days, and many related applications have been reported in the industry. However, due to the limited performance and functionalities of underlying cryptographic technologies, these applications are often concentrated in some simple scenarios, and it is difficult to expand them to larger and more complex business scopes.

Therefore, the breakthrough of Pegasus has taken a step forward in solving the problem of the limitations of FHE functionalities, broadening the potential application scenarios of various privacy-enhancing computing technologies.

