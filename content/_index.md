---
title: "Xiangrui Yang"
description: "🎓 PhD Student @ HKU | 🔬 ML Systems & HPC Research"
---

<div class="cv-hero">
<div class="cv-hero-text">
<p class="cv-hero-label">I work on machine learning systems, storage systems, and high-performance computing, with an emphasis on practical performance optimization.</p>
<div class="cv-contact-row">
<span class="cv-contact-item">📧 <a href="mailto:yxr620@gmail.com">yxr620@gmail.com</a></span>
<span class="cv-contact-item">📱 (+86) 18963961350</span>
</div>
<div class="cv-social-links">
<a href="https://github.com/yxr620">GitHub</a>
<a href="/blog/">Blog</a>
<a href="#academic-papers">Selected Papers</a>
</div>
</div>
<div class="cv-hero-photo">
<img src="/images/user.jpg" alt="Xiangrui Yang" />
</div>
</div>

---

## About Me

I am a first-year PhD student at the University of Hong Kong, advised by Professor [Yiming Qiu](https://yimingqiu.me/). I received my Master's degree in Computer Science from Huazhong University of Science and Technology (HUST), advised by Professor [Qiang Cao](http://english.cs.hust.edu.cn/info/1464/1194.htm), and my Bachelor's degree in Computer Science from Sun Yat-Sen University (SYSU), advised by Professor [Yuedong Yang](https://cse.sysu.edu.cn/content/2951). 

My research interests lie in the optimization of machine learning systems and high-performance computing. I have experience working with tools like CUDA and DGL for model acceleration. I researched sparse matrix multiplication in an advertisement scoring system during the internship at Tencent. 

Outside of academia, I enjoy diving into economics and investment.

---

## Academic Papers

- [HeteroGNN: A Heterogeneous Task Division Based GNN Training Framework to Maximize CPU-GPU Parallelism](https://ieeexplore.ieee.org/document/11209980), **ICME 2025**
- [Rearchitecting Buffered I/O in the Era of High-Bandwidth SSDs](https://www.usenix.org/conference/fast26/presentation/zhan), **FAST 2026**
- ASMA: An Anisotropy Scaling Memristor-based Accelerator for LLM Inference, **ICCD 2025**
- [Rethinking the Request-to-IO Transformation Process of File Systems for Full Utilization of High-Bandwidth SSDs](https://www.usenix.org/conference/fast25/presentation/zhan), **FAST'25**
- [AIS: An Active Idleness I/O Scheduler to Reduce Buffer-Exhausted Degradation for Commodity SSDs](https://dl.acm.org/doi/10.1145/3708538), **ACM TACO**
- [RomeFS: A CXL-SSD Aware File System Exploiting Synergy of Memory-Block Dual Paths](https://dl.acm.org/doi/10.1145/3698038.3698539), **SoCC'24**
- [HEncode: A Highly Modularized and Efficient FPGA QC-LDPC Encoder Using High Level Synthesis](https://ieeexplore.ieee.org/document/10818010/), **ICCD'24**
- [A Study on Data-Layout Optimization in Memory for High-Performance Erasure Coding](http://xwxt.sict.ac.cn/CN/Y2025/V46/I4/1003)
- [Analyzing performance degradation for wide stripe erasure codes](https://www.spiedigitallibrary.org/conference-proceedings-of-spie/13067/130670E/Analyzing-performance-degradation-for-wide-stripe-erasure-codes/10.1117/12.3024709.full)
- [PMLDS: An LSM-tree Direct Managed Storage for Key-value Stores on Byte-addressable Devices](https://dl.acm.org/doi/10.1145/3605573.3605629)
- [Leveraging Orbital Information and Atomic Feature in Deep Learning Model](https://arxiv.org/abs/2211.11543)

---

## Education Background

### **University of Hong Kong**  
*Department of Computer Science, PhD*  
**Duration**: Nov. 2025 - Now  
**Supervisor**: Professor Yiming Qiu

### **Huazhong University of Science and Technology**  
*School of Computer Science and Technology, Master Degree*  
**Duration**: Sep. 2022 - Jun. 2025  
**Honor**: Outstanding Graduate (Top 20\%) 

### **Sun Yat-sen University**  
*School of Computer Science and Engineering, Bachelor Degree*  
**Duration**: Sep. 2018 - Jun. 2022 

---

## Talks & Presentations

- ICME'25, IEEE International Conference on Multimedia & Expo 2025, Nantes, France. [Website](https://whova.com/embedded/session/hlWY6K3rL7pHvG8Yd1TfjYJVgDEZvOuEPKWGmeuUbIQ%3D/4654604/?widget=primary)
- FAST'25, 23rd USENIX Conference on File and Storage Technologies, Santa Clara, California. [Video](https://www.youtube.com/watch?v=6dGa7Ol8Ryk)
- SoCC'24, 15th ACM Symposium on Cloud Computing, Redmond, Washington.
- HiPEAC'25, 20th High Performance, Edge And Cloud computing, Barcelona, Spain.

---


## Internship

### [Tencent](https://www.tencent.com/en-us/)
*Advertising Engineering Department Intern*  
**Duration**: May. 2024 - Sep. 2024  & Apr. 2025 - Jun. 2025  
**Location**: Shenzhen  

- Used int8 quantization in Advertisement scoring system, achieving over 30\% time reduction on GPU kernel functions and over 2\% system throughput.
- Added new time-consuming analysis logs to the advertising recall system and adjusted the parameter settings to increase the QPS from 10,000 to 15,000.

### [Shengquan Hengyuan Investment Company](https://www.sqhyfund.com/)

*Quantitative Finance Researcher Intern*  
**Duration**: Jun. 2023 - Aug. 2023  
**Location**: Nanjing 


- Achieved annual cumulative abnormal return of over 30\% using both high and low frequency trading information.
- Participated in configuring the training environment for GPU servers and accelerated the training process of time series models and multi-factor models with GPU servers.


### [Miracle Plus](https://www.miracleplus.com/en/)
*Investment and Operations Assistant Intern*  
**Duration**: May. 2023 - Jun. 2023  
**Location**: Beijing

- Invested in an important startup in networking industry, with a Series A funding round in the tens of millions.


### [SYSU AI4Science](http://biomed.nscc-gz.cn/sail/en:research)

*Data Analyst*  
**Duration**: Jan. 2022 - Jun. 2022  
**Location**: Guangzhou  

- Extracted genetic relationships using random walking, and predicted Synthetic Lethality using a model constructed on a graph convolution network combined with a multi-view method.
- Used crystal database provided by Contemporary Amperex Technology Co. Limited to build message passing model to predict the physical characteristics of crystals.


---

## Academic Projects

### **Model Optimization Works**  
- Analyzed the bottlenecks in the convolutional modules of DGL using tools such as Nsight System and Nsight Compute, optimized the normalization module in Graph Convolutional Networks (GCN) based on sampling results, achieving a 30\% improvement over DGL
- Proficient in using the cpp\_extension tool to write C libraries for Python and capable of implementing CUDA operator overloading.
- Developed deep learning models using the deep graph model library DGL and got familiar with common Python libraries such as Pandas, Numpy, and Pytorch. 
- Skilled in using the Linux development environment and environment control tools like Conda and Docker.

### **Reed-Solomon Code Optimization**  
- Analyzed the performance of wide-stripe and narrow-stripe erasure codes using the ISA-L and Jerasure encoding libraries, and compared the underlying finite field implementations.
- Achieved single node encoding throughput of 128 Gbps using existing RS encoding libraries with an OpenMP multithread implementation.

### **Solid-State Drive Optimization**  
- Developed SSDTEST to evaluate the performance of SSDs and the performance degradation to further modeling this phenomenon.
- Developed SSD IO scheduler to control the tail latency of SSD especially during the performance degradation.

---

## Certificates and Awards

### Awards
- Sangfor Scholarship (Apr. 2024)
- Huazhong University of Science and Technology Scholarship, Second Prize (Oct. 2023)
- Distinguished Activist in Community Affairs (Oct. 2023)
- Sun Yat-sen University Scholarship, Second Prize (Oct. 2021)
- 2019 ACM-ICPC Sun Yat-sen University Competition, Second Prize, Guangzhou (Oct. 2019)


### Certificates
- IELTS (International English Language Testing System) 7.0
- GRE (Graduate Record Examinations) 320
- TOEFL (Test of English as a Foreign Language) 106