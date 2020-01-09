---
layout: default
title: Federated Learning and Secure Multi-party Computation
parent: Blogs
nav_order: 990
---

# Different ways to achieve Privacy Preserving Machine Learning (PPML)

Although people talked about PPML everywhere, PPML is a term that is not well defined.  Generally it's safe to say that in PPML, people use 
technologies including  (but not limited to) differential privacy / homomorphic encryption / secure multi-party computation / trusted 
execution environment to protect the data during training or inference. 

Federated learning (FL) [orginally proposed by Google](https://arxiv.org/abs/1602.05629v1), is one of those PPML technologies. According to the 
definitions in [wikipedia](https://en.wikipedia.org/wiki/Federated_learning), FL is a machine learning technique that trains a model 
across multiple decentralized edge devices or servers holding local data samples. FL's design of exchanging parameters instead of 
exchanging raw data provide users with a sense of security, which has made FL one of the most promising PPML techniques.

# Main idea of FL

The main idea of FL comes from the design of parameter server which aims to solve the distributed training problem. The following figure
picked from [Li et.al.](https://www.groundai.com/project/federated-learning-challenges-methods-and-future-directions/1)
could roughly summarize the FL architecture:

![](https://storage.googleapis.com/groundai-web-prod/media/users/user_237920/project_386956/images/x10.png)

1.	The coordinator sends the initial model $W$ to all the participants;
2.	The $i^{th}$ participant trains locally using $W$ and obtain a update $\Delta W_i$;
3.	All the participants send their updates to the coordinator;
4.	The coordinator aggregates the updates and use them to update $W$;
5.  Repeat the Step 1-4 loop until converge.

## Secure aggregation

At first glance, the security lies in whether the update $\delta W_i$ leak information about the underlying data samples. Unfortunately 
a lot of research works have already made a conclusion that the answer is **YES**: 
[Exploiting unintended feature leakage in collaborative learning](https://arxiv.org/abs/1805.04049)(in SP2019),
[Deep leakage from gradients](https://arxiv.org/abs/1906.08935) (in NeurIPS2019),
[Beyond Inferring Class Representatives: User-Level Privacy Leakage From Federated Learning](https://arxiv.org/abs/1812.00535)(in INFOCOM2019).

How to reduce the leakage caused by the updates? The answer is using [secure aggregation](https://eprint.iacr.org/2017/281.pdf), which is a method
that secretly sums all the updates so that the coordinator only sees the aggregated result. Since the result comes from all
of the participants, the coordinator can hardly learn anything meaningful about a single participant.

## Limitation of secure aggregation

Note that secure aggregation is only effective if there's a big number of participants, such as the edge computing scenario,
where the participants are mobile devices.  [Google Gboard](https://www.youtube.com/watch?v=89BGjQYA0uE) is one of such use cases.
 
But if we use FL on a few number (e.g. two) of participants, it becomes problematic, even with secure aggregation. 
The reason is straightforward: Upon seeing the updated model in $i^{th}$ loop, one of the participant can simply remove its update in $i-1^{th}$ loop to 
figure out the other one's update. It's inevitable as long as a new model is released in clear each round. 

There also exists solutions which encrypt the updates with homomorphic encryption, but as long as it's only **partial** and not **fully** homomorphic,
the updates must be decrypted at some intermediate step, which triggers the same problem above.

We have a short paper [Quantification of the Leakage in Federated Learning](https://arxiv.org/abs/1910.05467)(in FL-NeurIPS2019) describing this.

# Compare FL with Secure Multi-party Computation (MPC)

We introduced MPC in our [previous blog](https://alibaba-gemini-lab.github.io/docs/blog/pvc/). Briefly speaking, 
MPC is a cryptographic definition which reveals no intermediate information during the whole computation, all it reveals is the final 
result. In contrast, FL is a machine learning definition that iteratively collects and updates the model, which is revealed in each 
iteration.

MPC enjoys a much higher security level, at the price of expensive cryptographic operations, which often results in highed computation 
and communication cost. FL loosen the security requirements, enabling more clear and efficient implementation. 

It's worth mentioning MPC ML is already very efficient for simple model and small participant numbers. E.g. The logistic regression example in [our previous blog]
(https://alibaba-gemini-lab.github.io/docs/blog/tfe/) could be done in several seconds. However, in complex tasks such as training on millions of mobile phones, 
probably FL is the only realistic solution.

# Conclusion

To compare FL and MPC as a conclusion, we draw the following figure, which only stands for the writer's personal view.

Methods | Security level | Efficiency | Suitable number of participants | Suitable ML model
----                | ---           | ---           | ---            | 
Secure Multi-party Computation  | High (Provable secure) | Low  | Small (Cross-organization collaboration)  |  Simple model (Logistic regression)
 Federated Learning |  Medium (Leak intermediate information) | Medium | Big (Edge computing)  | All

