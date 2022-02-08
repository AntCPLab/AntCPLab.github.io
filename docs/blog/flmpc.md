---
layout: default
title: Federated Learning and Secure Multi-party Computation
parent: Blogs
nav_order: 990
---

# Federated Learning and Secure Multi-party Computation

Federated learning (FL) [orginally proposed by Google](https://arxiv.org/abs/1602.05629v1), is a machine learning technique that trains a model 
across multiple decentralized edge devices or servers holding local data samples. FL has a design of exchanging parameters instead of 
exchanging raw data, which provides users with a sense of security, and has made FL one of the most promising PPML techniques.

We introduced Secure Multiparty Computation (MPC) in [our previous blog](https://alibaba-gemini-lab.github.io/docs/blog/pvc/). Briefly speaking, 
MPC is a cryptographic protocol run by multiple participants. The protocol ensures that nothing else but the final computation result is revealed.

When the application scenario is machine learning training, FL and MPC looks similar: They all aim at training ML model among multiple data owners, without leaking the training data between each other. So what's the differences? This post will try to explain it. Could also visit [here](https://mp.weixin.qq.com/s/OmjQyQqd0YK8JT_QsNrplQ) for a full presentation in Chinese. 


# Main idea of FL

The main idea of FL comes from the design of parameter server which aims to solve the distributed training problem. The following figure
picked from [Li et.al.](https://arxiv.org/abs/1908.07873)
could roughly summarize the FL architecture:

![image](https://user-images.githubusercontent.com/35251608/152913569-932a0593-9e79-4dcc-b355-03bd5fba2cca.png)

1.	The coordinator sends the initial model $W$ to all the participants;
2.	The $i^{th}$ participant trains locally using $W$ and obtains an update $\Delta W_i$;
3.	All the participants send their updates to the coordinator;
4.	The coordinator aggregates the updates and use them to update $W$;
5.  Repeat the Step 1-4 loop until converge.

## Secure aggregation

At first glance, the security lies in whether the update $\Delta W_i$ leak information about the underlying data samples. Unfortunately 
a lot of research works have already made a conclusion that the answer is **YES**: 
[Exploiting unintended feature leakage in collaborative learning](https://arxiv.org/abs/1805.04049) (in SP2019),
[Deep leakage from gradients](https://arxiv.org/abs/1906.08935) (in NeurIPS2019),
[Beyond Inferring Class Representatives: User-Level Privacy Leakage From Federated Learning](https://arxiv.org/abs/1812.00535) (in INFOCOM2019).

How to reduce the leakage caused by the updates? The answer is using [secure aggregation](https://eprint.iacr.org/2017/281.pdf), which is a method
that secretly sums all the updates so that the coordinator only sees the aggregated result. Since the result comes from all
of the participants, the coordinator can hardly learn anything meaningful about a single participant.

## Limitation of secure aggregation

Note that secure aggregation is only effective if there's a big number of participants, such as the edge computing scenario,
where the participants are mobile devices.  [Google Gboard](https://www.youtube.com/watch?v=89BGjQYA0uE) is one of such use cases.
 
But if we use FL on a few number (e.g. two) of participants, it becomes problematic, even with secure aggregation. 
The reason is straightforward: Upon seeing the updated model in $i^{th}$ loop, one of the participant can simply remove its update in $i-1^{th}$ loop to 
figure out the other one's update. It's inevitable as long as a new model is released in clear each round. 

There also exists solutions which encrypt the updates with homomorphic encryption, but as long as the updates are decrypted at some intermediate step, the same problem exists.

We have a short paper [Quantification of the Leakage in Federated Learning](https://arxiv.org/abs/1910.05467) (in FL-NeurIPS2019) describing this.

# Comparing FL with Secure Multi-party Computation (MPC)

Like other cryptographic protocols, MPC has a strict definition of its security guarantee, which could be formalized by [Real-Ideal proofs](https://eprint.iacr.org/2016/046.pdf). The proof indicates that an attacker could not gain any extra advantage from the information he received in an MPC protocol. In contrast, FL is a machine learning definition that iteratively collects and updates the model, which could be revealed in each 
iteration. The security guarantee of FL is way harder to formalize. 

MPC enjoys a much higher security level, at the price of expensive cryptographic operations, which often results in higher computation 
and communication cost. FL loosen the security requirements, enabling more clear and efficient implementation. 

It's worth mentioning MPC is already very efficient for simple model and small participant numbers. E.g. The logistic regression example in [our another blog](https://alibaba-gemini-lab.github.io/docs/blog/tfe/) could be done in several seconds. However, in complex tasks such as training on millions of mobile phones, 
probably FL is the only realistic solution.

# Conclusion

As conclusion, we compare FL with MPC using the following figure, which only stands for the writer's personal view.

Methods | Security level | Efficiency | Suitable number of participants | Suitable model for ML training 
----                | ---           | ---           | ---            | 
Secure Multi-party Computation  | Provable secure<br>★★★★★ | Low  | Small (Cross-organization collaboration)  |  Simpler model 
 Federated Learning |  Leak intermediate information<br>★★★☆☆ | Medium | Big (Edge computing)  | All

