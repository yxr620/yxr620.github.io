---
title: "Xiangrui Yang"
description: "PhD Student at HKU"
---

<div class="cv-hero">
<div class="cv-hero-text">
<div class="cv-hero-kicker">About Me</div>
<details class="cv-hero-bio-expand">
<summary>PhD @ HKU, advised by Yiming Qiu. MSc @ HUST · BSc @ SYSU. Research: ML systems, storage, HPC.</summary>
<div class="cv-hero-bio-full">
<p>PhD student @ HKU, advised by Prof. Yiming Qiu. MSc CS @ HUST (adv. Prof. Qiang Cao) · BSc CS @ SYSU (adv. Prof. Yuedong Yang).</p>
<p>Research: optimizing ML systems and HPC — CUDA, DGL, sparse matrix acceleration. Explored sparse ops in ad-ranking systems at Tencent.</p>
<p>Outside academia: economics and investment.</p>
</div>
</details>
</div>
<div class="cv-hero-photo">
<div class="cv-hero-photo-frame">
<img src="/images/user.jpg" alt="Xiangrui Yang" />
</div>
</div>
</div>

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

<details>
<summary>Education</summary>
<div style="padding-top:0.5rem">
<h3><a href="https://www.hku.hk/">University of Hong Kong</a></h3>
<p><em>PhD, Computer Science</em><br><strong>2025 – present</strong> · adv. Prof. Yiming Qiu</p>
<h3>Huazhong University of Science and Technology</h3>
<p><em>MSc, Computer Science</em><br><strong>2022 – 2025</strong> · Outstanding Graduate (Top 20%)</p>
<h3>Sun Yat-sen University</h3>
<p><em>BSc, Computer Science</em><br><strong>2018 – 2022</strong></p>
</div>
</details>

<details>
<summary>Talks &amp; Presentations</summary>
<ul style="padding-top:0.5rem">
<li>ICME'25, IEEE International Conference on Multimedia &amp; Expo 2025, Nantes, France. <a href="https://whova.com/embedded/session/hlWY6K3rL7pHvG8Yd1TfjYJVgDEZvOuEPKWGmeuUbIQ%3D/4654604/?widget=primary">Website</a></li>
<li>FAST'25, 23rd USENIX Conference on File and Storage Technologies, Santa Clara, California. <a href="https://www.youtube.com/watch?v=6dGa7Ol8Ryk">Video</a></li>
<li>SoCC'24, 15th ACM Symposium on Cloud Computing, Redmond, Washington.</li>
<li>HiPEAC'25, 20th High Performance, Edge And Cloud computing, Barcelona, Spain.</li>
</ul>
</details>

<details>
<summary>Experience</summary>
<div style="padding-top:0.5rem">
<h3><a href="https://www.tencent.com/en-us/">Tencent</a></h3>
<p><em>Advertising Engineering — Intern</em><br><strong>May 2024 – Sep 2024 &amp; Apr 2025 – Jun 2025</strong> · Shenzhen</p>
<ul>
<li>int8 quantization in ad scoring system: &gt;30% GPU kernel speedup, &gt;2% system throughput gain.</li>
<li>Added latency-analysis logs to ad recall system; tuned parameters to raise QPS from 10,000 to 15,000.</li>
</ul>
<h3><a href="https://www.sqhyfund.com/">Shengquan Hengyuan Investment</a></h3>
<p><em>Quantitative Finance Research — Intern</em><br><strong>Jun 2023 – Aug 2023</strong> · Nanjing</p>
<ul>
<li>&gt;30% annual cumulative abnormal return using high- and low-frequency signals.</li>
<li>Accelerated time-series and multi-factor model training with GPU servers.</li>
</ul>
<h3><a href="https://www.miracleplus.com/en/">Miracle Plus</a></h3>
<p><em>Investment &amp; Operations — Intern</em><br><strong>May 2023 – Jun 2023</strong> · Beijing</p>
<ul>
<li>Led diligence on a networking-industry startup that closed a Series A in the tens of millions.</li>
</ul>
<h3><a href="http://biomed.nscc-gz.cn/sail/en:research">SYSU AI4Science</a></h3>
<p><em>Data Analyst</em><br><strong>Jan 2022 – Jun 2022</strong> · Guangzhou</p>
<ul>
<li>Predicted Synthetic Lethality using random-walk + graph convolution with multi-view fusion.</li>
<li>Built message-passing models on CATL crystal database to predict physical properties.</li>
</ul>
</div>
</details>

<details>
<summary>Academic Projects</summary>
<div style="padding-top:0.5rem">
<h3>Model Optimization</h3>
<ul>
<li>Profiled DGL conv bottlenecks with Nsight; optimized GCN normalization for a 30% speedup over DGL.</li>
<li>C++/CUDA extensions for Python; CUDA operator overloading.</li>
</ul>
<h3>Reed-Solomon Code Optimization</h3>
<ul>
<li>Compared wide- vs narrow-stripe erasure codes (ISA-L / Jerasure); reached 128 Gbps single-node throughput via OpenMP.</li>
</ul>
<h3>SSD Optimization</h3>
<ul>
<li>Built SSDTEST to characterize performance degradation; developed I/O scheduler to control tail latency.</li>
</ul>
</div>
</details>

<details>
<summary>Certificates &amp; Awards</summary>
<div style="padding-top:0.5rem">
<h3>Awards</h3>
<ul>
<li>Sangfor Scholarship (Apr. 2024)</li>
<li>HUST Scholarship, Second Prize (Oct. 2023)</li>
<li>Distinguished Activist in Community Affairs (Oct. 2023)</li>
<li>SYSU Scholarship, Second Prize (Oct. 2021)</li>
<li>2019 ACM-ICPC SYSU Competition, Second Prize (Oct. 2019)</li>
</ul>
<h3>Certificates</h3>
<ul>
<li>IELTS 7.0 · GRE 320 · TOEFL 106</li>
</ul>
</div>
</details>
