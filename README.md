# LangLands
# Introduction & Motivation

**Recent years have seen rapid developments in SNARKs, with provers becoming increasingly faster and the cost of verification becoming more affordable zkEVM has transitioned from a concept to reality, and RISC0 has even ushered in an era where any program can be verified. We now have various proof systems such as Halo2, Plonky2, Plonky3, EthStark, eStark, Spartan, and others.**

**These proof systems can generally be divided into front-end and back-end components. The front end primarily consists of constraint systems like Plonkish, AIR, and R1CS. The back-end, or Polynomial Commitment Scheme, mainly involves KZG, FRI, and Sumcheck.**

**For instance, Plonkish combined with KZG constitutes Halo2. A crucial factor is the choice of the domain for the Commitment Scheme, with smaller domains often being preferred.**

## Software Acceleration

**Looking back at the development history of these protocols, we can summarize the following trends in SNARK acceleration:**

1. **Choice of Domain**:
    - The primary difference between SNARK and STARK, for example, is that STARK's arithmetic circuit and commitment are in the same domain, and its domain is smaller than SNARK's scalar field and base field, granting STARK faster proof generation. Additionally, STARK's single-domain structure enhances its recursive performance over SNARK.
    - The Ulvetanna team has developed a new SNARK protocol, **Binius**, which operates in a 1-bit domain, achieving faster proof generation.
2. **Optimizing Protocol Details**: For example, Plonky2 enhances performance by reducing the layers in its Merkle Tree commitments and using the more ZK-friendly hash Poseidon2.
3. **Splitting Large Instruction Sets for Acceleration**: In zkVM, when the overall arithmetic circuit degree is high, using continuation to divide large instruction sets into smaller sets accelerates the process, effectively reducing circuit size by adding a layer of recursive circuits.
4. **Folding Scheme for Recursive Process Optimization**: Current options include Nova, ProtoStar, ProtoGalaxy, SuperNova, and HyperNova. ProtoStar, for instance, focuses on computing and committing cross-terms in each circuit folding, using the Perdson commitment scheme and committing witnesses, then folding both cross-terms and witnesses. However, its core still revolves around polynomial operations.
5. **Trade-offs in Circuit Writing**: This involves a balance between polynomial degree and quantity, with a preference for higher polynomial degrees in the final proof layer and more polynomials in earlier proofs.
6. **Lookup Innovations**: Lookups, vital for many zk applications like zkEVM, reduce instruction scale significantly, as seen in range checks. Recent advancements in lookup protocols (from Plonkup to Caulk, CQ, and Lasso) have lowered overall computational complexity from O(N*logN) to O(m*logm), where N is the table length and m is the query vector length.
7. **Potential for Non-structured Circuits (GKR) to Replace Structured Ones**

**Reflecting on these trends, we find that most optimizations eventually translate into enhancements in polynomial or polynomial commitment methods, signifying a trend towards optimizing these aspects in SNARK protocols.**

## Hardware Acceleration

**While these are predominantly software optimizations, another significant trend is hardware acceleration of operations like MSM, FFT, and NTT. For Plonk, around 80% of zk-SNARK proof generation time is spent on MSM, making its optimization crucial.**

**Current hardware acceleration methods include GPUs, FPGAs, and ASICs. For MSM, FFT, and NTT, notable GPU acceleration libraries are Icicle, Sppark, and Tachyon.**

**There are multiple GPU versions of Halo2, such as the Scroll, DelphinusLab, and Ingoyama versions.**

**GPU acceleration for Plonky2 is currently available in Ola's version and orbiter version.**

**Notable teams for FPGA acceleration include Cysis, Ingoyama, and Ulvetanna.**

**Overall, GPUs are the mainstream method, but FPGAs are becoming increasingly popular. (todo: ZPU)**

**However, we identify two issues with current hardware acceleration:**

1. Repetitive optimization of the same framework for halo2 by Scroll, Ingoyama, and DelphinusLab.
2. Integration challenges of libraries like Icicle and Sppark into one's protocols, typically allowing for the integration of only one due to resource constraints.
3. We currently lack many ZKP hardware acceleration engineers because there are very few people with the knowledge base of both ZKP and hardware acceleration, and the learning fields in these two fields are also very steep. We need to provide something like [https://learn.0xparc.org](https://learn.0xparc.org/) /halo2/’s courses to help more people enter this field.

**We aim to provide a user-friendly polynomial** repository **with comprehensive documentation, supporting both univariate and multivariate polynomials, along with commitment schemes like KZG, FRI, and Sumcheck. We plan to gradually include various lookup protocols like Caulk+ and CQ, Lasso, and integrate both Icicle and Sppark, along with future general acceleration libraries.**

This standard polynomial repository will be immensely beneficial for teams developing new proof systems. They can simply define their arithmetic constraints, including lookup arguments, and convert them into polynomial forms using our repository. This eliminates the need for developing a separate polynomial repository. Furthermore, our platform will be versatile, supporting various hardware accelerations like GPU, FPGA, and ASIC, offering flexibility and ease in selecting the most suitable hardware option.

**Additionally, we will offer a simple CUDA version of MSM code, akin to https://github.com/0xPARC/plonkathon, to onboard more developers into the field of ZKP GPU acceleration and collaboratively enhance this polynomial library.**

**To ensure we can filter most hardware acceleration libraries and provide diversity for the entire ZKP ecosystem and decentralized provers, we will explore efficient MSM acceleration on GPUs, FPGAs, and ASICs. We also aim to provide more educational articles to promote the flourishing development of the ZKP GPU acceleration industry.**

We will also try to explore our specialized FPGA version in the future to provide better performance. Our final goal is ASIC of ZK. Test the RTL design on FPGA is necessary our indispensable validation tool.

- FPGA offers greater flexibility, enabling the efficient solidification of unnecessary instruction flows and the creation of more optimized data pipelines.

- Presently, chip designs are predominantly closed-source, with specific details not openly disclosed due to commercial considerations. Nevertheless, a degree of openness in certain design aspects can enhance the diversity of the hardware ecosystem and mitigate the risk of supply chain attacks.

- On FPGA, MSM, NTT, and other algorithms have some open-source implementations from the academic community. Leveraging the team's expertise in Zero-Knowledge proofs (ZK), it can better validate and integrate these academic designs.

- This project can provide more possibilities for the future by making the Ethereum ZK layer less reliant on limited hardware companies. This will increase overall ecological diversity, decentralization, and resistance to censorship.

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

- What is your story?
*We'd love to hear more about you. What is your personal quest?*

    We want to create a project from scratch, starting from zero to one. This project aims to provide more possibilities for the future by making the Ethereum ZK layer less reliant on limited hardware companies. This will increase overall ecological diversity, decentralization, and resistance to censorship in the hardware perspective.

    Harold is a BSP engineer from China, who has 4+ years of experience developing driver for cryptographic hardware. during a year of exploration, I found Plancker DAO and did the research on Rollup, network state and so on with this community.
    Kenway is the CTO of XHash, have 15 years of software development experience and 4 years of blockchain work experience. Mainly focus on the research and achievement of the Ethereum consensus mechanism. How to make Ethereum more decentralized is my main work content.
    Yanlong is an experienced developer in the blockchain and Ethereum ecosystem. As a contributor of EthStorage, Yanlong focuses on its Proof-of-Storage ZK-SNARK algorithm. Additionally, Yanlong is a contributor of https://github.com/0xEigenLabs/eigen-zkvm, which focuses on implementing zkVM using STARK technology.

    XHash is a Web3.0 infrastructure provider, our vision is to build a stable, reliable, and secure blockchain infrastructure, provides POS staking service and multichain API to improve Web3.0 development with our customers.

    Plancker^ serves as a collaborative space dedicated to the Ethereum ecosystem, offering communication, education, treasure, and various resources to developers, product engineers, and researchers. Together, we are committed to building along the Ethereum roadmap, contributing to a digital future for all of humanity.

    Langlands is currently in close collaboration with Nebra. Considering that the current cloud infrastructure is more focused on AI scenarios, we are jointly dedicated to researching server configurations that are better suited for ZK business. This aims to provide improved services to a wide range of ZK teams. Additionally, we plan to collaboratively release a series of ZK Benchmarks and optimize relate software stack.

- Please describe your idea/project/research.
    
    ### **Description of the Idea/Project/Research:**
    
    Our project addresses critical challenges in the Zero-Knowledge Proof (ZKP) acceleration industry by focusing on the polynomial layer, serving as an intermediary between the higher-level proof systems and the underlying hardware acceleration technologies. In the current ZKP acceleration landscape, there is a significant gap between the development of proof systems and the efficient utilization of hardware resources. Our initiative aims to bridge this gap with a comprehensive solution.
    
    1. **Fragmentation in ZKP Acceleration**: Currently, the ZKP acceleration field is fragmented, with various teams working in isolation on either proof systems or hardware acceleration, leading to inefficiencies and duplicated efforts.
    2. **Integration Challenges Between Layers**: There is a lack of seamless integration between the advanced proof systems being developed and the hardware acceleration technologies available. This disconnection hinders the optimization and full utilization of resources.
    3. **Need for a Unified Middleware Solution**: There is a crucial requirement for a middleware solution that effectively translates the complex requirements of ZKP-proof systems into optimized hardware acceleration commands.
    
    Our project strategically positions itself at the polynomial layer, acting as a vital middleware that streamlines the interaction between sophisticated proof systems like SNARKs and STARKs and hardware acceleration technologies such as GPUs, FPGAs, and ASICs. By focusing on this layer, we aim to:
    
    - **Enhance Efficiency**: Optimize the polynomial computations which are fundamental to ZKP proof systems, ensuring they are tailored to leverage the full potential of the underlying hardware.
    - **Facilitate Integration**: Provide a unified platform that allows for easy integration of different proof systems with various hardware acceleration libraries, reducing the complexity and resource overhead for developers.
    - **Promote Scalability**: By optimizing at the polynomial layer, our solution directly contributes to the scalability of blockchain technologies, particularly Ethereum, by enabling faster and more efficient ZKP computations.
    
    Through our comprehensive polynomial library, we plan to support various commitment schemes and integrate major GPU acceleration libraries. Additionally, our CUDA-based MSM code will encourage more developers to participate in ZKP GPU acceleration. This holistic approach not only resolves the existing fragmentation in the ZKP acceleration industry but also empowers the Ethereum ecosystem to handle a larger scale of operations and a diverse range of applications more efficiently.
    
- How is your project onboarding the Next Billion users and reaching those underrepresented in the Ethereum community?
    
    Our project aims to onboard the next billion users and reach those underrepresented in the Ethereum community by leveraging the capabilities of Zero-Knowledge Proofs (ZKPs). ZKPs can effectively expand Ethereum's computational capacity. Unlike Ethereum's trust system, which is established through economic costs, ZKPs create a trust system derived from multi-party game theory. The core principle of both systems relies on the internet to transition from a human collaboration system, dependent on national or powerful entities for public trust, to a robust trust system where even the smallest entities can engage in commercial cooperation through ZKPs and Ethereum. This system enables transactions, akin to buying and selling goods, without relying on third-party platforms like Amazon.
    
    To realize this vision, we must generate ZKP proofs in an extremely short time. Hence, exploring the most efficient methods for generating ZKP proofs is crucial. Our focus on accelerating Multi-Scalar Multiplication (MSM) using FPGA, ASIC, and GPU technologies is essential since, for some proof systems, up to 80% of the computation time is spent on MSM. By maximizing the speed of MSM, we aim to bring ZKPs into practical use in real-world scenarios.
    
    This approach can potentially lead to a more equitable global wealth distribution by eliminating the need for powerful third-party entities and reducing military conflicts. By diminishing friction in commercial collaborations and fostering healthier production relationships, we can transmit individual credit through the ZKP+Ethereum trust network to every corner of the world.
    
- Roadmap and timeline for the project, in addition, or simultaneously to the Fellowship duration*
    - **Milestone 1**:
        - Completing educational versions of MSM, FFT, and NTT CUDA code (like https://github.com/0xPARC/plonkathon), along with analysis articles for Icicle and SPpark; plus additional MSM-related papers (EDMSM, PipeMSM, Pippenger).
    - **Milestone 2**:
        - Providing a comprehensive polynomial library supporting KZG and FRI schemes, compatible with Plonkup, offering acceleration options of SPpark and Icicle.
    - **Milestone 3**:
        - Integrating more lookup arguments, initially planning Caulk+, CQ, and Lasso, including GPU-accelerated versions.
    - **Milestone 4**:
        - Offer our proprietary FPGA version of MSM.
