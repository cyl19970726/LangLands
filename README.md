# LangLands
# Introduction & Motivation

**Recent years have seen rapid developments in SNARKs, with provers becoming increasingly faster and the cost of verification becoming more affordable zkEVM has transitioned from a concept to reality, and RISC0 has even ushered in an era where any program can be verified. We now have various proof systems such as Halo2, Plonky2, Plonky3, EthStark, eStark, Spartan, and others.**

**These proof systems can generally be divided into front-end and back-end components. The front-end primarily consists of constraint systems like Plonkish, AIR, and R1CS. The back-end, or Polynomial Commitment Scheme, mainly involves KZG, FRI, and Sumcheck.**

**For instance, Plonkish combined with KZG constitutes Halo2. A crucial factor is the choice of the domain for the Commitment Scheme, with smaller domains often being preferred.**

## Software Acceleration

**Looking back at the development history of these protocols, we can summarize the following trends in SNARK acceleration:**

1. **Choice of Domain**:
    - The primary difference between SNARK and STARK, for example, is that STARK's arithmetic circuit and commitment are in the same domain, and its domain is smaller than SNARK's scalar field and base field, granting STARK faster proof generation. Additionally, STARK's single-domain structure enhances its recursive performance over SNARK.
    - The Ulvetanna team has developed a new SNARK protocol, **Binius**, which operates in a 1-bit domain, achieving faster proof generation.
2. **Optimizing Protocol Details**: For example, Plonky2 enhances performance by reducing the layers in its Merkle Tree commitments and using the more ZK-friendly hash Poseidon2.
3. **Splitting Large Instruction Sets for Acceleration**: In zkVM, when the overall arithmetic circuit degree is high, using continuation to divide large instruction sets into smaller sets accelerates the process, effectively reducing circuit size by adding a layer of recursive circuits.
4. **Folding Scheme for Recursive Process Optimization**: Current options include Nova, ProtoStar, ProtoGalaxy, SuperNova, and HyperNova. ProtoStar, for instance, focuses on computing and committing cross-terms in each circuit folding, using Perdson commitment scheme and committing witnesses, then folding both cross-terms and witnesses. However, its core still revolves around polynomial operations.
5. **Trade-offs in Circuit Writing**: This involves a balance between polynomial degree and quantity, with a preference for higher polynomial degrees in the final proof layer and more polynomials in earlier proofs.
6. **Lookup Innovations**: Lookups, vital for many zk applications like zkEVM, reduce instruction scale significantly, as seen in range checks. Recent advancements in lookup protocols (from Plonkup to Caulk, CQ, and Lasso) have lowered overall computational complexity from O(N*logN) to O(m*logm), where N is the table length and m is the query vector length.
7. **Potential for Non-structured Circuits (GKR) to Replace Structured Ones**

**Reflecting on these trends, we find that most optimizations eventually translate into enhancements in polynomial or polynomial commitment methods, signifying a trend towards optimizing these aspects in SNARK protocols.**

## Hardware Acceleration

**While these are predominantly software optimizations, another significant trend is hardware acceleration of operations like MSM, FFT, NTT. For Plonk, around 80% of zk-SNARK proof generation time is spent on MSM, making its optimization crucial.**

**Current hardware acceleration methods include GPUs, FPGAs, and ASICs. For MSM, FFT, and NTT, notable GPU acceleration libraries are Icicle, Sppark, and Tachyon.**

**There are multiple GPU versions of Halo2, such as the Scroll, DelphinusLab, and Ingoyama versions.**

**GPU acceleration for Plonky2 is currently available in Ola's version and orbiter version.**

**Notable teams for FPGA acceleration include Cysis, Ingoyama, and Ulvetanna.**

**Overall, GPUs are the mainstream method, but FPGAs are becoming increasingly popular. (todo: ZPU)**

**However, we identify two issues with current hardware acceleration:**

1. Repetitive optimization of the same framework for halo2 by Scroll, Ingoyama, and DelphinusLab.
2. Integration challenges of libraries like Icicle and Sppark into one's protocols, typically allowing for the integration of only one due to resource constraints.
3. We currently lack many ZKP hardware acceleration engineers because there are very few people with the knowledge base of both zkp and hardware acceleration, and the learning fields in these two fields are also very steep. We need to provide something like [https://learn.0xparc.org](https://learn.0xparc.org/) /halo2/’s courses to help more people enter this field.

**We aim to provide a user-friendly polynomial** repository **with comprehensive documentation, supporting both univariate and multivariate polynomials, along with commitment schemes like KZG, FRI, Sumcheck. We plan to gradually include various lookup protocols like Caulk+ and CQ, Lasso, and integrate both Icicle and Sppark, along with future general acceleration libraries.**

This standard polynomial repository will be immensely beneficial for teams developing new proof systems. They can simply define their arithmetic constraints, including lookup arguments, and convert them into polynomial forms using our repository. This eliminates the need for developing a separate polynomial repository. Furthermore, our platform will be versatile, supporting various hardware accelerations like GPU, FPGA, and ASIC, offering flexibility and ease in selecting the most suitable hardware option.

**Additionally, we will offer a simple CUDA version of MSM code, akin to https://github.com/0xPARC/plonkathon, to onboard more developers into the field of ZKP GPU acceleration and collaboratively enhance this polynomial library.**

**To ensure we can filter most hardware acceleration libraries and provide diversity for the entire ZKP ecosystem and decentralized provers, we will explore efficient MSM acceleration on GPUs, FPGAs, and ASICs. We also aim to provide more educational articles to promote the flourishing development of the ZKP GPU acceleration industry.**

We will also try to explore our specialized FPGA version in the future to provide better performance.  In the context of Zero-Knowledge Proofs (ZKP), the choice between FPGA (Field-Programmable Gate Array) and GPU (Graphics Processing Unit) for hardware acceleration is pivotal. Recent developments indicate a nuanced comparison:

- Performance-per-Watt: FPGAs match GPUs in terms of performance-per-watt, which is crucial for applications where energy efficiency is a priority. However, FPGAs fall behind in performance-per-dollar compared to GPUs, making them less cost-effective in some scenarios .
- Application-Specific Acceleration: FPGA's architecture allows for more customized and application-specific acceleration. This is particularly beneficial for ZKP computations like MSM (Multi-Scalar Multiplication), where FPGAs can be tailored to optimize these specific operations .
- ZPrize Incentives: Competitions like ZPrize are motivating teams to develop hardware acceleration solutions for key ZKP bottlenecks (MSM, NTT, Poseidon, etc.) on various platforms, including FPGAs.
- Advantages in ZKP Calculations: The advantages and disadvantages of FPGAs and GPUs vary in accelerating zero-knowledge proof calculations. Factors like the specific computation (e.g., MSM) and the desired balance between energy efficiency and cost play a significant role in determining the ideal hardware choice].
- Disadvantages of FPGAs: A notable downside of FPGAs is their limited flexibility compared to GPUs. This can impact their adaptability in some ZKP applications.
- State-of-the-Art Solutions: Recent FPGA implementations, especially for MSM on specific curves like BLS12-377, have outperformed existing state-of-the-art solutions, showcasing FPGA's potential in ZKP acceleration.

These insights suggest that while FPGAs offer significant advantages in customization and energy efficiency for ZKP computations, their cost-effectiveness and adaptability may be lower compared to GPUs.

## Project Scope

In summary, our team is dedicated to integrating a broader range of general hardware acceleration libraries into a comprehensive polynomial library. This integration aims to facilitate more efficient Zero-Knowledge Proof (ZKP) processing. Key aspects of our focus include:

1. **Comprehensive Polynomial Library Development**: Creating a unified polynomial library that incorporates various hardware acceleration libraries, enhancing the efficiency and flexibility of ZKP computations.
2. **Educational Content on ZKP Hardware Acceleration**: Producing educational materials to demystify and simplify the understanding of ZKP hardware acceleration. This initiative will help onboard more developers and researchers into the field.
3. **Exploration of FPGA-Based MSM Algorithm**: Investigating and developing an FPGA version of the Multi-Scalar Multiplication (MSM) algorithm. FPGA technology offers promising performance-per-watt efficiency, making it an intriguing area for research and development in ZKP acceleration [[1](https://hackmd.io/@Cysic/BJQcpVbXn)][[2](https://www.paradigm.xyz/2022/04/zk-hardware)][[3](https://www.ingonyama.com/blog/hardware-review-gpus-fpgas-and-zero-knowledge-proofs)].

 

**Our team's milestones include:**

- **Milestone 1**:
    - Completing educational versions of MSM, FFT, and NTT CUDA code (like https://github.com/0xPARC/plonkathon), along with analysis articles for Icicle and SPpark; plus additional MSM-related papers (EDMSM, PipeMSM, Pippenger).
- **Milestone 2**:
    - Providing a comprehensive polynomial library supporting KZG and FRI schemes, compatible with Plonkup, offering acceleration options of SPpark and Icicle.
- **Milestone 3**:
    - Integrating more lookup arguments, initially planning Caulk+, CQ, and Lasso, including GPU-accelerated versions.
- **Milestone 4**:
    - Offer our proprietary FPGA version of MSM.
    

# Apply EF Grant

- Please describe your idea/project/research.
    
    ### **Description of the Idea/Project/Research:**
    
    Our project addresses critical challenges in the Zero-Knowledge Proof (ZKP) acceleration industry by focusing on the polynomial layer, serving as an intermediary between the higher-level proof systems and the underlying hardware acceleration technologies. In the current ZKP acceleration landscape, there is a significant gap between the development of proof systems and the efficient utilization of hardware resources. Our initiative aims to bridge this gap with a comprehensive solution.
    
    1. **Fragmentation in ZKP Acceleration**: Currently, the ZKP acceleration field is fragmented, with various teams working in isolation on either proof systems or hardware acceleration, leading to inefficiencies and duplicated efforts.
    2. **Integration Challenges Between Layers**: There is a lack of seamless integration between the advanced proof systems being developed and the hardware acceleration technologies available. This disconnection hinders the optimization and full utilization of resources.
    3. **Need for a Unified Middleware Solution**: There is a crucial requirement for a middleware solution that effectively translates the complex requirements of ZKP proof systems into optimized hardware acceleration commands.
    
    Our project strategically positions itself at the polynomial layer, acting as a vital middleware that streamlines the interaction between sophisticated proof systems like SNARKs and STARKs and the hardware acceleration technologies such as GPUs, FPGAs, and ASICs. By focusing on this layer, we aim to:
    
    - **Enhance Efficiency**: Optimize the polynomial computations which are fundamental to ZKP proof systems, ensuring they are tailored to leverage the full potential of the underlying hardware.
    - **Facilitate Integration**: Provide a unified platform that allows for easy integration of different proof systems with various hardware acceleration libraries, reducing the complexity and resource overhead for developers.
    - **Promote Scalability**: By optimizing at the polynomial layer, our solution directly contributes to the scalability of blockchain technologies, particularly Ethereum, by enabling faster and more efficient ZKP computations.
    
    Through our comprehensive polynomial library, we plan to support various commitment schemes and integrate major GPU acceleration libraries. Additionally, our CUDA-based MSM code will encourage more developers to participate in ZKP GPU acceleration. This holistic approach not only resolves the existing fragmentation in the ZKP acceleration industry but also empowers the Ethereum ecosystem to handle a larger scale of operations and a diverse range of applications more efficiently.
    
- How is your project onboarding the Next Billion users and reaching those underrepresented in the Ethereum community?
    
    Our project aims to onboard the next billion users and reach those underrepresented in the Ethereum community by leveraging the capabilities of Zero-Knowledge Proofs (ZKPs). ZKPs can effectively expand Ethereum's computational capacity. Unlike Ethereum's trust system, which is established through economic costs, ZKPs create a trust system derived from multi-party game theory. The core principle of both systems relies on the internet to transition from a human collaboration system, dependent on national or powerful entities for public trust, to a robust trust system where even the smallest entities can engage in commercial cooperation through ZKPs and Ethereum. This system enables transactions, akin to buying and selling
