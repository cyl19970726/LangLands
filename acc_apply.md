> [!IMPORTANT]
A proposal will go through a review process by a PSE to ensure the quality of the task and alignment with the acceleration program mission. Please be patient and wait for the review to complete.
> 

### Open Task RFP for Langlands

### Executive Summary

- Project Overview: Implement KZG over a polynomial repo and integrate Sppark and Icicle

### Project Details

- Motivation:
    - The different high-performance hardware-accelerated versions of the same proof system, developed by various teams, are often proprietary because, for most teams, it is a vital weapon that allows them to survive in commercial competition. This situation is similar to the existence of multiple GPU versions of a game like Halo2, with examples including the Scroll, DelphinusLab, Tachyon, and Ingoyama versions. Each version, developed by different teams, brings unique features or performance enhancements that provide a competitive edge in the market. But I don’t think this is the way to maximize value because developers often do a lot of duplication of work.
    - In the future, there may be more such general acceleration libraries that not only work on GPUs but also on ASICs and FPGAs. So for most teams, it is impossible for them to spend a lot of time integrating so much hardware. acceleration libraries and compare their performance differences one by one. We need to add an intermediate layer to the proof system and the hardware acceleration library so that most teams that develop proof systems only need to integrate this middle layer to run on different hardware flexibly. Switch between acceleration plans. Zpu is a potential solution, but we hope to do this in the upper polynomial layer of ZPU developed by Ingoyama, because for all proof systems, they essentially end up operating on polynomials, so we hope to provide a useful polynomial library and integrate enough common hardware acceleration libraries on this library.
    - We currently lack many ZKP hardware acceleration engineers because there are very few people with the knowledge base of both ZKP and hardware acceleration, and the learning fields in these two fields are also very steep. We need to provide something like https://learn.0xparc.org/ /halo2/’s courses to help more developers enter this area.
- Scope of Work:
    - Choose a polynomial library that is general enough, and we decide to select https://github.com/arkworks-rs/algebra/tree/master/poly as the repo to develop.
    - Implement KZG over this polynomial repo and integrate Sppark and Icicle
    - We plan to output some educational content about developing the MSM algorithm using Cuda and compare it with different MSM-CUDA versions developed by different awesome teams.
- Expected Outcomes:
    - Implement KZG over this polynomial repo and integrate Sppark and Icicle.
    - Support CQ lookup argument
    - Write an article to summarize the similarities and differences between Icicle and Sppark in the implementation of the MSM algorithm and compare the performance data.

### Qualifications

- Skills Required:
    - Good rust development capabilities
    - A deep understanding of snark
    - A certain understanding of GPU programming
- Preferred Qualifications:
    - Excellent document writing skills

### Administrative Details

- Estimated Project Duration:
    The deadline is February 31
- Project Complexity:
    - Medium, Because to complete this work, you need to have a certain understanding of a variety of technologies. Still, you do not need to have a deep understanding of every technical field, and more work is to find some better technical solutions on the market. , combine them.

### Additional Information

- Reference Material:
    - We ultimately hope that this project can integrate more lookup arguments and more commit schemes.
    - icicle: https://github.com/ingonyama-zk/icicle.git
    - sppark: https://github.com/supranational/sppark.git
