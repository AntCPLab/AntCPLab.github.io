---
layout: default
title: What's new
nav_order: 1
description: "Ant CP Lab"
permalink: /
---

<style>
.tab-container {
  margin-bottom: 2rem;
}

.tab-buttons {
  display: flex;
  gap: 1rem;
  margin-bottom: 1.5rem;
  border-bottom: 2px solid #e5e5e5;
}

.tab-btn {
  padding: 0.75rem 1.5rem;
  border: none;
  background: none;
  cursor: pointer;
  font-size: 1rem;
  font-weight: 600;
  color: #666;
  border-bottom: 3px solid transparent;
  transition: all 0.3s ease;
}

.tab-btn.active {
  color: #2c5aa0;
  border-bottom-color: #2c5aa0;
}

.tab-btn:hover {
  color: #2c5aa0;
}

.tab-content {
  display: none;
}

.tab-content.active {
  display: block;
  animation: fadeIn 0.3s ease;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}
</style>

<script>
function switchTab(tabName) {
  // 隐藏所有 tab 内容
  var contents = document.querySelectorAll('.tab-content');
  for (var i = 0; i < contents.length; i++) {
    contents[i].classList.remove('active');
  }
  
  // 取消所有按钮的 active 状态
  var buttons = document.querySelectorAll('.tab-btn');
  for (var i = 0; i < buttons.length; i++) {
    buttons[i].classList.remove('active');
  }
  
  // 显示当前 tab
  document.getElementById(tabName).classList.add('active');
  
  // 激活当前按钮
  var activeBtn = document.querySelector('.tab-btn[data-tab="' + tabName + '"]');
  if (activeBtn) {
    activeBtn.classList.add('active');
  }
}
</script>

<div class="tab-container">
  <div class="tab-buttons">
    <button class="tab-btn active" data-tab="crypto" onclick="switchTab('crypto')">🔐 Crypto</button>
    <button class="tab-btn" data-tab="ai" onclick="switchTab('ai')">🤖 AI</button>
  </div>

  <div id="crypto" class="tab-content active" markdown="1">

# Applied Crypto

### 2026.4
- Paper "[MOAI: Module-Optimizing Architecture for Non-Interactive Secure Transformer Inference](https://eprint.iacr.org/2025/991)" accepted by ICLR 2026.

### 2026.3
- Paper "Secure Lookup Tables: Faster, Leaner, and More General" accepted by SP 2026.
  
### 2026.2
- Paper "Soloist: Distributed SNARK for R1CS with Constant Proof Size" accepted by Eurocrypt 2026.
  
### 2026.1
- Paper "RBOOT: Accelerating Homomorphic Neural Network Inference by Fusing ReLU within Bootstrapping" accepted by USENIX Security 2026. 
  
### 2025.11
- The 'SM2MLKEM768' hybrid post-quantum key exchange, proposed by [Tongsuo](https://github.com/Tongsuo-Project), receives official [IANA TLS code 4590](https://www.iana.org/assignments/tls-parameters.xhtml#tls-parameters-8).

### 2025.10
- Cheng Hong  serves as a PC member of ACM CCS 2026.
- Cheng Hong  receives the [top reviewer award](https://raw.githubusercontent.com/AntCPLab/AntCPLab.github.io/refs/heads/master/assets/images/rccs25.jpg) of ACM CCS 2025.

### 2025.9
- Paper "Dory: Streaming PCG with Small Memory" accepted by SP 2026.
- Attended CHES 2025 in Kuala Lumpur: [pic](https://antcplab.github.io/assets/images/CHES2025.png).
  
### 2025.8
- Attended USENIX Security 2025 in Seattle. Pictures of our colleagues at the sponsor's desk: [pic](https://raw.githubusercontent.com/AntCPLab/AntCPLab.github.io/master/assets/images/sec25.JPG).
  
### 2025.7
- Paper "PANTHER: Private Approximate Nearest Neighbor Search in the Single Server Setting" [[paper]](https://eprint.iacr.org/2024/1774)  accepted by ACM CCS 2025.
- Cheng Hong serves as a PC member of USENIX Security 2026.
  
### 2025.6
- Cheng Hong is elected as the chair of [Tongsuo](https://github.com/Tongsuo-Project) project management commitee.
- Paper "XBOOT: Free-XOR Gates for CKKS with Applications to Transciphering" [[paper]](https://eprint.iacr.org/2025/074) [[code]](https://github.com/AntCPLab/xboot-ckks-transciphering) accepted by CHES 2025.

### 2025.5
- Cheng Hong  receives the [Distinguished Young Scientist Award](https://kw.beijing.gov.cn/ztzl/2024ndbjskxjsjl/2024jcqnzgcj/) from Beijing People's Goverment.
- Attended SP 2025 in San Francisco.  Pictures of our colleague presenting:  [pic1](https://raw.githubusercontent.com/AntCPLab/AntCPLab.github.io/master/assets/images/SP25-1.jpg) and [pic2](https://raw.githubusercontent.com/AntCPLab/AntCPLab.github.io/master/assets/images/SP25-2.jpg).
 
### 2025.4
- Zhicong Huang  serves as a PC member of ACM CCS 2025.
- Paper "SoK: FHE-Friendly Symmetric Ciphers and Transciphering" [[paper]](https://eprint.iacr.org/2025/669) [[code]](https://github.com/AntCPLab/awesome-transciphering)  accepted by CHES 2025.
  
### 2025.3
- Paper ["ZHE: Efficient Zero-Knowledge Proofs for HE Evaluations"](https://eprint.iacr.org/2025/770)  accepted by SP 2025. **Important update: A bug was found in Section 4, making ZHE's claimed 3-party computation insecure.**
- Paper "HyperPianist: Pianist with Linear-Time Prover and Logarithmic Communication Cost" [[paper]](https://eprint.iacr.org/2024/1273) [[code]](https://github.com/AntCPLab/HyperPianist) accepted by EUROCRYPT 2025.
  
### 2025.2
- Paper "GraphAce: Secure Two-Party Graph Analysis Achieving Communication Efficiency"  accepted by USENIX Security 2025.
- Attended NDSS 2025 in San Diego.

### 2025.1
- Cheng Hong  serves as a PC member of ACM CCS 2025.

### 2024.11
- Attended ChinaCrypt 2024 in Hangzhou.  Pictures of our colleagues presenting: [pic](https://raw.githubusercontent.com/AntCPLab/AntCPLab.github.io/master/assets/images/CHINACRYPT2024.jpg).
  
### 2024.10
- Attended [ACM CCS 2024](https://www.sigsac.org/ccs/CCS2024/) in Salt Lake City.  Pictures of our colleagues presenting: [pic](https://raw.githubusercontent.com/AntCPLab/AntCPLab.github.io/master/assets/images/CCS24.jpg).

### 2024.8
  
- Paper "Coral: Maliciously Secure Computation Framework for Packed and Mixed Circuits" [[paper]](https://eprint.iacr.org/2024/1372) [[code]](https://github.com/AntCPLab/OpenCoral) accepted by ACM CCS 2024.
- Paper "Sublinear Distributed Product Checks on Replicated Secret-Shared Data over Large Finite Fields without Ring Extensions" [[paper]](https://eprint.iacr.org/2024/700) [[code]](https://github.com/AntCPLab/malicious-dspc) accepted by ACM CCS 2024.
- Attended [USENIX Security 2024](https://www.usenix.org/conference/usenixsecurity24/) in Philadelphia as a silver sponsor.  Pictures of our colleagues at the sponsor's desk: [pic](https://raw.githubusercontent.com/AntCPLab/AntCPLab.github.io/master/assets/images/sec24.JPG).
  
### 2024.7

- Paper "BumbleBee: Secure Two-party Inference Framework for Large Transformers" [[paper]](https://eprint.iacr.org/2023/1678) [[code]](https://github.com/AntCPLab/OpenBumbleBee)  accepted by NDSS 2024.
  
### 2024.5

- Attended [SP 2024](https://sp2024.ieee-security.org/index.html) in San Francisco.  Pictures of our colleagues presenting: [pic](https://raw.githubusercontent.com/AntCPLab/AntCPLab.github.io/master/assets/images/SP24.jpg).

### 2024.1
- Cheng Hong  serves as a PC member of PKC 2024.

### 2023.12

- Attended [ACM CCS 2023](https://www.sigsac.org/ccs/CCS2023/index.html) in Copenhagen as a platinum sponsor. [Picture](https://raw.githubusercontent.com/AntCPLab/AntCPLab.github.io/master/assets/images/CCS23.jpg).

### 2023.8

- Attended [USENIX Security 2023](https://www.usenix.org/conference/usenixsecurity23/) in Anaheim. Pictures of our colleagues presenting: [pic1](https://raw.githubusercontent.com/AntCPLab/AntCPLab.github.io/master/assets/images/sec23-1.jpg) and [pic2](https://raw.githubusercontent.com/AntCPLab/AntCPLab.github.io/master/assets/images/sec23-2.jpg).

- Paper [Accelerating Secure Collaborative Machine Learning with Protocol-Aware RDMA](https://www.usenix.org/system/files/sec23winter-prepub-4-ren.pdf)   accepted by USENIX Security 2024.

### 2023.5

- Paper "Efficient 3PC for Binary Circuits with Application to Maliciously-Secure DNN Inference" [[paper]](https://eprint.iacr.org/2023/909) [[code]](https://github.com/AntCPLab/malicious_3pc_binary) accepted by EUROCRYPT 2023.
- Attended [SP 2023](https://sp2023.ieee-security.org/index.html) in San Francisco.

### 2023.4

- Paper "CHAM: A Customized Homomorphic Encryption Accelerator for Fast Matrix-Vector Product" [[paper]](https://github.com/alibaba-damo-academy/damo_ctl_cham/blob/main/DAC_2023_CHAM.pdf) [[code]](https://github.com/alibaba-damo-academy/damo_ctl_cham) accepted by ACM DAC 2023.

- [An Attack on RIAC Homomorphic Encryption Algorithm](http://www.jcr.cacrnet.org.cn/CN/10.13868/j.cnki.jcr.000604) was published in Journal of Cryptologic Research (in Chinese). It describes how to break the RIAC cipher.

### 2023.3

- Gave a talk at the [6th HomomorphicEncryption.org Standards Meeting](https://homomorphicencryption.org/6th-homomorphicencryption-org-standards-meeting/) in Seoul, South Korea.

### 2023.2

- Paper "Squirrel: A Scalable Secure Two-Party Computation Framework for Training Gradient Boosting Decision Tree" [[paper]](https://eprint.iacr.org/2023/527) [[code]](https://github.com/secretflow/secretflow) accepted by USENIX Security 2023.

### 2023.1

- **We have moved to** [**Ant Group**](https://www.antgroup.com/en)! 

### Prior works at Alibaba Gemini Lab

2022.8
> We just deliver a major update to [TF Encrypted](https://github.com/tf-encrypted/tf-encrypted), including benchmarks on several PPML operations such as NN training and inference. Please check the [changelog](https://github.com/tf-encrypted/tf-encrypted/releases/tag/v0.8.0).

2022.3
> The [Microsoft SEAL](https://github.com/microsoft/SEAL) homomorphic encryption library released version 4.0, including the [BGV implementation](https://github.com/microsoft/SEAL/pull/283) we contributed.

2022.2
> Paper [Cheetah: Lean and Fast Secure Two-Party Deep Neural Network Inference](https://eprint.iacr.org/2022/207) accepted by USENIX Security 2022.

2022.1
> We found that the [RIAC (Random iterative affine cipher)](https://fate.readthedocs.io/en/develop-1.5/_build_temp/python/federatedml/secureprotol/README.html#iterativeaffine-homomorphic-encryption) is insecure. Check out our [technical report](https://arxiv.org/abs/2203.05205).

2021.12
> Paper [More Efficient Secure Matrix Multiplication for Unbalanced Recommender Systems](https://www.computer.org/csdl/journal/tq/5555/01/09665288/1zJiScWQJ1e) accepted by IEEE TDSC.

2021.11
> Standard [IEEE Recommended Practice for Secure Multi-Party Computation](https://standards.ieee.org/standard/2842-2021.html) is published! Thanks for everyone contributed in the project.

2021.5
> Paper [When Homomorphic Encryption Marries Secret Sharing](https://arxiv.org/abs/2008.08753) accepted by SIGKDD2021.

2020.12
> Paper [Pegasus: bridging polynomial and Non-polynomial evaluations in Homomorphic Encryption](https://eprint.iacr.org/2020/1606) accepted by S&P 2021.

> We got the second place in Track I of [iDASH2020 secure genome analysis competition](http://www.humangenomeprivacy.org/2020/). 

2020.9
> Paper  [Improving Utility and Security of the Shuffler-based Differential Privacy](https://arxiv.org/abs/1908.11515) accepted  by VLDB 2021.

> Paper [Faster Secure Multiparty Computation of Adaptive Gradient Descent](https://dl.acm.org/doi/10.1145/3411501.3419427) accepted by the PPMLP workshop in Conjunction with CCS 2020.

> Paper [hPRESS: A Hardware-enhanced Proxy Re-encryption Scheme using Secure Enclave](https://ieeexplore.ieee.org/document/9187972) accepted by IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems.

2020.8
> Giving a [talk](https://isc.360.com/2020/another.html?uid=5010) about Federated learning and Secure Multi-party Computation in [ISC 2020](https://isc.360.com).

2020.2
> Paper [Privacy-preserving collaborative machine learning on genomic data using TensorFlow](https://arxiv.org/abs/2002.04344) accepted  to the Trustworthy ML Workshop co-located with ICLR 2020.

2020.1
> Paper "Secure Social Recommendation based on Secret Sharing" accepted by ECAI 2020.

> Paper "HomoPAI: A Secure Collaborative Machine Learning Platform based on Homomorphic Encryption" accepted by ICDE 2020 demo track. Watch the demo video on [Bilibili](https://www.bilibili.com/video/BV1Sz4y1e74z).

2019.12
> We are named the first place in Track IV of [iDASH2019 secure genome analysis competition](http://www.humangenomeprivacy.org/2019/). 
>
> We have open-sourced our competition code to [TF-Encrypted](https://github.com/tf-encrypted/tf-encrypted/pull/721) and received their [official acknowledgements](https://twitter.com/tf_encrypted/status/1215508893950201857).

> Attended NeurIPS 2019.

2019.11
> Invited as panelist to [2019 Westlake International Forum on Cyber Security Research](https://icsr.zju.edu.cn/xihu2019/en/).

> Joined [MPC Alliance](https://www.mpcalliance.org/).

2019.10
> Short paper [Quantification of the Leakage in Federated Learning](https://arxiv.org/abs/1910.05467) accepted by the Workshop on Federated Learning for Data Privacy and Confidentiality in Conjunction with CCS 2019.

> Paper [DPSAaS: Multi-Dimensional Data Sharing and Analytics as Services under Local Differential Privacy](http://www.vldb.org/pvldb/vol12/p1862-xu.pdf) accepted by VLDB 2019 demo track.

2019.9
> Established working group [P2842 - Recommended Practice for Secure Multi-party Computation](https://standards.ieee.org/project/2842.html) in IEEE Standards Association.

> Established working group [Technical framework and application for secure multi-party computation](https://www.itu.int/itu-t/workprog/wp_item.aspx?isn=15245) in ITU-T.

2019.8
> Attended [the 4th HomomorphicEncryption.org Standards Meeting](http://homomorphicencryption.org/).

> Attended USENIX Security 2019.

2019.3
> Paper [Answering multi-dimensional analytical queries under local differential privacy](https://dl.acm.org/doi/10.1145/3299869.3319891) accepted by SIGMOD 2019.

2019.1
> Paper [Covert Security with Public Verifiability: Faster, Leaner, and Simpler](https://eprint.iacr.org/2018/1108.pdf) accepted by EUROCRYPT 2019.

2018.11
> Invited as panelist to [2018 Westlake International Forum on Cyber Security Research](https://icsr.zju.edu.cn/xihu2018/en/index.htm).

2018.10
> Attended ACM CCS 2018.

2018.5
> Attended [TPMPC 2018](https://www.multipartycomputation.com/tpmpc-2018).

> Witnessed the [inaugural ceremony](https://www.zju.edu.cn/english/2018/0610/c19573a816865/page.htm) of the AZFT Cyberspace Security Lab.

2017.11
> Attended ACM CCS 2017.

  </div>

  <div id="ai" class="tab-content" markdown="1">

# AI Security & Privacy

### 2026.4
- Paper "[Fingerprinting LLMs via Prompt Injection](https://arxiv.org/abs/2509.25448)" accepted by ACL 2026.

### 2026.2
- Paper "[TEAR: Temporal-aware Automated Red-teaming for Text-to-Video Models](https://arxiv.org/abs/2511.21145)" accepted by CVPR 2026 (**Oral**).
  
### 2025.9
- Paper "MARS: A Malignity-Aware Backdoor Defense in Federated Learning" accepted by NeurIPS 2025.
- Paper "EnchTable: Unified Safety Alignment Transfer in Fine-tuned Large Language Models" accepted by SP 2026.

### 2025.7
- Attended ICML 2025 in Vancouver. Pictures: [pic1](https://raw.githubusercontent.com/AntCPLab/AntCPLab.github.io/master/assets/images/icml251.jpg) and [pic2](https://raw.githubusercontent.com/AntCPLab/AntCPLab.github.io/master/assets/images/icml252.jpg).
- Zhicong Huang serves as a PC member of USENIX Security 2026.

### 2025.5
- Paper "GaussMarker: Robust Dual-Domain Watermark for Diffusion Models" [[paper]](https://arxiv.org/abs/2506.11444) accepted by ICML 2025.
 
### 2025.4
- Zhicong Huang  serves as a PC member of ACM CCS 2025.
  
  </div>
</div>
