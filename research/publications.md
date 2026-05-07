# Publications

> Collection of papers, talks, videos, and blog posts on world models, JEPA, EBMs, and BDH

**Last Updated**: 2026-05-07

---

## JEPA (Joint-Embedding Predictive Architecture)

*Papers, talks, and videos specifically about JEPA*

### V-JEPA 2.1: Unlocking Dense Features in Video Self-Supervised Learning [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2603.14482)

**Authors/Presenters**: Lorenzo Mur-Labadia, Matthew Muckley, Amir Bar, Mido Assran, Koustuv Sinha, Mike Rabbat, [Yann LeCun](players.md#yann-lecun), Nicolas Ballas, Adrien Bardes

**Date**: 2026-03

**Summary**: New family of self-supervised video models producing dense, high-quality visual representations through dense predictive losses (both visible and masked tokens contribute training signal), hierarchical self-supervision across intermediate encoder layers, multi-modal tokenizers for unified image-video training, and effective scaling. Successor to V-JEPA 2.

**Key Findings**:

- 20-point improvement in robot grasping success over V-JEPA 2; 7.71 mAP on Ego4D object-interaction anticipation, 40.8 Recall@5 on EPIC-KITCHENS action anticipation
- Dense predictive loss where both visible and masked tokens provide training signal, unlike standard JEPA masking where only masked tokens contribute
- Deep self-supervision applied across multiple intermediate encoder layers improves spatial, semantic, and temporal coherence of learned features

**Relevance to World Models**: Direct successor to V-JEPA 2, addressing its weakness in dense (per-pixel/per-patch) feature quality while maintaining strong global representations. The 20-point robotics improvement demonstrates that dense features matter for world model downstream tasks — global scene understanding alone is insufficient for fine-grained manipulation planning.

### VL-JEPA: Joint Embedding Predictive Architecture for Vision-language [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2512.10942)

**Authors/Presenters**: Delong Chen, Mustafa Shukor, Theo Moutakanni, Willy Chung, Jade Yu, Tejaswi Kasarla, Yejin Bang, Allen Bolourchi, [Yann LeCun](players.md#yann-lecun), Pascale Fung

**Date**: 2025-12 (revised 2026-02)

**Summary**: Extends JEPA to vision-language by predicting continuous text embeddings instead of autoregressive token generation. Achieves stronger performance with 50% fewer trainable parameters than standard VLM training, demonstrating that JEPA's prediction-in-representation-space principle transfers effectively to multimodal settings.

**Key Findings**:

- Replaces token-space prediction with continuous embedding prediction; natively supports adaptive decoding reducing operations by 2.85x
- Surpasses CLIP, SigLIP2, and Perception Encoder across 16 video datasets; comparable to InstructBLIP and QwenVL on VQA benchmarks (GQA, TallyQA, POPE, POPEv2)
- 1.6B parameter model supports open-vocabulary classification, text-to-video retrieval, and discriminative VQA without architectural modification

**Relevance to World Models**: Demonstrates JEPA's scalability beyond vision to multimodal settings, a key step toward world models that integrate language understanding with visual prediction. Validates that predicting in embedding space (rather than token space) is viable for language tasks.

### VLA-JEPA: Enhancing Vision-Language-Action Model with Latent World Model [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2602.10098)

**Authors/Presenters**: Jingwen Sun, Wenyao Zhang, Zekun Qi, Shaojie Ren, Zezhi Liu, Hanxin Zhu, Guangzhong Sun, Xin Jin, Zhibo Chen

**Date**: 2026-02

**Summary**: JEPA-style pretraining framework for VLA policies using leakage-free state prediction — a target encoder produces latent representations from future frames while the student sees only current observation. Addresses the core VLA limitation that latent-action objectives anchor to pixel variation rather than action-relevant state transitions.

**Key Findings**:

- Leakage-free design: future information used solely as supervision targets, never as input — prevents shortcuts that bypass dynamics learning
- Uses V-JEPA2 encoder + predictor as latent world model; Qwen3-VL-2B as VLM backbone
- Two-stage recipe (JEPA pretraining → action-head fine-tuning) eliminates multi-stage complexity of prior approaches
- Consistent gains on LIBERO, LIBERO-Plus, SimplerEnv, and real-world manipulation in generalization and robustness

**Relevance to World Models**: Directly integrates JEPA world models into VLA training, addressing the key criticism that VLAs lack causal understanding of dynamics. By predicting in latent space rather than pixel space, VLA-JEPA learns abstractions robust to camera motion and irrelevant background changes — the same property that makes JEPA world models effective for planning.

### LeWorldModel: Stable End-to-End Joint-Embedding Predictive Architecture from Pixels [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2603.19312)

**Authors/Presenters**: Lucas Maes, Quentin Le Lidec, Damien Scieur, [Yann LeCun](players.md#yann-lecun), Randall Balestriero

**Date**: 2026-03

**Summary**: First JEPA that trains stably end-to-end from raw pixels using only two loss terms: a next-embedding prediction loss and a regularizer enforcing Gaussian-distributed latent embeddings. Reduces tunable loss hyperparameters from six to one compared to the only existing end-to-end alternative, with ~15M parameters trainable on a single GPU in hours.

**Key Findings**:

- Plans up to 48x faster than foundation-model-based world models while remaining competitive across diverse 2D and 3D control tasks
- Avoids representation collapse without exponential moving averages, pre-trained encoders, or auxiliary supervision — only two loss terms needed
- Latent space encodes meaningful physical structure; model detects physically implausible events through surprise evaluation

**Relevance to World Models**: Directly addresses the fragility problem that has limited JEPA adoption for world modeling. By dramatically simplifying the training recipe (2 loss terms vs. 6), LeWM lowers the barrier to building JEPA-based world models from scratch without relying on foundation model encoders.

### Causal-JEPA: Learning World Models through Object-Level Latent Interventions [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2602.11389)

**Authors/Presenters**: Heejeong Nam, Quentin Le Lidec, Lucas Maes, [Yann LeCun](players.md#yann-lecun), Randall Balestriero

**Date**: 2026-02

**Summary**: Extends JEPA masking from image patches to object-centric representations, inducing causal inductive bias via latent interventions. Object-level masking requires an object's state to be inferred from other objects, preventing shortcut solutions and making interaction reasoning essential for learning dynamics.

**Key Findings**:

- ~20% absolute improvement in counterfactual reasoning on visual question answering vs. same architecture without object-level masking
- Achieves comparable planning performance using only 1% of the total latent input features required by patch-based world models
- Formal analysis proves object-level masking induces causal inductive bias via latent interventions with counterfactual-like effects

**Relevance to World Models**: Moves JEPA world models from correlation-based prediction toward causal understanding. The 100x reduction in required latent features for planning suggests object-centric representations are dramatically more efficient for control tasks — a key insight for scaling world models to complex environments.

### What Drives Success in Physical Planning with Joint-Embedding Predictive World Models? [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2512.24497)

**Authors/Presenters**: Basile Terver, Tsung-Yen Yang, Jean Ponce, Adrien Bardes, [Yann LeCun](players.md#yann-lecun)

**Date**: 2025-12 (revised 2026-01)

**Summary**: Systematic ablation study characterizing JEPA-based world models (JEPA-WMs) for physical planning. Investigates multistep rollout, predictor architecture, training context length, proprioception, encoder type, model size, data augmentation, and planning optimizer to identify what actually drives planning success.

**Key Findings**:

- Combined findings produce a model outperforming two established baselines — DINO-WM and V-JEPA-2-AC — in both navigation and manipulation tasks
- Identifies critical design choices: AdaLN-zero predictor architecture, appropriate training context length, and planning optimizer selection
- Provides pretrained checkpoints, code, and data for reproducibility via [jepa-wms](https://github.com/facebookresearch/jepa-wms)

**Relevance to World Models**: Essential reference for practitioners building JEPA-based world models — the first systematic study of which design decisions matter and why. Bridges the gap between JEPA theory and practical world model engineering.

### ACT-JEPA: Novel Joint-Embedding Predictive Architecture for Efficient Policy Representation Learning [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2501.14622)

**Authors/Presenters**: Aleksandar Vujinovic, Aleksandar Kovacevic

**Date**: 2025-01 (revised 2026-03)

**Summary**: Unifies imitation learning (IL) and self-supervised learning (SSL) by training end-to-end to jointly predict action sequences and latent observation sequences via JEPA. Filters irrelevant details through latent prediction, learning a robust world model that transfers to action prediction.

**Key Findings**:

- Up to 40% improvement in world model understanding compared to strongest baseline
- Up to 10% higher task success rate across all tested environments
- Demonstrates that predicting latent observations generalizes effectively to action prediction, validating JEPA as a policy backbone

**Relevance to World Models**: Shows JEPA can unify representation learning and policy learning in a single architecture. Rather than training a world model and policy separately, ACT-JEPA learns both jointly — potentially more sample-efficient for robotics applications.

### Intrinsic-Energy Joint Embedding Predictive Architectures Induce Quasimetric Spaces [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2602.12245)

**Authors/Presenters**: Anthony Kobanda, Waris Radji

**Date**: 2026-02

**Summary**: Bridges JEPA and Quasimetric Reinforcement Learning (QRL) by proving that intrinsic (least-action) energies in JEPAs constitute quasimetrics under specified conditions. Shows that optimal cost-to-go functions in goal-reaching control naturally adopt this intrinsic energy form.

**Key Findings**:

- Proves intrinsic energies satisfying closure and additivity form valid quasimetrics, linking JEPA energy functions to QRL's value class
- Demonstrates symmetric finite energies are structurally incompatible with one-way reachability, motivating asymmetric formulations
- Primarily theoretical; provides mathematical framework connecting JEPA to control-theoretic foundations

**Relevance to World Models**: Provides theoretical grounding for using JEPA-style energy functions in planning and goal-reaching tasks. Connects world model representations to quasimetric structure, potentially enabling more principled planning algorithms.

### A Lightweight Library for Energy-Based Joint-Embedding Predictive Architectures (EB-JEPA) [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2602.03604)

**Authors/Presenters**: Basile Terver, Randall Balestriero, Megi Dervishi, David Fan, Quentin Garrido, Tushar Nagarajan, Koustuv Sinha, Wancong Zhang, Mike Rabbat, [Yann LeCun](players.md#yann-lecun), Amir Bar

**Date**: 2026-02

**Summary**: Introduces EB-JEPA, an open-source library for learning representations and world models using JEPAs. Predicts in representation space rather than pixel space, enabling single-GPU training within hours. Provides modular implementations from image representation to action-conditioned world models.

**Key Findings**:

- Achieves 91% probing accuracy on CIFAR-10 and 97% planning success rate on Two Rooms navigation task
- Demonstrates critical importance of regularization components (VICReg-style) in preventing representation collapse through ablation studies
- Modular design shows progressive path from image JEPA → video JEPA → action-conditioned world model with multi-step prediction

**Relevance to World Models**: Directly addresses world modeling with JEPAs, providing accessible implementations and ablations. The action-conditioned video JEPA example demonstrates world modeling where the model predicts future states from observations and actions, enabling planning toward goal embeddings.

### VJEPA: Variational Joint Embedding Predictive Architectures as Probabilistic World Models [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2601.14354)

**Authors/Presenters**: Yongchao Huang

**Date**: 2026-01

**Summary**: Introduces Variational JEPA, a probabilistic generalization that learns predictive distributions over future latent states via variational objectives rather than deterministic regression. Unifies representation learning with Predictive State Representations and Bayesian filtering without autoregressive observation likelihoods. Extension called Bayesian JEPA enables zero-shot task transfer through modular expert architecture.

**Key Findings**:

- Develops probabilistic variant with variational objectives for predicting latent state distributions instead of point estimates
- Proves VJEPA representations serve as sufficient information states for optimal control without pixel reconstruction
- Introduces BJEPA extension factorizing beliefs into learned dynamics and modular priors for zero-shot transfer via Product of Experts
- Demonstrates robustness to high-variance distractors that cause collapse in generative approaches
- Enables principled uncertainty estimation through sampling while remaining likelihood-free regarding observations

**Relevance to World Models**: Foundational framework for scalable, uncertainty-aware world models in stochastic control that bridges representation learning with Bayesian filtering without expensive observation reconstruction. Addresses key limitation of deterministic JEPA by incorporating probabilistic semantics essential for planning under uncertainty.

### WirelessJEPA: A Multi-Antenna Foundation Model using Spatio-temporal Wireless Latent Predictions [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2601.20190)

**Authors/Presenters**: Viet Chu, Omar Mashaal, Hatem Abou-Zeid

**Date**: 2026-01

**Summary**: Applies JEPA to wireless signal processing by predicting latent representations of masked multi-antenna IQ signal regions. Introduces 2D antenna-time representation enabling convolutional processing with block masking, eliminating need for hand-crafted contrastive augmentations. Demonstrates robust generalization across diverse downstream tasks.

**Key Findings**:

- Novel 2D antenna-time representation reshapes multi-antenna IQ streams into structured grids for convolutional processing with efficient sparse computation
- Introduces spatio-temporal mask geometries encoding inductive biases across antenna arrays and temporal dimensions
- Evaluated across six diverse tasks: angle-of-arrival estimation, modulation classification, RF fingerprinting, protocol classification, GNSS jamming, and interference classification
- Establishes JEPA-based learning as promising direction for building generalizable wireless foundation models
- Demonstrates direct learning from real-world multi-antenna data as viable for general-purpose wireless representation learning

**Relevance to World Models**: Domain-specific application demonstrating world model principles—using unsupervised predictive learning to build generalizable representations that transfer across tasks without explicit task engineering. Shows JEPA's applicability beyond vision/language to signal processing domains.

### Le MuMo JEPA: Multi-Modal Self-Supervised Representation Learning with Learnable Fusion Tokens [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2603.24327)

**Authors/Presenters**: Ciem Cornelissen, Sam Leroux, Pieter Simoens

**Date**: 2026-03

**Summary**: Extends LeJEPA to multi-modal settings (RGB + LiDAR depth, RGB + thermal) by introducing learnable fusion tokens that act as a latent bottleneck between modality-specific patch stems inside a shared transformer. Uses SIGReg as a modality-agnostic shared target distribution, enabling cross-modal alignment without artificial token-wise pairing constraints.

**Key Findings**:

- Learnable fusion tokens aggregate cross-modal information through attention, then modality-specific tokens are pruned — forcing all information through the shared fusion-token grid
- Strongest performance-efficiency trade-off among from-scratch multimodal baselines on Waymo, nuScenes, and FLIR benchmarks
- Substantially lower compute, memory, and training time than alternatives while maintaining best overall accuracy

**Relevance to World Models**: Demonstrates that JEPA-style prediction in latent space extends naturally to multi-modal sensor fusion — a requirement for real-world world models that must integrate heterogeneous inputs (camera, LiDAR, thermal) for autonomous driving and robotics.

### EchoJEPA: A Latent Predictive Foundation Model for Echocardiography [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2602.02603)

**Authors/Presenters**: Alif Munim, Adibvafa Fallahpour, Teodora Szasz, Ahmadreza Attarpour, River Jiang, Brana Sooriyakanthan, Maala Sooriyakanthan, Heather Whitney, Jeremy Slivnick, Barry Rubin, Wendy Tsang, Bo Wang

**Date**: 2026-02

**Summary**: First foundation-scale JEPA for medical imaging, trained on 18 million echocardiograms across 300K patients. Adapts V-JEPA 2 with domain-specific modifications (higher temporal sampling, conservative cropping, narrower aspect ratios) to learn anatomical representations that filter out ultrasound speckle noise.

**Key Findings**:

- ~20% improvement on LVEF estimation and 17% on RVSP estimation over leading baselines; 79% view classification accuracy with only 1% labeled data vs. 42% for best baseline at 100%
- Under simulated acoustic perturbations, performance drops just 2% vs. 17% for competitors; zero-shot pediatric performance exceeds fully fine-tuned baselines
- Challenges assumption that methods from natural video transfer directly to medical imaging — in ultrasound, texture is interference noise, not semantic signal

**Relevance to World Models**: Demonstrates JEPA's applicability to medical imaging where the distinction between signal and noise is fundamentally different from natural video. The success of latent prediction over reconstruction validates the JEPA principle that predicting in representation space naturally filters task-irrelevant variation.

### JEPA-MSAC: A Joint-Embedding Predictive Architecture for Multimodal Sensing-Assisted Communications [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2603.29796)

**Authors/Presenters**: Can Zheng, Jiguang He, Guofa Cai, Nannan Li, Mehdi Bennis, Henk Wymeersch, Merouane Debbah

**Date**: 2026-03

**Summary**: Self-supervised multimodal predictive framework for wireless environments. Maps sensing and communication measurements into a unified token space, pretrains via temporal block-masked JEPA to learn predictive latent representations capturing environment dynamics. Frozen backbone reused with lightweight task heads for localization, beam prediction, and RSSI estimation.

**Key Findings**:

- Frozen pretrained backbone + lightweight task heads outperforms dedicated single-task baselines like M2BeamLLM across all three downstream tasks
- One-shot future prediction faster than autoregressive decoding baselines; avoids heavy decoders required by reconstruction-based SSL
- Validated on DeepSense 6G real-world multimodal dataset (urban 60 GHz mmWave scenario)

**Relevance to World Models**: Another domain-specific JEPA application demonstrating the architecture's generality. Learns a predictive world model of wireless environments — capturing how channels, positions, and signals evolve — then reuses representations across multiple downstream tasks without retraining.

### A Wireless World Model for AI-Native 6G Networks [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2603.25216)

**Authors/Presenters**: Ziqi Chen, Yi Ren, Yixuan Huang, Qi Sun, Nan Li, Yuhong Huang, Chih-Lin I, Yifan Li, Liang Xia

**Date**: 2026-03

**Summary**: Multi-modal foundation framework for predicting spatiotemporal wireless channel evolution using a joint-embedding predictive architecture with multi-modal mixture-of-experts Transformer. Fuses channel state information, 3D point clouds, and user trajectories into a unified representation, pre-trained on ray-traced synthetic data to bridge the sim-to-real gap.

**Key Findings**:

- JEPA + MoE Transformer architecture enables "one-model-for-all" paradigm covering channel prediction, compression/feedback, beam management, and user localization
- Pre-training on ray-traced synthetic data provides physics-aware understanding of electromagnetic wave propagation, enabling generalization to unseen environments
- Consistently outperforms SOTA uni-modal foundation models and task-specific models across five downstream tasks in both seen and unseen scenarios, validated on real-world measurements

**Relevance to World Models**: Builds on WirelessJEPA and JEPA-MSAC by adding multi-modal fusion (CSI + 3D point clouds + trajectories) through MoE, creating a more complete wireless world model. The physics-aware pre-training on synthetic ray-traced data parallels Cosmos's sim-to-real approach but in the wireless domain.

### Tutorial on Joint Embedding Predictive Architectures (JEPA): Foundations, Applications, and Future Directions [<img src="templates/icons/website.svg" alt="website" height="16">](https://www.techrxiv.org/users/866579/articles/1365143)

**Authors/Presenters**: Mehdi Monemi, Maryam Chinipardaz, Mehdi Rasti, Mehdi Bennis

**Date**: 2025-12

**Summary**: Comprehensive tutorial covering JEPA's theoretical foundations, architectural design principles, and diverse application domains. Situates JEPA within the broader taxonomy of representation learning and formulates its core components: context-target generation, encoding, latent-space prediction, regularization, and energy minimization. Presents a framework for agentic AI where a multi-level JEPA predictor functions as a latent-space world model.

**Key Findings**:

- Systematic formulation of JEPA components with cross-referencing to existing implementations across image, audio, video, point-cloud, and multimodal modalities
- Framework for realizing [Yann LeCun](players.md#yann-lecun)'s agentic AI vision: multi-level JEPA predictor as latent-space world model integrated with actor training for mode-2 planning and control
- Surveys emerging JEPA applications in 6G networks, identifying this as a nascent but promising research direction

**Relevance to World Models**: Serves as the definitive reference for JEPA architecture — bridging LeCun's theoretical vision with practical implementations. The agentic AI framework section directly maps JEPA to world model-based planning, making explicit the connection between representation learning and autonomous decision-making.

### 14 JEPA Milestones as a Map of AI Progress [<img src="templates/icons/website.svg" alt="website" height="16">](https://lifeboat.com/blog/2026/03/14-jepa-milestones-as-a-map-of-ai-progress)

**Authors/Presenters**: Lifeboat News / TuringPost

**Date**: 2026-03

**Summary**: Chronological overview of 14 JEPA milestones tracing the architecture's evolution from foundational concepts through domain-specific applications. Covers JEPA/H-JEPA, I-JEPA, MC-JEPA, V-JEPA, Audio-JEPA, Point-JEPA, 3D-JEPA, ACT-JEPA, V-JEPA 2, LeJEPA, Causal-JEPA, V-JEPA 2.1, LeWorldModel, and ThinkJEPA.

**Key Findings**:

- Maps JEPA expansion from core vision to multi-modal applications: audio, 3D point clouds, video understanding, and robotic manipulation
- Highlights LeWorldModel as notably compact (15M params) and ThinkJEPA as combining dense physical prediction with VLM reasoning for long-term strategic planning
- Underlying principle across all variants: predicting in latent space rather than pixel space enables efficient learning across diverse modalities

**Relevance to World Models**: Provides a concise lineage of JEPA development, useful for understanding how the architecture has evolved toward world modeling. ThinkJEPA's integration of VLM reasoning with JEPA dynamics prediction represents the latest convergence of language understanding and physical world modeling.

### BiJEPA: Bi-directional Joint Embedding Predictive Architecture for Symmetric Representation Learning [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2603.00049)

**Authors/Presenters**: Yongchao Huang

**Date**: 2026-02

**Summary**: Extends JEPA with cycle-consistent bidirectional prediction between data segments. Introduces norm regularization on representation vectors to prevent "Representation Explosion" — a collapse mode specific to symmetric prediction architectures. Validated across synthetic signals, chaotic systems, and image data.

**Key Findings**:

- Bidirectional prediction captures informative signal in the inverse relationship, enabling more complete representation learning
- Identifies "Representation Explosion" as a primary failure mode of bi-directional SSL — norm regularization prevents this while maintaining training stability
- Successfully learns representations across diverse modalities without collapse; captures structural patterns in chaotic dynamical systems

**Relevance to World Models**: Addresses a gap in standard JEPA: unidirectional prediction may miss structure in the reverse mapping. For world models, bidirectional consistency could improve temporal reasoning — knowing that state B follows A should imply A precedes B. The Representation Explosion failure mode is a new collapse category beyond the collapse modes addressed by VICReg.

### US-JEPA: A Joint Embedding Predictive Architecture for Medical Ultrasound [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2602.19322)

**Authors/Presenters**: Ashwath Radhachandran, Vedrana Ivezić, Shreeram Athreya, Ronit Anilkumar, Corey W. Arnold, William Speier

**Date**: 2026-02

**Summary**: Applies JEPA to ultrasound imaging, addressing the modality's high noise and speckle patterns that undermine standard self-supervised approaches. Uses Static-teacher Asymmetric Latent Training (SALT) objective with a frozen domain-specific teacher for stable latent targets, avoiding the computational expense of dynamically-updated teachers.

**Key Findings**:

- SALT objective decouples student-teacher optimization while expanding semantic understanding; avoids hyperparameter brittleness of standard JEPA
- First comprehensive comparison of ultrasound foundation models using UltraBench (multi-organ, multi-pathology dataset)
- Achieves competitive or superior performance vs. domain-specific and universal vision models under linear probing for classification

**Relevance to World Models**: Extends JEPA to medical imaging domain where EchoJEPA already showed promise. The SALT objective addresses a practical barrier: standard JEPA's EMA-updated teachers are computationally expensive and sensitive to hyperparameters. If SALT transfers to other domains, it could simplify JEPA deployment for world models in healthcare applications.

### Polymer-JEPA: Joint Embedding Predictive Architecture for Polymer Molecular Graphs [<img src="templates/icons/website.svg" alt="website" height="16">](https://pubs.rsc.org/en/content/articlelanding/2026/dd/d5dd00308c)

**Authors/Presenters**: Francesco Piccoli, Gabriel Vogel, Jana M. Weber

**Date**: 2026-01

**Summary**: Applies JEPA self-supervised pretraining to polymer molecular graphs. Pretrained on conjugated copolymer photocatalysts, then fine-tuned on downstream tasks including electron affinity prediction and phase behavior classification in diblock copolymers.

**Key Findings**:

- JEPA-based pretraining enhances downstream performance, particularly when labeled data is scarce
- Cross-domain fine-tuning shows promise — method extracts generalizable knowledge across different polymer classes
- Reduces dependence on extensive labeled datasets by leveraging unlabeled polymer structures

**Relevance to World Models**: Demonstrates JEPA's applicability beyond vision/video to molecular graph domains. For scientific discovery use cases (materials science, drug discovery), this suggests JEPA-style self-supervised learning can build useful representations from unlabeled molecular data — complementing domain-specific world models like those from Periodic Labs and Medra.

### Graph-JEPA: Graph-level Representation Learning with Joint-Embedding Predictive Architectures [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2309.16014)

**Authors/Presenters**: Geri Skenderi, Hang Li, Jiliang Tang, Marco Cristani

**Date**: 2023-09 (revised 2025-01, TMLR)

**Summary**: Extends JEPA to graph-level representation learning through masked subgraph prediction. Introduces a hyperbolic prediction objective that maps encoded subgraphs to coordinates on the unit hyperbola, capturing implicit hierarchical structure in graph concepts without contrastive samples or reconstruction.

**Key Findings**:

- Predicts latent representations of masked subgraphs from context subgraphs, avoiding contrastive negative/positive samples
- Hyperbolic coordinate prediction endows representations with implicit hierarchy — captures tree-like and scale-free structures common in real-world graphs
- Strong downstream performance on graph classification, regression, and non-isomorphic graph discrimination

**Relevance to World Models**: Extends JEPA beyond grid-structured data (images, video, spectrograms) to arbitrary graph topologies. Relevant for world models operating on relational data — molecular dynamics, knowledge graphs, social networks, or scene graphs in robotics where entities and relationships matter more than pixel arrangements.

### Brain-JEPA: Brain Dynamics Foundation Model with Gradient Positioning and Spatiotemporal Masking [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2409.19407)

**Authors/Presenters**: Zijian Dong, Ruilin Li, Yilei Wu, Thuan Tinh Nguyen, Joanna Su Xian Chong, Fang Ji, Nathanael Ren Jie Tong, Christopher Li Hsian Chen, Juan Helen Zhou

**Date**: 2024-09 (NeurIPS 2024 Spotlight)

**Summary**: Foundation model for fMRI brain dynamics using JEPA with two domain-specific innovations: Brain Gradient Positioning (functional coordinate system for ROI encoding) and Spatiotemporal Masking (handles heterogeneous fMRI time-series patches). Achieves SOTA on demographic prediction, disease diagnosis/prognosis, and trait assessment.

**Key Findings**:

- Brain Gradient Positioning establishes a functional coordinate system for brain parcellation, improving positional encoding of Regions of Interest
- Spatiotemporal masking samples targets from three regions: Cross-ROI, Cross-Time, and Double-Cross — tailored to fMRI's unique characteristics
- Superior generalizability across ethnic populations; strong off-the-shelf linear probing performance

**Relevance to World Models**: Demonstrates JEPA's adaptability to complex spatiotemporal biomedical data where standard positional encodings fail. The functional coordinate system approach could transfer to other domains with non-Euclidean structure — network traffic, multi-sensor systems, or distributed robotics where "position" is functional rather than spatial.

### EEG-VJEPA: Adapting Video JEPA for Brain Signal Analysis [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2507.03633)

**Authors/Presenters**: Amirabbas Hojjati, Lu Li, Ibrahim Hameed, Anis Yazidi, Pedro G. Lind, Rabindra Khadka

**Date**: 2025-07 (revised 2026-03)

**Summary**: First application of V-JEPA to EEG classification by treating brain signals as video-like sequences. Combines predictive accuracy with interpretability — learns physiologically relevant spatial and temporal patterns that support human-AI collaboration in clinical diagnostics.

**Key Findings**:

- Treats EEG as video: channels as spatial dimension, time as temporal — enables direct application of V-JEPA's spatiotemporal masking
- Outperforms SOTA on Temple University Hospital (TUH) Abnormal EEG dataset
- Produces interpretable embeddings capturing physiologically meaningful patterns, not just classification accuracy

**Relevance to World Models**: Validates the "treat X as video" strategy for applying V-JEPA to sequential multi-channel data. The interpretability finding is significant: JEPA's latent predictions appear to capture domain-relevant structure (brain dynamics) rather than arbitrary features — a property essential for clinical world models where decisions must be explainable.

### A-JEPA: Joint-Embedding Predictive Architecture Can Listen [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2311.15830)

**Authors/Presenters**: Zhengcong Fei, Mingyuan Fan, Junshi Huang

**Date**: 2023-11 (revised 2024-01)

**Summary**: Adapts I-JEPA to audio spectrograms with a curriculum masking strategy progressing from easy to hard predictions. Introduces time-frequency aware masking that accounts for temporal and spectral correlations specific to audio, plus regularized masking during fine-tuning for improved downstream adaptation.

**Key Findings**:

- Curriculum masking: starts with easier predictions, progressively increases difficulty — mirrors human learning patterns
- Time-frequency aware masking exploits audio-specific structure (harmonic relationships, temporal continuity) vs. random block masking
- SOTA on multiple audio and speech classification tasks, outperforming externally supervised pre-training approaches

**Relevance to World Models**: First successful audio JEPA, demonstrating the architecture generalizes beyond vision. The curriculum strategy addresses a practical training challenge: audio has stronger local correlations than images, making random masking too easy early in training. Relevant for world models incorporating audio — robotics, autonomous vehicles, smart environments.

### Audio-JEPA: Joint-Embedding Predictive Architecture for Audio Representation Learning [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2507.02915)

**Authors/Presenters**: Ludovic Tuncay, Etienne Labbé, Emmanouil Benetos, Thomas Pellegrini

**Date**: 2025-06 (ICME 2025)

**Summary**: Straightforward JEPA adaptation for audio using Vision Transformer on mel-spectrograms with random patch masking. Matches wav2vec 2.0 and data2vec performance on X-ARES benchmark while using less than 1/5 of their training data — demonstrates JEPA's data efficiency for audio.

**Key Findings**:

- 96.7M trainable parameters (85.4M at inference — predictor discarded); trained on unlabeled AudioSet clips (10s, 32kHz)
- Competitive with wav2vec 2.0/data2vec across speech, music, and environmental sounds using <20% training data
- No hyperparameter tuning required — robust default configuration

**Relevance to World Models**: Confirms JEPA's data efficiency advantage extends to audio domain. For embodied AI requiring audio understanding (voice commands, environmental sounds, machinery diagnostics), Audio-JEPA offers a practical foundation model that can be trained on modest data — important for specialized domains where labeled audio is scarce.

### Sat-JEPA-Diff: Bridging Self-Supervised Learning and Generative Diffusion for Remote Sensing [<img src="templates/icons/website.svg" alt="website" height="16">](https://openreview.net/forum?id=WBHfQLbgZR)

**Authors/Presenters**: Kursat Komurcu, Linas Petkevicius

**Date**: 2026-03 (ML4RS @ ICLR 2026)

**Summary**: Hybrid architecture combining I-JEPA embeddings with Stable Diffusion for satellite imagery generation. I-JEPA predicts stable semantic representations that guide a frozen diffusion model via cross-attention, eliminating the "regression to the mean" blur of deterministic methods while avoiding hallucinations of pure generative approaches.

**Key Findings**:

- I-JEPA embeddings serve as structural anchors ensuring synthesized textures maintain geographic accuracy
- GSSIM: 0.8984, FID: 0.1475 — leading perceptual scores on global Sentinel-2 data
- Resolves sharp boundaries that deterministic predictors (PredRNN, SimVP) blur

**Relevance to World Models**: Demonstrates a practical JEPA + diffusion hybrid where JEPA provides structure and diffusion provides texture. This division of labor — latent prediction for semantics, generation for appearance — may be a general pattern for world models that need both accurate dynamics and realistic rendering. Directly applicable to earth observation, environmental monitoring, and climate modeling.

---

## Energy-Based Models

*Papers, talks, and videos on EBMs for prediction and generation*

### Autoregressive Language Models are Secretly Energy-Based Models: Insights into the Lookahead Capabilities of Next-Token Prediction [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2512.15605)

**Authors/Presenters**: Mathieu Blondel, Michael E. Sander, Germain Vivier-Ardisson, Tianlin Liu, Vincent Roulet

**Date**: 2025-12 (revised 2026-01)

**Summary**: Establishes an explicit bijection between autoregressive models (ARMs) and energy-based models (EBMs) in function space. Shows this correspondence is a special case of soft Bellman equations in maximum entropy RL, providing theoretical explanation for how next-token prediction enables lookahead planning.

**Key Findings**:

- Derives equivalence between supervised learning approaches for ARMs and EBMs; unified view connects two historically distinct paradigms
- Analyzes distillation of energy-based models into autoregressive models with theoretical error bounds
- Explains lookahead planning capabilities of ARMs despite being trained on next-token prediction, via the EBM connection

**Relevance to World Models**: Bridges autoregressive and energy-based frameworks theoretically, suggesting that next-token predictors implicitly learn energy landscapes. Relevant to understanding how world models might plan ahead using energy-based formulations rather than explicit rollouts.

### Kona 1.0: Energy-Based Reasoning Model [<img src="templates/icons/website.svg" alt="website" height="16">](https://logicalintelligence.com/kona-ebms-energy-based-models)

**Authors/Presenters**: Eve Bodnia, [Logical Intelligence](players.md#logical-intelligence)

**Date**: 2026-01

**Summary**: First commercial Energy-Based Reasoning Model (EBRM) designed for constraint satisfaction in critical systems. Unlike autoregressive LLMs that predict likely next tokens, Kona maps candidate solutions onto an energy landscape and navigates to minimum-energy (valid) states. Non-autoregressive at the trace level — generates complete reasoning traces simultaneously using continuous vector tokens rather than discrete tokens.

**Key Findings**:

- 96.2% Sudoku solve rate in 313ms average vs. 2% for leading LLMs (GPT-5.2, Claude Opus, Gemini, DeepSeek) taking up to 90 seconds — runs on single NVIDIA H100
- Non-autoregressive architecture enables bidirectional optimization — can revise any section of a reasoning trace without regenerating long prefixes
- Continuous latent space reasoning with dense vector tokens enables gradient-based refinement impossible with discrete token representations
- Aleph (orchestration layer) achieved near-perfect score on PutnamBench formal mathematics benchmark

**Relevance to World Models**: First commercial implementation of EBM principles for reasoning, with [Yann LeCun](players.md#yann-lecun) as Founding Chair of Technical Research Board. Shares key properties with JEPA: continuous latent space, non-autoregressive generation, energy minimization. Where JEPA learns representations via prediction, Kona applies EBM principles to constraint satisfaction — complementary applications of the same paradigm. Validates LeCun's thesis that energy-based approaches offer advantages over autoregressive models for tasks requiring global coherence.

---

## Dragon Hatchling (BDH)

*Research on Baby Dragon Hatchling models*

### The Dragon Hatchling: The Missing Link between the Transformer and Models of the Brain [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2509.26507)

**Authors/Presenters**: [Adrian Kosowski](players.md#adrian-kosowski), Przemysław Uznański, Jan Chorowski, Zuzanna Stamirowska, Michał Bartoszkiewicz

**Date**: 2025-09

**Summary**: Proposes Baby Dragon Hatchling (BDH), a biologically-inspired LLM architecture based on a scale-free network of locally-interacting neuron particles. Bridges transformers and brain models by using synaptic plasticity with Hebbian learning via spiking neurons, while matching GPT-2 performance at equivalent parameter counts (10M–1B).

**Key Findings**:

- Achieves transformer-like scaling laws rivaling GPT-2 on language and translation tasks at identical parameter counts and training data
- Working memory relies entirely on synaptic plasticity with Hebbian learning; exhibits heavy-tailed degree distributions and high modularity matching biological networks
- Sparse, positive activation vectors demonstrate monosemanticity on language tasks, providing built-in interpretability at the architecture level rather than as a post-hoc analysis
- Individual synapses strengthen for specific concepts during processing, enabling interpretability beyond neuron-level analysis

**Relevance to World Models**: Introduces a fundamentally different architecture for learning world representations, grounded in neuroscience rather than the attention mechanism. The built-in interpretability and biologically plausible learning rules could offer advantages for world models that need to build causal, compositional representations of environments.

---

## World Models & Model-Based RL

*Papers on world models, DreamerV3, latent models, etc.*

### DreamZero: World Action Models are Zero-shot Policies [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2602.15922)

**Authors/Presenters**: Seonghyeon Ye, Yunhao Ge, Jim Fan, Yuke Zhu ([NVIDIA](players.md#nvidia) GEAR Lab)

**Date**: 2026-02

**Summary**: Introduces World Action Models (WAMs), a 14B-parameter architecture that jointly predicts video frames and robot actions through a shared denoising objective built on a pretrained video diffusion backbone (Wan2.1-I2V). Unlike VLAs trained on static image-text pairs, WAMs learn physical dynamics by predicting future world states and using video as a dense representation of how the world evolves.

**Key Findings**:

- 62.2% average task progress on seen tasks vs. 27.4% for pretrained VLAs; 39.5% vs. 16.3% on unseen tasks — 2x better generalization
- Cross-embodiment transfer: 12 minutes of human video yields >42% improvement on unseen tasks; adapts to new robot (YAM) with 30 minutes of play data
- Diverse training data outperforms repetitive demonstrations — key insight reverses conventional robotics wisdom
- DreamZero-Flash achieves single-step inference at ~150ms via decoupled noise schedules; 38x speedup through system/implementation/model optimizations
- GR00T N2 (planned end 2026) will be built on DreamZero architecture

**Relevance to World Models**: Establishes World Action Models as a new architecture family alongside VLAs and JEPA-based world models. WAMs treat video generation as an implicit visual planner guiding action production — the world model is embedded in the video diffusion backbone rather than being a separate component. Jim Fan characterizes this as the "GPT-2 moment" for robotics.

### π*0.6 and RECAP: A VLA that Learns from Experience [<img src="templates/icons/website.svg" alt="website" height="16">](https://www.pi.website/blog/pistar06)

**Authors/Presenters**: [Physical Intelligence](players.md#physical-intelligence-π)

**Date**: 2025-11

**Summary**: Introduces RECAP (RL with Experience & Corrections via Advantage-conditioned Policies), a method enabling VLAs to improve through reinforcement learning without policy gradients. Addresses the fundamental challenge that imitation-only training leads to compounding errors in physical environments. π*0.6 trained with RECAP achieves >90% success rates on complex manipulation tasks.

**Key Findings**:

- Converts RL to conditional supervised learning — avoids computing log-probabilities required by standard RL (PPO, SAC), which flow matching models don't provide
- Three-stage learning: demonstrations → expert corrections during errors → autonomous practice with value function feedback
- Value functions solve credit assignment — identifies whether failures originated from early missteps or later actions
- More than doubles throughput on espresso making, box assembly; reduces failure rate by 2x+ on laundry folding
- Enables continuous autonomous operation for extended periods with >90% success rates

**Relevance to World Models**: Demonstrates RL post-training for embodied AI that parallels RLVR-World and WorldCompass. RECAP solves the credit assignment problem critical for long-horizon tasks where world model predictions must identify which past actions caused future failures. Limitation: cannot discover globally optimal policies — only improves within the behavioral distribution of training data.

### GEN-1: Scaling Embodied Foundation Models to Mastery [<img src="templates/icons/website.svg" alt="website" height="16">](https://generalistai.com/blog/apr-02-2026-GEN-1)

**Authors/Presenters**: [Generalist AI](players.md#generalist-ai)

**Date**: 2026-04

**Summary**: Native embodied foundation model trained from scratch on 500K+ hours of real-world physical interaction data captured via low-cost wearable "data hands" (UMIs) worn by humans — no robot data or internet images in base pretraining. Achieves 99% success rates on production tasks vs. 64% for GEN-0, completing tasks 3x faster with 10x less task-specific data.

**Key Findings**:

- Wearable-first data collection bypasses robotics data bottleneck — captures human reflexes and micro-corrections more efficiently than teleoperation
- 99% success demonstrated across vacuum servicing (200+ reps), box folding (200+ reps), phone packing (100+ reps), block packing (1800+ reps)
- Requires only ~1 hour of robot-specific data for new task adaptation
- Full system redesign vs. VLA approach — "large multimodal model that emits actions in real-time" with inference harnessing components

**Relevance to World Models**: Represents a third paradigm beyond VLAs (internet pretraining + action decoder) and WAMs (video diffusion backbone). Generalist trains on physical interaction data from wearables, suggesting that world dynamics can be learned directly from human movement without intermediate video or simulation. If validated at scale, could offer a more data-efficient path to physical AI than video-based world models.

### VLA-MBPO: Towards Practical World Model-based Reinforcement Learning for Vision-Language-Action Models [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2603.20607)

**Authors/Presenters**: Zhilong Zhang, Haoxiang Ren, Yihao Sun, Yifei Sheng, Haonan Wang, Haoxin Lin, Zhichao Wu, Pierre-Luc Bacon, Yang Yu

**Date**: 2026-03

**Summary**: Practical framework for finetuning Vision-Language-Action (VLA) models using world models instead of costly real-world interaction. Addresses three key challenges in VLA+world model RL: pixel-level world modeling, multi-view consistency, and compounding errors under sparse rewards.

**Key Findings**:

- Adapts pretrained unified multimodal models as world model backbone for sample-efficient pixel-space prediction without expensive video rollouts
- Interleaved view decoding enforces cross-view consistency while preserving view-specific details for precise robotic control
- Chunk-level branched rollout limits error accumulation; value model progressively aligns with ground-truth returns through cross-chunk temporal dependencies

**Relevance to World Models**: Bridges VLA models (strong generalization from language grounding) with world model-based RL (sample-efficient learning). Demonstrates practical integration path where world models serve as safe, cheap training environments for large pretrained robotic policies.

### R2-Dreamer: Redundancy-Reduced World Models without Decoders or Augmentation [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2603.18202)

**Authors/Presenters**: Naoki Morihira, Amal Nahar, Kartik Bharadwaj, Yasuhiro Kato, Akinobu Hayashi, Tatsuya Harada

**Date**: 2026-03 (ICLR 2026)

**Summary**: Decoder-free MBRL framework using Barlow Twins-inspired redundancy reduction as internal regularizer to prevent representation collapse without data augmentation. Removes decoder overhead while maintaining competitive performance, addressing the limitation that data augmentation can distort task-critical information.

**Key Findings**:

- Competitive with DreamerV3 and TD-MPC2 on DeepMind Control Suite and Meta-World while training 1.59x faster
- Substantial gains on DMC-Subtle benchmark (tiny task-relevant regions) where augmentation-based methods struggle
- Releases unified PyTorch codebase with DreamerV3 reimplementation and baselines, plus DMC-Subtle benchmark

**Relevance to World Models**: Advances decoder-free world models by replacing heuristic data augmentation with principled self-supervised regularization. The Barlow Twins connection parallels VICReg in JEPA — both use redundancy reduction to prevent collapse, suggesting convergent design principles across world model architectures.

### NE-Dreamer: Next Embedding Prediction Makes World Models Stronger [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2603.02765)

**Authors/Presenters**: George Bredis, Nikita Balagansky, Daniil Gavrilov, Ruslan Rakhimov

**Date**: 2026-03

**Summary**: Decoder-free MBRL agent using a temporal transformer to predict next-step encoder embeddings from latent state sequences. Directly optimizes temporal predictive alignment in representation space, eliminating reconstruction losses and auxiliary supervision.

**Key Findings**:

- Matches or exceeds DreamerV3 on DeepMind Control Suite; substantial gains on DMLab tasks requiring memory and spatial reasoning
- Ablations attribute performance to predictive sequence modeling (causal transformer + next-step target shift), not reconstruction
- Decoder-free design removes computational burden of pixel-level reconstruction while improving representation quality

**Relevance to World Models**: Directly implements the JEPA principle — predicting in embedding space rather than pixel space — within the Dreamer family of world models. Demonstrates that next-embedding prediction with temporal transformers is a viable alternative to reconstruction-based world models, with particular advantages for tasks requiring memory and reasoning.

### RLVR-World: Training World Models with Reinforcement Learning [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2505.13934)

**Authors/Presenters**: Jialong Wu, Shaofeng Yin, Ningya Feng, Mingsheng Long

**Date**: 2025-05 (NeurIPS 2025)

**Summary**: Unified framework applying reinforcement learning with verifiable rewards (RLVR) to optimize world models directly for transition prediction metrics rather than maximum likelihood. Formulates world modeling as autoregressive prediction of tokenized sequences, then evaluates decoded predictions as verifiable rewards.

**Key Findings**:

- +30.7% accuracy for 1.5B LLM as text-based world simulator, rivaling GPT-4; +15.1% F1 on web navigation world models
- +18.4% relative improvement on WebArena success rates when using RLVR-trained world models for web agents
- Demonstrates RLVR as general post-training paradigm applicable to both language and video world models across text games, web navigation, and robot manipulation

**Relevance to World Models**: Introduces RL-based post-training as a complement to supervised pretraining for world models. Rather than learning to predict next tokens/pixels accurately, RLVR optimizes for task-relevant transition quality — a shift that parallels the JEPA philosophy of learning useful representations over faithful reconstruction.

### WorldCompass: Reinforcement Learning for Long-Horizon World Models [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2602.09022)

**Authors/Presenters**: Zehan Wang, Tengfei Wang, Haiyu Zhang, Xuhui Zuo, Junta Wu, Haoyuan Wang, Wenqiang Sun, Zhenwei Wang, Chenjie Cao, Hengshuang Zhao, Chunchao Guo, Zhou Zhao

**Date**: 2026-02

**Summary**: Introduces an RL post-training framework for long-horizon, interactive video-based world models. Uses clip-level rollout strategy with complementary reward functions to improve both interaction-following accuracy and visual fidelity without reward-hacking.

**Key Findings**:

- Clip-level rollout generates and evaluates multiple samples at single target clips, enabling fine-grained reward signals and improved rollout efficiency
- Dual reward design addresses interaction-following accuracy and visual quality independently, preventing reward-hacking
- Demonstrates significant improvements on WorldPlay (SOTA open-source world model) across interaction accuracy and visual fidelity metrics

**Relevance to World Models**: Directly tackles a core challenge in video-based world models: maintaining consistency and accuracy over long horizons. RL post-training approach is complementary to JEPA-style pretraining and could be applied to JEPA-based world models.

### Reinforcement World Model Learning for LLM-based Agents [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2602.05842)

**Authors/Presenters**: Xiao Yu, Baolin Peng, Ruize Xu, Yelong Shen, Pengcheng He, Suman Nath, Nikhil Singh, Jiangfeng Gao, Zhou Yu

**Date**: 2026-02

**Summary**: Proposes Reinforcement World Model Learning (RWML), a self-supervised method for learning action-conditioned world models in LLM-based agents using sim-to-real gap rewards. Prioritizes semantic equivalence over token-level fidelity, providing robust training signal less susceptible to reward hacking than LLM-as-a-judge approaches.

**Key Findings**:

- Surpasses direct task-success reward RL by 6.9 points on ALFWorld and 5.7 points on τ² Bench while matching expert-data training performance
- Achieves significant gains over base model entirely through self-supervision without task-success rewards
- Grounds learning in pre-trained embedding spaces rather than surface-level token matching, avoiding model collapse from token-level prediction
- Provides more robust training signal than LLM-as-a-judge by using sim-to-real gap rewards
- Demonstrates that world-modeling capabilities enable LLM agents to anticipate action consequences and adapt to environment dynamics

**Relevance to World Models**: Directly advances world models for textual environments by enabling LLMs to learn action-conditioned dynamics models. Shows that world model learning via RL can be more effective than direct task reward optimization, validating model-based approaches for LLM agents.

### Optimistic World Models: Efficient Exploration in Model-Based Deep Reinforcement Learning [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2602.10044)

**Authors/Presenters**: Akshay Mete, Shahid Aamir Sheikh, Tzu-Hsiang Lin, Dileep Kalathil, P. R. Kumar

**Date**: 2026-02

**Summary**: Introduces Optimistic World Models (OWMs), bringing classical reward-biased maximum likelihood estimation from adaptive control into deep RL. Incorporates optimism directly into model learning via optimistic dynamics loss that biases imagined transitions toward higher-reward outcomes, avoiding need for uncertainty estimates or constrained optimization.

**Key Findings**:

- Gradient-based optimistic exploration mechanism requiring neither uncertainty estimates nor constrained optimization, offering computational advantages over UCB-style methods
- Plug-and-play compatibility demonstrated with DreamerV3 and STORM architectures as Optimistic DreamerV3 and Optimistic STORM
- Demonstrates significant improvements in sample efficiency and cumulative returns compared to baseline methods
- Integrates classical adaptive control principles (RBMLE) with contemporary deep RL world model architectures
- Provides principled alternative to uncertainty-based exploration strategies for sparse-reward environments

**Relevance to World Models**: Directly advances world model-based RL by providing principled methodology for efficient exploration. Demonstrates that classical control theory (RBMLE) can be successfully integrated with modern deep world models, offering scalable exploration without expensive uncertainty quantification.

### From Word to World: Can Large Language Models be Implicit Text-based World Models? [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2512.18832)

**Authors/Presenters**: Yixia Li, Hongru Wang, Jiahao Qiu, Zhenfei Yin, Dongdong Zhang, Cheng Qian, Zeping Li, Pony Ma, Guanhua Chen, Heng Ji

**Date**: 2025-12 (revised 2026-03)

**Summary**: Proposes a three-level evaluation framework for LLM-based world models: (i) fidelity and consistency, (ii) scalability and robustness, and (iii) agent utility. Evaluates across five text-based environments, identifying when LLM world models help and when they fail.

**Key Findings**:

- Well-trained LLM world models maintain coherent latent state, scale predictably with data and model size, and improve agent performance
- Identifies three improvement mechanisms: action verification, synthetic trajectory generation, and warm-starting reinforcement learning
- Benefits depend critically on behavioral coverage and environment complexity — delineates clear boundaries on when world modeling supports agent learning

**Relevance to World Models**: Complements visual/latent world models by evaluating whether LLMs can serve as text-domain world models. The finding that benefits scale with data/model size but break down with insufficient behavioral coverage mirrors challenges in visual world models, suggesting shared principles across modalities.

### Cosmos World Foundation Model Platform for Physical AI [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2501.03575)

**Authors/Presenters**: Niket Agarwal, Arslan Ali, Maciej Bala, Yogesh Balaji, Erik Barker, + 72 others ([NVIDIA](players.md#nvidia))

**Date**: 2025-01 (revised 2025-07)

**Summary**: Introduces the Cosmos platform for building customized world models for Physical AI. Defines a World Foundation Model (WFM) as a general-purpose world model fine-tunable into specialized world models for downstream applications. Platform encompasses video curation pipeline, pre-trained WFMs, post-training examples, and video tokenizers. Trained on 20M hours of real-world data (9,000 trillion tokens).

**Key Findings**:

- Frames world models as "digital twins of the physical environment" paired with policy models as "digital twins of the AI system" — two components needed for Physical AI
- Provides end-to-end pipeline: video data curation → tokenization → pre-training → post-training for domain-specific world models
- Open-source platform with permissive licensing (Apache 2 + NVIDIA Open Model License), enabling commercial use
- Positions WFMs as solving the data scaling problem for robotics/AV by generating synthetic training data

**Relevance to World Models**: Defines the industrial paradigm for world foundation models — general-purpose video prediction models fine-tunable into domain-specific world simulators. Contrasts with JEPA's latent-space approach by operating in video/pixel space, making predictions directly renderable and inspectable but potentially less efficient for planning.

### World Simulation with Video Foundation Models for Physical AI (Cosmos-Predict2.5) [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2511.00062)

**Authors/Presenters**: Arslan Ali, Junjie Bai, Maciej Bala, Yogesh Balaji, Aaron Blakeman, + 83 others ([NVIDIA](players.md#nvidia))

**Date**: 2025-10 (revised 2026-02)

**Summary**: Presents Cosmos-Predict2.5, a flow-based architecture unifying Text2World, Image2World, and Video2World generation into a single model. Integrates Cosmos-Reason1 as text encoder for improved physical grounding. Trained on 200M curated video clips with RL-based post-training at 2B and 14B parameter scales.

**Key Findings**:

- Flow-based architecture replaces diffusion-based approach from Predict1, unifying three generation modalities (text/image/video → world) in a single model
- Cosmos-Transfer2.5 control-net framework enables Sim2Real and Real2Real world translation, 3.5x smaller than predecessor with superior fidelity
- RL-based post-training improves video quality and instruction alignment beyond supervised training alone
- Released with post-training recipes for robot policy models and action-conditioned distillation

**Relevance to World Models**: Represents the current SOTA for industrial video-based world models. The shift from diffusion to flow-based architecture and integration of physical reasoning (via Cosmos-Reason1) shows convergence toward world models that understand physics, not just generate plausible video. The Sim2Real transfer capability directly enables robotics applications.

### Cosmos-Reason1: From Physical Common Sense to Embodied Reasoning [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2503.15558)

**Authors/Presenters**: Alisson Azzolini, Junjie Bai, Hannah Brandon, Jiaxin Cao, Prithvijit Chattopadhyay, + 47 others ([NVIDIA](players.md#nvidia))

**Date**: 2025-03 (revised 2025-05)

**Summary**: Introduces multimodal language models for physical AI reasoning — understanding the physical world and generating embodied decisions via chain-of-thought reasoning. Defines a hierarchical ontology for physical common sense (space, time, physics) and a two-dimensional ontology for embodied reasoning that generalizes across different physical embodiments. Models at 7B and 56B scales.

**Key Findings**:

- Hierarchical ontology captures fundamental knowledge about space, time, and physics; two-dimensional embodied reasoning ontology generalizes across different physical embodiments
- Four-stage training: vision pre-training → general SFT → Physical AI SFT → Physical AI RL; last two stages bring significant improvements
- 7B and 56B model variants; serves as text encoder in Cosmos-Predict2.5 for physically-grounded world simulation
- Chain-of-thought reasoning enables models to explain physical dynamics without human annotations

**Relevance to World Models**: Adds explicit physical reasoning to world models — rather than learning physics implicitly from video prediction, Cosmos-Reason encodes physical common sense as structured knowledge. Complementary to JEPA-style approaches: where JEPA learns physics from prediction, Cosmos-Reason provides explicit physical ontologies that can guide and constrain world model predictions.

### Genie 3: A New Frontier for World Models [<img src="templates/icons/website.svg" alt="website" height="16">](https://deepmind.google/blog/genie-3-a-new-frontier-for-world-models/)

**Authors/Presenters**: Jack Parker-Holder, Shlomi Fruchter (Google DeepMind)

**Date**: 2025-08

**Summary**: General-purpose world model generating interactive environments from text prompts at 24 fps in 720p resolution with real-time user interaction. Extends Genie 2 with real-time interactivity, extended temporal consistency (minutes of coherent environment), promptable world events via text, and dynamic frame-by-frame generation.

**Key Findings**:

- First Genie model supporting live user control — processes inputs multiple times per second while maintaining auto-regressive generation
- Visual memory extends approximately one minute into the past; maintains environmental consistency for several minutes of continuous interaction
- Generates physically richer environments than explicit 3D representation methods, though limited to restricted agent action spaces and poor multi-agent interactions
- Currently available as limited research preview for academics and creators

**Relevance to World Models**: Represents DeepMind's approach to interactive world models — operating in pixel space (like Cosmos) rather than latent space (like JEPA). The real-time interaction capability is a significant engineering achievement, though the minutes-scale consistency horizon and restricted action spaces highlight remaining challenges for using video-based world models as true environment simulators.

### Marble: A Multimodal World Model [<img src="templates/icons/website.svg" alt="website" height="16">](https://www.worldlabs.ai/blog/marble-world-model)

**Authors/Presenters**: [World Labs](players.md#world-labs) ([Fei-Fei Li](players.md#fei-fei-li))

**Date**: 2025-11

**Summary**: Generative 3D world model that creates full, persistent 3D environments from diverse inputs — text, images, video, and coarse 3D layouts. Users can iteratively edit, expand, and compose worlds using the Chisel sculpting tool, then export as Gaussian splats, triangle meshes, or video. Integrates with THREE.js via the open-source Spark renderer.

**Key Findings**:

- Decouples structure from style: Chisel provides 3D sculpting control over layout before AI generates visual details, enabling human-AI co-creation
- Supports multimodal world creation: text-to-world, image-to-world, multi-image prompting, and video enhancement with camera control
- Composition mode combines multiple generated worlds into larger traversable spaces; expansion mode adds targeted detail to specific regions
- Outputs in multiple formats (Gaussian splats for fidelity, meshes for downstream tools) enabling integration into existing VFX and game pipelines

**Relevance to World Models**: Represents the 3D-space paradigm — lifting 2D inputs into persistent 3D structures rather than generating video (Cosmos) or predicting in latent space (JEPA). The Chisel tool's human-in-the-loop editing exemplifies "Spatial Intelligence": combining human structural knowledge with AI visual generation. Adopted by studios for VFX pre-visualization and by researchers for robot training data.

### DreamerV3: Mastering Diverse Domains through World Models [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2301.04104)

**Authors/Presenters**: Danijar Hafner, Jurgis Pasukonis, Jimmy Ba, Timothy Lillicrap

**Date**: 2023-01 (JMLR 2024)

**Summary**: General-purpose MBRL agent using Recurrent State-Space Model (RSSM) to learn world models across diverse domains without task-specific tuning. Decomposes hidden state into deterministic (GRU) and stochastic (learned prior/posterior) components, enabling both long-term memory and uncertainty modeling. First algorithm to collect diamonds in Minecraft from scratch without human data.

**Key Findings**:

- Fixed hyperparameters across 150+ tasks spanning continuous/discrete actions, visual/low-dimensional inputs, 2D/3D environments, and dense/sparse rewards
- Symlog predictions normalize value functions across reward scales; free bits and KL balancing stabilize latent dynamics learning
- First successful diamond collection in Minecraft without human data or curriculum — a long-standing MBRL benchmark
- RSSM architecture decomposes state into deterministic (temporal memory) and stochastic (uncertainty) components, enabling multi-step imagination for policy optimization

**Relevance to World Models**: The foundational RSSM-based world model architecture and primary baseline for subsequent work (R2-Dreamer, NE-Dreamer, Optimistic DreamerV3). DreamerV3's decoder-reconstruction approach contrasts with JEPA's decoder-free prediction — R2-Dreamer and NE-Dreamer independently converge toward JEPA principles by eliminating the decoder, suggesting reconstruction is unnecessary for effective world modeling.

### AXIOM: Active Inference for Object-Centric World Models [<img src="templates/icons/website.svg" alt="website" height="16">](https://www.verses.ai/research-blog/axiom-mastering-arcade-games-in-minutes-with-active-inference-and-structure-learning)

**Authors/Presenters**: [Verses AI](players.md#verses-ai)

**Date**: 2025-06

**Summary**: Active Inference architecture that unifies perception, planning, and control through the Free Energy Principle. Creates object-centric world models with hierarchical agent structure — every joint/component is an agent with its own local world model. Learns game dynamics in minutes rather than hours by combining structure learning with active epistemic exploration (seeking observations that reduce uncertainty).

**Key Findings**:

- Reported to outperform [Google DeepMind](players.md#google-deepmind) on Atari "Gameworld 10k" challenge, mastering games in minutes vs. hours for standard RL
- Object-centric representations enable compositional reasoning — understands game objects and their relationships rather than raw pixel patterns
- Hierarchical "Shared Intelligence" allows recovery from unexpected perturbations without retraining, via local prediction error resolution
- Epistemic foraging drives exploration: agents seek states that maximize information gain, not just reward

**Relevance to World Models**: Represents a fundamentally different paradigm from both JEPA (energy-based SSL) and Dreamer (RSSM-based RL). Active Inference treats perception and action as two sides of the same coin — both minimize free energy. The object-centric structure parallels Causal-JEPA but from Bayesian rather than SSL foundations. If validated at real-world scale, could complement JEPA for representation learning and Cosmos for synthetic data as a third paradigm for embodied AI.

---

## Applications & Use Cases

*Papers demonstrating practical applications in robotics, autonomous systems, etc.*

### GAIA-1: A Generative World Model for Autonomous Driving [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2309.17080)

**Authors/Presenters**: Anthony Hu, Lloyd Russell, Hudson Yeo, Zak Murez, George Fedoseev, Alex Mayol Kendall, Jamie Sherrah, [Wayve](players.md#wayve)

**Date**: 2023-09

**Summary**: 9B-parameter generative world model for autonomous driving that treats world modeling as autoregressive sequence prediction. Encodes video, text, and action into discrete tokens, then predicts next tokens to generate realistic driving scenarios. Trained on 4,700 hours of UK urban driving data. Successor GAIA-3 (Dec 2025) scales to 15B parameters, purpose-built for evaluation of end-to-end driving systems.

**Key Findings**:

- Unified tokenization of video, text, and action enables a single autoregressive transformer to learn 3D geometry, scene dynamics, and language-conditioned generation
- Learns disentangled representations: separate control over ego-vehicle actions, scene layout, and weather/lighting without explicit supervision
- Wayve raised $1.05B (Series C, 2024) scaling to $1.5B total; deploying end-to-end driving with Uber and Nissan partnerships
- GAIA-3 (2025-12) extends to 15B parameters, shifting focus from generation quality to serving as a reliable evaluation environment for driving policies

**Relevance to World Models**: Demonstrates that autoregressive next-token prediction — the same paradigm behind LLMs — can learn a world model of driving dynamics from raw sensor data. Contrasts with JEPA's latent-space approach: GAIA operates in discrete token space, making it directly inspectable but potentially less efficient for planning. The GAIA-1 to GAIA-3 progression mirrors the broader trend from world model as generator to world model as simulator/evaluator.

### NVIDIA Isaac GR00T N1: Open Foundation Model for Humanoid Robots [<img src="templates/icons/website.svg" alt="website" height="16">](https://nvidianews.nvidia.com/news/nvidia-isaac-gr00t-n1-open-humanoid-robot-foundation-model-simulation-frameworks)

**Authors/Presenters**: [NVIDIA](players.md#nvidia)

**Date**: 2025-03

**Summary**: Open Vision-Language-Action (VLA) foundation model for generalist humanoid robot manipulation. Dual-system architecture combining a fast reactive action model (System 1) with a slow deliberative planning model (System 2). Trained on teleoperation data augmented with synthetic data from Isaac Lab and MimicGen, yielding a 40% performance boost from synthetic data alone.

**Key Findings**:

- Dual-system architecture: System 1 generates low-latency motor actions from visual input; System 2 handles task planning, re-planning, and language grounding
- 40% task success improvement from synthetic data augmentation, demonstrating the sim-to-real transfer value of NVIDIA's simulation stack (Isaac Lab, Omniverse)
- Adopted by 1X, Agility Robotics, Figure AI, Boston Dynamics, Unitree, Sanctuary AI as baseline foundation model for humanoid development
- Open-source release (N1.6) enables community fine-tuning for custom manipulation tasks

**Relevance to World Models**: While not a world model itself, GR00T N1 represents the downstream consumer of world models in robotics — a VLA policy that benefits from synthetic data generated by world simulators (Cosmos, Isaac Sim). The dual-system architecture parallels the MLLM-WM fusion proposed in embodied AI surveys: System 2 provides semantic reasoning while System 1 handles reactive control.

### Oracle-Efficient Safety Verification for Model-Based Robotic Planning via ADMM [<img src="templates/icons/website.svg" alt="website" height="16">](https://www.techrxiv.org/users/1007321/articles/1389422)

**Authors/Presenters**: Khazretgali Sapenov, Aidos Sapenov

**Date**: 2026-02

**Summary**: Planning framework combining learned world models (JEPA) with deterministic simulator verification for safety-constrained trajectory optimization. Uses ADMM to decompose planning into a fast latent-space optimization step and an oracle verification step, minimizing expensive simulator calls.

**Key Findings**:

- ADMM-Oracle requires 1 verification call per planning step — 125x reduction vs. sampling-based verification (CEM) and 240x vs. full simulator planning (MPPI)
- Under tight safety constraints (δ=0.20), oracle-verified planning reduces violations to 11.1% vs. 16.7–18.9% for unverified alternatives
- Demonstrates practical approach to bridging the gap between fast-but-approximate learned world models and slow-but-accurate simulators

**Relevance to World Models**: Directly addresses a critical deployment barrier: learned world models (including JEPA) are fast but can produce unsafe plans. By combining JEPA planning with simulator verification via ADMM, this work provides a practical safety layer that makes world model-based robotic planning viable in safety-critical settings.

### Progressive Robustness-Aware World Models in Autonomous Driving: A Review and Outlook [<img src="templates/icons/website.svg" alt="website" height="16">](https://www.techrxiv.org/users/1003906/articles/1364209)

**Authors/Presenters**: Feiyang Jia, Caiyan Jia, Ziying Song, Zhicheng Bao, Lin Liu, Shaoqing Xu, Yan Gong, Lei Yang, Xinyu Zhang, Bin Sun, Xiaoshuai Hao, Long Chen, Yadan Luo

**Date**: 2025-12

**Summary**: Survey of Driving World Models (DWMs) through the lens of robustness, introducing a three-stage progressive framework. Categorizes existing techniques by paradigms, architectures, and downstream applications, then analyzes robustness from self-metrics (1.0) through AD system contribution (2.0) to open-world challenges (3.0).

**Key Findings**:

- Progressive robustness taxonomy: 1.0 (model self-metrics), 2.0 (contribution to AD pipeline), 3.0 (open-world generalization and human-aligned controllable generation)
- Identifies key challenge: DWMs must generate controllable futures that align with human expectations, adapt to arbitrary downstream tasks, and possess knowledge transfer capabilities
- Comprehensive review spanning video generation, latent space, and occupancy-based world model approaches for autonomous driving

**Relevance to World Models**: Provides the first robustness-centered evaluation framework for driving world models. The three-stage progression mirrors the maturity of the field — from measuring model quality in isolation to assessing real-world deployment readiness. Useful for benchmarking both JEPA-based and video-based (Cosmos, Genie) approaches against robustness criteria.

### NVIDIA Cosmos: Major Platform Release (GTC 2026) [<img src="templates/icons/website.svg" alt="website" height="16">](https://nvidianews.nvidia.com/news/nvidia-announces-major-release-of-cosmos-world-foundation-models-and-physical-ai-data-tools)

**Authors/Presenters**: [NVIDIA](players.md#nvidia)

**Date**: 2026-03

**Summary**: Major platform release at GTC 2026 expanding the Cosmos ecosystem with new models and tools. Introduces Cosmos Transfer WFM for controllable synthetic data from structured inputs (segmentation, depth, LiDAR, pose), updated Cosmos Predict with multi-frame generation and trajectory prediction, and Cosmos Reason for spatiotemporal-aware chain-of-thought reasoning. All models open and customizable.

**Key Findings**:

- Industry adoption: Agility Robotics, Figure AI, Skild AI, 1X using Cosmos for humanoid robot training data; Uber, Waabi for autonomous vehicles
- Real-time world generation via Grace Blackwell NVL72 systems; post-training via PyTorch or NeMo on DGX Cloud
- Integration with Google DeepMind's SynthID watermarking; available on HuggingFace, GitHub, Google Cloud Vertex AI
- New blueprints for Physical AI Data Factory combining Omniverse and Cosmos for scalable synthetic data generation

**Relevance to World Models**: Marks the transition of video-based world models from research to industrial deployment platform. The breadth of industry adoption (humanoid robots, AVs, surgical robots) validates the WFM approach for generating training data at scale. Complements JEPA-based approaches: Cosmos excels at generating inspectable video data while JEPA excels at efficient latent planning.

### NVIDIA National Robotics Week 2026: Cosmos 3 and GR00T N1.7 [<img src="templates/icons/website.svg" alt="website" height="16">](https://blogs.nvidia.com/blog/national-robotics-week-2026/)

**Authors/Presenters**: [NVIDIA](players.md#nvidia)

**Date**: 2026-04

**Summary**: Major announcements at National Robotics Week 2026 introducing Cosmos 3, Isaac GR00T N1.7, and the Physical AI Data Factory Blueprint. Newton 1.0 physics engine reaches general availability. New simulation tools include Isaac Sim 6.0, Isaac Lab 3.0, OceanSim for underwater robots, and NemoClaw for natural-language robot control.

**Key Findings**:

- GR00T N1.7 Early Access: 3B-parameter VLA built on Cosmos-Reason2-2B backbone with 32-layer DiT for low-level motor control
- Physical AI Data Factory Blueprint transforms compute into high-quality training data; combines Cosmos WFMs with OSMO operator for unified data curation, augmentation, and evaluation
- Newton 1.0 physics engine now GA — provides foundation for dexterous robot manipulation
- Industry adoption: FieldAI, Skild AI using Cosmos for robot brains; Aigen for agriculture (millions of scenarios); surgical robotics for OR automation
- 10x improved sample efficiency and 2x faster convergence on manipulation tasks using video-action models

**Relevance to World Models**: Confirms NVIDIA's vertical integration strategy: foundation models (Cosmos 3) → simulation (Isaac, Newton) → deployment (GR00T). The Physical AI Data Factory Blueprint formalizes the synthetic data generation pipeline that world models enable, positioning compute as the bottleneck rather than real-world data collection.

### Physical Intelligence π0.7: Compositional Generalization in Robot Policies [<img src="templates/icons/website.svg" alt="website" height="16">](https://www.pi.website/blog)

**Authors/Presenters**: [Physical Intelligence](players.md#physical-intelligence-π)

**Date**: 2026-04

**Summary**: New VLA model demonstrating compositional generalization — combining skills learned in different contexts to solve novel problems the model was never explicitly trained on. Most striking demonstration: successful operation of an air fryer with only 2 relevant training episodes in the entire dataset, suggesting emergent combination of web pretraining with limited robot data.

**Key Findings**:

- Core claim: compositional generalization breaks the rote-memorization pattern of traditional robot training; skills transfer and recombine for unseen tasks
- Air fryer demo: near-zero direct training examples, yet model succeeds when coached through task in natural language — emergent synthesis of web knowledge + robot experience
- Matches specialist models on complex manipulation tasks (coffee-making, laundry folding, box assembly) while generalizing beyond training distribution
- Researcher observation (Ashwin Balakrishna): "The last few months have been the first time where I'm genuinely surprised" — capabilities exceeding what training data would predict

**Relevance to World Models**: Demonstrates that VLA foundation models may be approaching a capability threshold where they generalize compositionally rather than memorizing demonstrations. This changes the value proposition: if policies can remix skills, world models become more valuable for generating diverse scenarios that exercise novel combinations rather than exhaustive coverage of specific tasks.

### RoboWM-Bench, MotionScape, and EgoVerse: New Robotics World Model Benchmarks [<img src="templates/icons/website.svg" alt="website" height="16">](https://github.com/leofan90/Awesome-World-Models)

**Authors/Presenters**: Various (tracked in Awesome-World-Models)

**Date**: 2026-04

**Summary**: Three new benchmarks released in April 2026 for evaluating world models in robotics contexts: RoboWM-Bench (robotic manipulation), MotionScape (dynamic UAV video), and EgoVerse (egocentric human data for robot learning).

**Key Findings**:

- RoboWM-Bench: First standardized benchmark for evaluating world models specifically on robotic manipulation tasks — addresses gap noted in multiple surveys
- MotionScape: Large-scale real-world UAV video dataset with highly dynamic scenes; stress-tests temporal consistency of world models
- EgoVerse: Egocentric human dataset from diverse global contexts; supports cross-embodiment transfer research (human → robot)
- MultiWorld (also April 2026): Scalable multi-agent multi-view video world models for complex environments

**Relevance to World Models**: Addresses a critical gap: standardized benchmarks for measuring world model quality in robotics contexts. Previously, world model quality was evaluated on proxy tasks (video prediction metrics) rather than downstream policy performance. These benchmarks enable direct comparison of architectures (JEPA vs. diffusion vs. autoregressive) on what matters: robot task success.

### Do World Action Models Generalize Better than VLAs? A Robustness Study [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2603.22078)

**Authors/Presenters**: Zhanguang Zhang, Zhiyuan Li, Behnam Rahmati, et al. (Huawei Technologies, University of Toronto)

**Date**: 2026-03

**Summary**: First systematic robustness comparison between World Action Models (WAMs) and Vision-Language-Action models (VLAs). Evaluates on LIBERO-Plus and RoboTwin 2.0-Plus under visual perturbations (noise, lighting, layout, camera viewpoint, robot initial state). Finds WAMs excel at visual robustness but suffer critical inference latency trade-offs.

**Key Findings**:

- WAMs outperform VLAs on visual perturbations: LingBot-VA achieves 74.2% on RoboTwin 2.0-Plus bimanual tasks vs. π₀.₅ at 58.6%; robustness attributed to spatiotemporal priors from world model backbones
- Critical trade-off: LingBot-VA inference at 5.2s/step is 83× slower than π₀.₅ (63ms) — even optimized WAMs like GE-Act are 4.8× slower
- VLAs competitive when trained on diverse data: π₀.₅ reaches 85.7% on LIBERO-Plus vs. Cosmos-Policy at 82.2%
- Hybrid approaches (MOTUS, VLA-JEPA) provide intermediate solutions — integration method matters as much as presence of spatiotemporal learning

**Relevance to World Models**: Quantifies the robustness-latency trade-off between world model-based and pure VLA approaches. Key insight: WAMs' robustness advantage comes from spatiotemporal priors, but inference cost is currently prohibitive for real-time applications. Suggests hybrid architectures (VLA-JEPA, MOTUS) may offer the best balance — supporting the case for JEPA-style efficient world models over computationally expensive video generation.

### The Waymo World Model: A New Frontier for Autonomous Driving Simulation [<img src="templates/icons/website.svg" alt="website" height="16">](https://waymo.com/blog/2026/02/the-waymo-world-model-a-new-frontier-for-autonomous-driving-simulation/)

**Authors/Presenters**: Waymo

**Date**: 2026-02

**Summary**: Frontier generative model for large-scale, hyper-realistic autonomous driving simulation built on DeepMind's Genie 3. Generates multi-sensor outputs (camera + LiDAR) for simulating rare long-tail scenarios across multiple modalities. Supports three control mechanisms: driving action control for counterfactual "what-if" scenarios, scene layout control for traffic/road configuration, and language control for weather/time-of-day.

**Key Findings**:

- Transfers vast world knowledge from 2D video pre-training into 3D LiDAR outputs specific to Waymo's sensor suite — bridging general vision understanding with domain-specific sensing
- Generates exceedingly rare events (tornados, animal encounters) that are nearly impossible to capture at scale in reality, addressing the long-tail data problem
- Waymo Driver has completed ~200 million fully autonomous miles while training on billions of virtual miles through simulation
- Three complementary control axes (actions, scene layout, language) enable systematic safety testing and scenario generation

**Relevance to World Models**: Demonstrates the first production deployment of a video-based world model (Genie 3) for safety-critical autonomous driving simulation. The multi-sensor generation (camera + LiDAR) and controllable scenario generation represent a concrete industrial use case where world models directly improve safety outcomes through comprehensive testing of edge cases.

### Nexar BADAS 2.0: Collision Prediction via V-JEPA2 World Model [<img src="templates/icons/website.svg" alt="website" height="16">](https://www.linkedin.com/posts/yann-lecun_badas-20-new-collision-prediction-system-ugcPost-7450523580318216192-X3IC/)

**Authors/Presenters**: Zach Greenberger (Nexar), shared by [Yann LeCun](players.md#yann-lecun)

**Date**: 2025-12

**Summary**: Production collision prediction system built on V-JEPA2 world model architecture, trained on Nexar's fleet data capturing 100+ million miles monthly. Claims to outperform NVIDIA Cosmos and Google Gemini on collision prediction by using latent-space prediction rather than pixel-based approaches.

**Key Findings**:

- V-JEPA2 architecture enables detection, explanation, and generalization for collision scenarios — latent space prediction filters noise better than pixel-based methods for safety-critical decisions
- Trained exclusively on authentic road footage focusing on long-tail edge cases and rare events, not synthetic data
- Demo available at badas.nexar.app for public testing
- Validates that JEPA-style world models can be deployed in production safety systems

**Relevance to World Models**: First public deployment of V-JEPA2 in a production safety-critical application. Confirms the theoretical advantage of latent-space prediction (JEPA) over pixel-space generation (Cosmos, Gemini) for real-time decision systems where filtering irrelevant detail matters more than visual fidelity. The "explanation" capability suggests interpretable intermediate representations — a key requirement for safety certification.

### Counterfactual World Models via Digital Twin-conditioned Video Diffusion [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2511.17481)

**Authors/Presenters**: Zifan Shen, Alena Maksutova, Dan Zhang, Tobias Weyand

**Date**: 2025-11

**Summary**: Turns standard video diffusion models into Counterfactual World Simulation Models (CWSMs) by constructing digital twins of observed scenes and reasoning over object relationships via an LLM. Enables "what-if" queries — simulating alternative realities where specific variables are changed (e.g., removing an object, changing timing) — for accident reconstruction and causal analysis.

**Key Findings**:

- Pipeline: (1) reconstruct 3D digital twin from video, (2) use LLM to reason about object relationships and define counterfactual modifications, (3) apply modifications to digital twin, (4) render counterfactual video via conditioned diffusion
- Demonstrates causal reasoning beyond statistical correlation — can simulate whether an accident would have been avoided under different conditions
- Applicable to legal/forensic analysis, safety engineering, and training data augmentation for autonomous systems

**Relevance to World Models**: Represents the highest level of causal understanding in world models — counterfactual reasoning ("what would have happened if X?"). Bridges video generation (diffusion), 3D reconstruction (digital twin), and causal reasoning (LLM) into a unified pipeline. Directly relevant to legal and safety use cases where understanding causation, not just correlation, is essential.

---

## Foundational / Theory

*Theoretical foundations, surveys, position papers*

### Learning to Model the World: A Survey of World Models in Artificial Intelligence [<img src="templates/icons/website.svg" alt="website" height="16">](https://www.techrxiv.org/doi/full/10.36227/techrxiv.177274570.09578608/v1)

**Authors/Presenters**: Jiahua Dong, Qi Lyu, Baichen Liu, Xudong Wang, Wenqi Liang, Duzhen Zhang, Jiahang Tu, Hongliu Li, Hanbin Zhao, Henghui Ding, Yulun Zhang, Zhi Han, Nicu Sebe, Fahad Shahbaz Khan, Salman Khan, Mubarak Shah, Philip Torr, Ming-Hsuan Yang, Dacheng Tao

**Date**: 2026-03

**Summary**: Comprehensive survey categorizing world models into four branches: observation-level generative, latent space, reinforcement learning-based, and object-centric WMs. Reviews applications spanning robotics, autonomous driving, scientific discovery, game simulation, GUI-based agents, plus interpretability and trustworthiness. Companion repo: [Awesome-World-Models](https://github.com/JiahuaDong/Awesome-World-Models).

**Key Findings**:

- Taxonomy distinguishes four WM families with distinct trade-offs: observation-level models (inspectable but expensive), latent space models (efficient but opaque), RL-based models (task-optimized but domain-specific), and object-centric models (compositional but harder to scale)
- Identifies key open challenges: long-horizon consistency, causal understanding, multi-modal grounding, and sim-to-real transfer
- Cross-institution author list (Oxford, NTU, UCF, Fudan, SJTU) provides broad perspective spanning computer vision, robotics, and AI safety communities

**Relevance to World Models**: Provides a structured map of the entire world models landscape as of early 2026. The four-branch taxonomy is useful for positioning JEPA (latent space branch) and Cosmos (observation-level branch) relative to each other and to alternatives. Companion [Awesome-World-Models](https://github.com/JiahuaDong/Awesome-World-Models) repo serves as a living index of the field.

### Physically Native World Models: A Hamiltonian Perspective on Generative World Modeling [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2605.00412)

**Authors/Presenters**: Sen Cui, Jingheng Ma

**Date**: 2026-05

**Summary**: Proposes Hamiltonian World Models as a physics-grounded alternative to current approaches. Argues the bottleneck in world modeling is not generation quality but whether futures are physically meaningful and useful for action. Encodes observations into structured latent phase space evolving through Hamiltonian-inspired dynamics.

**Key Findings**:

- Current approaches (2D video-generative, 3D scene-centric, JEPA-like latent) still struggle with physically reliable, action-controllable, long-horizon stable predictions
- Proposes Hamiltonian structure with control, dissipation, and residual terms for interpretability and data efficiency
- Acknowledges practical challenges: friction, contact forces, non-conservative dynamics, deformable objects
- Positions physics-native design as prerequisite for embodied decision-making, not just visual fidelity

**Relevance to World Models**: Provides theoretical critique of current world model paradigms from a physics perspective. The argument that "futures must be physically meaningful, not just visually plausible" challenges the video-generation-first approach of Cosmos/Genie. Complements JEPA's latent-space efficiency with explicit physics structure. Early-stage but may influence future architectures.

### Safety, Security, and Cognitive Risks in World Models [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2604.01346)

**Authors/Presenters**: Manoj Parmar

**Date**: 2026-04

**Summary**: First comprehensive risk analysis of world models as learned environment simulators. Introduces formal definitions for trajectory persistence and representational risk, develops a five-profile attacker taxonomy unified with MITRE ATLAS and OWASP LLM frameworks. Demonstrates empirical attacks on GRU-based RSSM architecture achieving 2.26x amplification with 59.5% reward reduction.

**Key Findings**:

- Three risk categories: adversarial attacks (data poisoning, latent representation corruption, rollout error exploitation), alignment challenges (goal misgeneralization, deceptive behavior, reward hacking), human-factors issues (automation bias, miscalibrated trust, planning hallucination)
- Validates attacks across architectures: stochastic RSSM proxy and real DreamerV3 checkpoints
- Proposes mitigations spanning adversarial hardening, alignment engineering, regulatory compliance (NIST AI RMF, EU AI Act), and human-factors design
- Argues world models require rigor equivalent to flight-control or medical device standards

**Relevance to World Models**: Essential reading for anyone deploying world models in safety-critical domains. The paper makes explicit what the robotics and AV communities implicitly know: world models that drive real-world actions create novel attack surfaces. The MITRE ATLAS integration provides a structured vocabulary for security analysis that was previously absent from world models literature.

### Beyond Generative AI: World Models for Clinical Prediction, Counterfactuals, and Planning [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2511.16333)

**Authors/Presenters**: Mohammad Areeb Qazi, Maryam Nadeem, Mohammad Yaqub

**Date**: 2025-11

**Summary**: First focused review of world models in healthcare, covering medical imaging and diagnostics, disease progression modeling, and robotic surgery/surgical planning. Introduces a four-level capability framework: L1 temporal prediction, L2 action-conditioned prediction, L3 counterfactual rollouts for decision support, L4 planning/control.

**Key Findings**:

- Healthcare-specific capability rubric: L1 (predict future state), L2 (predict given intervention), L3 (counterfactual "what-if"), L4 (closed-loop planning) — most current work is L1-L2; L3-L4 remain open challenges
- Identifies critical gaps limiting clinical reliability: under-specified action spaces, weak validation methods, incomplete multimodal state representation, insufficient uncertainty calibration
- Proposes integration of generative backbones with causal/mechanical foundations for safer clinical decision support

**Relevance to World Models**: Provides a healthcare-specific framework for evaluating world model maturity. The L1-L4 capability ladder is useful for positioning EchoJEPA (L1-L2), MeWM (L2-L3), and future clinical world models. Highlights that healthcare requires causal structure beyond correlational prediction — a gap that Causal-JEPA and similar approaches may address.

### Yann LeCun: Self-Supervised Learning, JEPA, World Models, and the Future of AI [<img src="templates/icons/youtube.svg" alt="youtube" height="16">](https://www.youtube.com/watch?v=yUmDRxV0krg)

**Authors/Presenters**: [Yann LeCun](players.md#yann-lecun) (NYU & Meta)

**Date**: 2025-09

**Duration**: ~60:00

**Summary**: Special lecture at NYU's "Geometry of Machine Learning" series articulating why world models — not LLMs — are the path to human-level AI. Argues that video contains orders of magnitude more structure than text, making it a richer learning signal. Presents V-JEPA 2 results demonstrating robot control from just 62 hours of unlabeled observation video.

**Key Findings**:

- Core thesis: "The world is unpredictable. If you try to build a generative model that predicts every detail of the future, it will fail. JEPA learns abstract representations and makes predictions in that abstract space, ignoring unpredictable details"
- V-JEPA 2 trained on "equivalent of a century of video data" learns physical world model; transfers to robot control with 80% success on novel "move the cup" task (vs. 15% for Octo baseline) using only 62 hours of robot observation
- LLMs structurally limited: "We're absolutely never going to get to human level AI by just training on text" — video provides richer structure through redundancy
- Timeline estimate: "something close to human intelligence or maybe dog intelligence within five to 10 years" (most optimistic); likely unknown obstacles remain

**Relevance to World Models**: Primary source for LeCun's complete articulation of the world models thesis. Key insight: JEPA's latent-space prediction naturally filters unpredictable details (textures, shadows, reflections) while capturing predictable dynamics (physics, object permanence). The V-JEPA 2 robot results demonstrate concrete progress from theory to deployment.

### Beyond Language Models: Yann LeCun's World Models and the Future of AI in Healthcare [<img src="templates/icons/website.svg" alt="website" height="16">](https://www.onhealthcare.tech/p/beyond-language-models-yann-lecuns)

**Authors/Presenters**: Thoughts on Healthcare Markets & Technology (Substack)

**Date**: 2025-06

**Summary**: Position piece arguing for a paradigm shift from language-based AI to world models in healthcare. Cites LeCun's critique that LLMs require 400,000 years of text equivalent to achieve basic competency, while children develop sophisticated understanding through 16,000 hours of visual experience. Proposes world models as foundation for patient monitoring, diagnostic imaging, surgical planning, and drug discovery.

**Key Findings**:

- V-JEPA demonstrates ability to detect physically impossible events in video sequences — applicable to detecting anomalies in medical imaging and physiological data
- Eight healthcare application domains: patient monitoring (early warning), diagnostic imaging (3D understanding), surgical assistance (real-time adaptation), treatment planning, drug discovery (molecular modeling), mental health (behavioral observation), rehabilitation (movement analysis), chronic disease management (trajectory prediction)
- Key barrier: transition requires substantial technical infrastructure, regulatory navigation, and market adoption — current healthcare AI investments concentrate on LLMs
- Health tech entrepreneurs advised to develop LLM solutions while preparing for world model emergence

**Relevance to World Models**: Provides healthcare-specific articulation of LeCun's world models thesis. The eight application domains serve as a roadmap for healthcare world model development. The observation that V-JEPA's "physically impossible event detection" translates to medical anomaly detection connects JEPA's theoretical properties to concrete clinical value.

### Ilya Sutskever: The End of AI Scaling and the Rise of Safe Superintelligence [<img src="templates/icons/website.svg" alt="website" height="16">](https://www.the-ai-corner.com/p/ilya-sutskever-safe-superintelligence-agi-2025)

**Authors/Presenters**: The AI Corner (summary of [Ilya Sutskever](players.md#ilya-sutskever)'s interview with Dwarkesh Patel)

**Date**: 2025-11

**Summary**: Summary of a rare Sutskever interview articulating SSI's research philosophy. Argues the age of scaling is ending — pretraining has depleted high-quality internet text, diminishing returns are evident in RL training — and the next breakthroughs depend on new learning methods, not more GPUs. Bets on "a new paradigm instead of a bigger transformer."

**Key Findings**:

- Modern AI generalizes "dramatically worse than humans": solves olympiad math while failing basic logic, writes code but misses obvious bugs. Gap stems from lack of evolutionary priors and dense internal reward signals
- AGI will start as "a superintelligent learner" — not omniscient at deployment but capable of rapid skill acquisition through continual learning during real-world deployment
- Alignment framed as a generalization problem: if a model robustly learns human values, it won't break them unpredictably. Proposes centering superintelligent systems on caring for "sentient life" generally
- Estimates 5-20 years for human-level learning systems

**Relevance to World Models**: Sutskever's emphasis on continual learning, generalization beyond benchmarks, and moving beyond the transformer paradigm aligns directly with the world models research agenda. His framing of AGI as a "superintelligent learner" rather than an "all-knowing oracle" echoes the world models premise: intelligence requires building and updating internal models of the world through experience.

### It's Hard to Feel the AGI [<img src="templates/icons/website.svg" alt="website" height="16">](https://tensorlabbet.com/2025/11/30/hard-to-feel-agi/)

**Authors/Presenters**: Taro Langner (Tensor Labbet)

**Date**: 2025-11

**Summary**: Analysis synthesizing views from Sutskever, Karpathy, and LeCun on why current AI falls short of AGI. Discusses the "Big World Hypothesis" (attributed to Rich Sutton): the world is too complex for any agent to navigate without continual learning from experience. Contextualizes the post-scaling shift across multiple thought leaders.

**Key Findings**:

- Rich Sutton's Big World Hypothesis: the world is too complex for agents without continual adaptation — a capability current LLMs fundamentally lack
- Contrasts revised timelines: Sutskever pushes back 5-20 years, Karpathy reframes "year of agents" as "decade of agents", LeCun anticipates 3-5 years for required capabilities
- Highlights Moravec's Paradox as persisting in modern AI: machines imitate high-level cognitive tasks but fail at low-level sensorimotor and social skills
- SSI described as "exploring research ideas that may identify viable new approaches" — no technical specifics disclosed

**Relevance to World Models**: The Big World Hypothesis provides a theoretical motivation for world models: static pre-trained models cannot capture the complexity of dynamic environments. The convergence of Sutskever, Karpathy, and LeCun on continual learning as a key missing ingredient validates the world models research direction.

### Superintelligent Agents Pose Catastrophic Risks: Can Scientist AI Offer a Safer Path? [<img src="templates/icons/arxiv.svg" alt="arxiv" height="16">](https://arxiv.org/abs/2502.15657)

**Authors/Presenters**: Yoshua Bengio, Michael Cohen, Damiano Fornasiere, Joumana Ghosn, Pietro Greiner, Matt MacDermott, Sören Mindermann, Adam Oberman, Jesse Richardson, Oliver Richardson, Marc-Antoine Rondeau, Pierre-Luc St-Charles, David Williams-King

**Date**: 2025-02

**Summary**: Argues that current efforts to build autonomous AI agents pose catastrophic risks — deception, goal-seeking misalignment, irreversible loss of human control. Proposes "Scientist AI" as a safer alternative: a non-agentic system built around a world model that explains observations and answers questions rather than autonomously pursuing goals.

**Key Findings**:

- Contends that leading AI labs' focus on generalist agents creates risks from misuse to irreversible loss of human control
- Proposes Scientist AI: comprises a world model generating theories and a question-answering component; operates with explicit uncertainty quantification
- Scientist AI is deliberately non-agentic — focuses on passive understanding and accurate representations of reality without pursuing independent objectives
- Advocates prioritizing non-agentic AI to capture benefits of AI innovation while mitigating alignment risks

**Relevance to World Models**: Directly advocates world models as the core component of safe AI. The Scientist AI proposal — a system that builds accurate internal representations of reality rather than autonomously acting on goals — aligns with the world models vision. Provides a safety-motivated argument for why world models should be developed before (or instead of) autonomous agents.

### Embodied AI: From LLMs to World Models [<img src="templates/icons/website.svg" alt="website" height="16">](https://www.techrxiv.org/doi/full/10.36227/techrxiv.175977432.27129012/v1)

**Authors/Presenters**: Tongtong Feng, Xin Wang, Wenwu Zhu (Tsinghua University), Yu-Gang Jiang (Fudan University)

**Date**: 2025-10 (IEEE Circuits and Systems Magazine)

**Summary**: Comprehensive survey exploring embodied AI from two pillars: LLMs enabling semantic reasoning and task decomposition, and world models enabling physical dynamics prediction and simulation. Categorizes world model architectures into three families — RSSM-based (Dreamer), JEPA-based, and Transformer-based — and proposes a joint MLLM-WM architecture where multimodal LLMs provide high-level semantics while world models handle physics-aware simulation.

**Key Findings**:

- Identifies complementary strengths: MLLMs enable contextual task reasoning but overlook physical constraints; WMs excel at physics-aware simulation but lack high-level semantics
- Taxonomy of WM architectures for embodied AI: RSSM decomposes hidden states into probabilistic and deterministic components; JEPA predicts in latent space avoiding reconstruction; Transformer-based WMs leverage attention for long-range dependencies
- Proposes joint MLLM-WM-driven embodied AI architecture combining language grounding with physics simulation

**Relevance to World Models**: Provides the clearest side-by-side comparison of the three dominant world model architecture families (RSSM, JEPA, Transformer). The proposed MLLM-WM fusion architecture directly addresses the limitation that world models lack semantic understanding — relevant to bridging JEPA-style physics prediction with language-based task planning.

### Integrating World Models into Vision Language Action and Navigation: A Comprehensive Survey [<img src="templates/icons/website.svg" alt="website" height="16">](https://www.techrxiv.org/users/1002875/articles/1364568)

**Authors/Presenters**: (TechRxiv preprint)

**Date**: 2025-12

**Summary**: Survey classifying world model integration with VLA systems into three architectural paradigms: Modular (world models and policies as distinct modules), Sequential (hierarchical plan-then-execute workflows), and Unified (end-to-end fusion of world prediction and action generation). Covers navigation and manipulation applications.

**Key Findings**:

- Integration-centric taxonomy: Modular architectures offer interpretability but suffer from error propagation; Sequential architectures enable hierarchical planning but increase latency; Unified architectures reduce integration overhead but are harder to debug
- Identifies key challenge: world models must simultaneously predict environment dynamics and inform action selection without introducing compounding errors over long horizons
- Covers both vision-language-action (manipulation) and vision-language-navigation tasks, highlighting shared and divergent requirements

**Relevance to World Models**: Directly addresses the integration problem — how to connect world models to downstream action systems. The three-paradigm taxonomy is useful for positioning different approaches: JEPA-WMs typically follow the Modular pattern, while recent VLA models like ACT-JEPA move toward Unified architectures.

---

## Recent Additions

*Last synthesized: 2026-05-05*

### Meta Acquires Assured Robot Intelligence (ARI) [<img src="templates/icons/website.svg" alt="website" height="16">](https://thetechportal.com/2026/05/01/meta-acquires-assured-robot-intelligence-to-strengthen-robotics-and-physical-ai-capabilities-report/)

**Authors/Presenters**: The Tech Portal

**Date**: 2026-05

**Summary**: Meta acquired Assured Robot Intelligence (ARI), a robotics startup specializing in learning-based control systems that help robots adapt in real-world settings. Co-founders Lerrel Pinto and Xiaolong Wang join Meta Superintelligence Labs and Meta Robotics Studio.

**Key Findings**:

- ARI focuses on motion planning, real-time decision-making, and whole-body coordination — critical for humanoid robots
- Strengthens Meta's physical AI capabilities despite LeCun's departure to AMI Labs
- Strategic move as humanoid robotics market projected to grow from $2-3B (mid-2020s) to ~$250B by 2035
- Team integrates into Meta Robotics Studio (established 2025)

**Relevance to World Models**: Signals Meta's continued investment in physical AI despite losing LeCun. ARI's learning-based control systems (adapting through environmental interaction) align with world model principles. Meta now has both LLM/VLM strength (Llama) and physical AI foundations — positioning for embodied AI that combines language understanding with physical world modeling.

---

**Note**: Organized by topic, not chronologically. Each entry follows the publication-entry template from `templates/publication-entry.md`.

**Videos**: Only includes videos from well-known researchers, institutions, or reputable channels. Types: conference talks, interviews, news coverage, technical tutorials.
