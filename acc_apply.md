> [!IMPORTANT]
A proposal will go through a review process by a PSE to ensure the quality of the task and alignment with the acceleration program mission. Please be patient and wait for the review to complete.
> 

### Open Task RFP for Langlands

### Executive Summary

- Project Overview: Implement KZG over a polynomial repository and integrate Sppark and Icicle

### Project Details

- Motivation:
    - Different high-performance hardware-accelerated versions of the same proof system, developed by various teams, are often proprietary. Because, for most teams, it serves as a vital weapon that allows them to survive in commercial competition. This situation is similar to the existence of multiple GPU versions of a game like Halo2. For example, some famous versions are from the Scroll, DelphinusLab, Tachyon, and Ingonyama versions. Each version brings unique features or performance enhancements that provide a competitive edge in the market. However, we believe this pattern may not maximize value as it leads to duplication of work among developers.
    - Insert a layer between a proof system and a hardware acceleration library. It is expected more general acceleration libraries in the future, working on GPUs, ASICs, and FPGAs. However, it would be impractical and time-consuming to integrate so many hardware acceleration libraries and compare their performances. To address this challenge, we propose the addition of an intermediate layer between a proof system and a hardware acceleration library. It would allow teams developing proof systems to integrate this middle layer and seamlessly switch between different hardware acceleration libraries, without the need for extensive integration efforts. ZPU is a polynomial library developed by Ingonyama. It is a potential solution by extending the upper polynomial layer of ZPU since all proof systems essentially operate on polynomials. Our work would provide a useful polynomial library integrated with sufficient common hardware acceleration libraries.
    - Develop courses for beginners and developers. There is a huge shortage of ZKP hardware acceleration engineers in the market. One of the reasons is the steep learning curves for gaining a solid knowledge of ZKP and hardware acceleration. To address this challenge, we will develop tutorial courses based on our experiences to help more developers enter this area. The proposed courses would be similar to those offered in the Halo2 program https://learn.0xparc.org/, but be more beginner-friendly and up-to-date. 
- Scope of Work:
    - Choose a polynomial library that is general enough. We have tentatively decided to select https://github.com/arkworks-rs/algebra/tree/master/poly as the repository to develop. This repository provides a wide range of functionality and features that make it suitable for handling various polynomial-related tasks.
    - Implement KZG(Kate-Zaverucha-Groth) over this polynomial repository and integrate Sppark and Icicle libraries.
    - Output some educational content on developing the MSM algorithm using CUDA and the comparative analysis of different MSM-CUDA versions developed by different awesome teams.
- Expected Outcomes:
    - Implementation of KZG over the chosen polynomial repository and seamless integration of the Sppark and Icicle libraries to enhance the functionality and security of the scheme.
    - Support cq's lookup protocol

### Qualifications

- Skills Required:
    - Deep understanding of SNARK
    - Good rust development capabilities
    - Good understanding of GPU programming
- Preferred Qualifications:
    - Excellent English document writing skills

### Administrative Details

- Estimated Project Duration:
    The deadline is February 31
- Project Complexity:
    - 这句话是不是有问题，Medium, Because to complete this work, you need to have a certain understanding of a variety of technologies. Still, you do not need to have a deep understanding of every technical field, and more work is to find some better technical solutions on the market. , combine them.

### Additional Information

- Reference Material:
    - The ultimate goal of this project is to integrate most of the popular lookup arguments and commit schemes.
    - Icicle: https://github.com/ingonyama-zk/icicle.git
    - Sppark: https://github.com/supranational/sppark.git
****
