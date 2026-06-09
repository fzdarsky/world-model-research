# Open Source and Open Data Projects

> GitHub repos, frameworks, libraries, tools, and datasets for world models research

**Last Updated**: 2026-06-09

---

## JEPA Implementations

*Projects implementing JEPA variants*

### EB-JEPA: Energy-Based Joint-Embedding Predictive Architectures

**URL**: [github.com/facebookresearch/eb_jepa](https://github.com/facebookresearch/eb_jepa)

**Description**: Open-source library providing community examples of Joint Embedding Predictive Architectures for learning representations from images, video, and action-conditioned video, with planning capabilities. Self-contained training examples runnable on single GPU within hours.

**Tech Stack**: Python, PyTorch, Weights & Biases integration, optional Conda/SLURM support

**Key Features**:

- Three main examples: Image JEPA, Video JEPA, and Action-Conditioned Video JEPA
- Single-GPU training within hours per example (91% CIFAR-10 probing accuracy, 97% Two Rooms planning success)
- SLURM launcher support for multi-seed sweeps and distributed training
- Comprehensive testing framework with code formatting standards
- Modular design showing progressive path from image → video → action-conditioned world model

**Status**: Active

**Stats**: 464 stars, 35 forks, 34 commits (Meta AI Research)

**Last Updated**: 2025-12 (created), actively maintained through 2026-02

### V-JEPA 2: Self-Supervised Video Models

**URL**: [github.com/facebookresearch/vjepa2](https://github.com/facebookresearch/vjepa2)

**Description**: PyTorch implementation of state-of-the-art self-supervised video encoders achieving top performance on motion understanding and action anticipation. Includes V-JEPA 2 (pre-trained encoder) and V-JEPA 2-AC (action-conditioned variant for robot manipulation with zero-shot planning). V-JEPA 2.1 (March 2026) adds a new training recipe producing high-quality, temporally consistent dense features.

**Tech Stack**: Python 3.12, PyTorch, Vision Transformer (ViT), CUDA, TimM, Einops

**Key Features**:

- Masked latent feature prediction on internet-scale video data
- Multiple model sizes: ViT-L/16 (300M), ViT-H/16 (600M), ViT-g/16 (1B parameters)
- V-JEPA 2.1: improved temporally consistent dense features via novel training recipe
- Action-conditioned world model for robot task solving (45% grasping success vs. 8% baseline, 73% pick-and-place vs. 13%)
- Pre-trained checkpoints via PyTorch Hub and HuggingFace
- Benchmark results: EK100 (39.7%), SSv2 (77.3%), Diving48 (90.2%)

**Status**: Active

**Stats**: 3,100+ stars, 347 forks (Meta AI Research)

**Last Updated**: 2025-06 (released), V-JEPA 2.1 released 2026-03-16

### JEPA-WMs: Physical Planning with Joint-Embedding Predictive World Models

**URL**: [github.com/facebookresearch/jepa-wms](https://github.com/facebookresearch/jepa-wms)

**Description**: Code, data, and pretrained weights for systematic ablation of JEPA-based world models for physical planning. Includes pretrained JEPA-WMs alongside DINO-WM and V-JEPA-2-AC baselines, with environments for navigation and manipulation tasks.

**Tech Stack**: Python, PyTorch, HuggingFace (models + datasets)

**Key Features**:

- Pretrained checkpoints for JEPA-WMs, DINO-WM, and V-JEPA-2-AC(fixed) baselines
- Multiple simulated environments for navigation and manipulation
- Comprehensive ablation framework covering predictor architecture, encoder type, rollout strategy, and planning optimizer
- CC-BY-NC 4.0 licensed models and datasets on HuggingFace

**Status**: Active

**Stats**: 160 stars, 17 forks, 1 contributor (Meta AI Research)

**Last Updated**: 2026-02

### HWM: Hierarchical Planning with Latent World Models

**URL**: [github.com/kevinghst/HWM_PLDM](https://github.com/kevinghst/HWM_PLDM)

**Description**: Code and pretrained weights for hierarchical MPC with latent world models. Implements two-level planning (macro-action subgoal generation + short-horizon execution) across multiple world model backbones (V-JEPA-2-AC, DINO-WM, PLDM) for navigation and manipulation tasks.

**Tech Stack**: Python, PyTorch

**Key Features**:

- Model-agnostic hierarchical planning layer that plugs into existing latent world models
- Multi-temporal-scale predictor training with macro-action encoding
- Evaluated on real-robot Franka manipulation, Push-T, and maze navigation
- Achieves 70% success on real-robot pick-and-place (vs 0% for flat planner)

**Status**: Active

**Stats**: 113 stars, 14 forks, NYU + Meta AI Research

**Last Updated**: 2026-05

### LeWorldModel (LeWM): Stable End-to-End JEPA from Pixels

**URL**: [github.com/lucas-maes/le-wm](https://github.com/lucas-maes/le-wm)

**Description**: Official implementation of LeWorldModel, the first JEPA that trains stably end-to-end from raw pixels using only two loss terms. ~15M parameters trainable on a single GPU in hours, plans up to 48x faster than foundation-model-based world models.

**Tech Stack**: Python, PyTorch

**Key Features**:

- Minimal training recipe: next-embedding prediction loss + Gaussian latent regularizer (2 loss terms vs. 6 in alternatives)
- Single-GPU training in hours at ~15M parameters
- Competitive across 2D and 3D control tasks
- MIT licensed

**Status**: Active

**Stats**: 1,623 stars, 139 forks, 3 contributors (Mila, NYU, Brown)

**Last Updated**: 2026-03

### EchoJEPA: Latent Predictive Foundation Model for Echocardiography

**URL**: [github.com/bowang-lab/EchoJEPA](https://github.com/bowang-lab/EchoJEPA)

**Description**: First foundation-scale JEPA for medical imaging, trained on 18M echocardiograms across 300K patients. Adapts V-JEPA 2 with domain-specific modifications for cardiac ultrasound, learning anatomical representations that filter speckle noise. EchoJEPA-L released on public data for independent evaluation.

**Tech Stack**: Python, PyTorch, Vision Transformer

**Key Features**:

- ~20% improvement on LVEF, 17% on RVSP over leading baselines
- 79% view classification with 1% labels vs. 42% for best baseline at 100%
- Domain-specific adaptations: 24 fps sampling, conservative cropping, narrow aspect ratio augmentation
- Apache 2.0 licensed

**Status**: Active

**Stats**: 273 stars, 42 forks, 2 contributors (U. Toronto, Vector Institute, U. Chicago)

**Last Updated**: 2026-02

### Locate 3D / 3D-JEPA: Object Localization via Self-Supervised 3D Learning

**URL**: [github.com/facebookresearch/locate-3d](https://github.com/facebookresearch/locate-3d)

**Description**: 3D-JEPA encoder and Locate 3D model for localizing objects in 3D scenes from natural language referring expressions. 3D-JEPA applies masked prediction in latent space to sensor point clouds featurized with 2D foundation models (CLIP, DINO), then fine-tunes with a language-conditioned decoder for 3D mask and bounding box prediction.

**Tech Stack**: Python, PyTorch, Conda, HuggingFace (model: facebook/3d-jepa)

**Key Features**:

- 3D-JEPA: self-supervised learning on point clouds via masked latent prediction — extends JEPA principle to 3D spatial data
- Locate 3D: SOTA referential grounding from referring expressions ("the small coffee table between the sofa and the lamp")
- Operates directly on sensor observation streams (posed RGB-D frames), enabling deployment on robots and AR devices
- Locate 3D Dataset: 130K+ annotations across multiple capture setups for systematic generalization study

**Status**: Active

**Stats**: (Meta AI Research)

**Last Updated**: 2025-04

### ThinkJEPA: VLM-Guided Latent World Models

**URL**: [github.com/Hai-chao-Zhang/ThinkJEPA](https://github.com/Hai-chao-Zhang/ThinkJEPA)

**Description**: Dual-path embodied prediction framework combining a VLM "thinker" (Qwen3-VL-Thinking) with a JEPA "controller" (V-JEPA 2 predictor) for trajectory prediction. VLM provides long-horizon semantic guidance via hierarchical pyramid features; JEPA branch handles fine-grained dynamics.

**Tech Stack**: Python 3.10/3.11, PyTorch 2.10.0, Qwen3-VL, V-JEPA 2 (bundled subtree), EgoDex dataset, HuggingFace, DDP multi-GPU training

**Key Features**:

- Dual-temporal pathway: dense JEPA frames + sparse VLM frames with hierarchical pyramid guidance transfer
- Pre-extracted Qwen3-VL feature cache available on HuggingFace (haichaozhang/cache)
- Bundled V-JEPA 2 subtree and EgoDex data helpers
- BSD-3-Clause-based custom license with attribution requirements

**Status**: Active

**Stats**: 38 stars, 5 forks, 1 contributor

**Last Updated**: 2026-03

---

## EBM Libraries & Frameworks

*Tools and libraries for Energy-Based Models*

---

## World Model Frameworks

*Complete frameworks like DreamerV3, etc.*

### Baby Dragon Hatchling (BDH)

**URL**: [github.com/pathwaycom/bdh](https://github.com/pathwaycom/bdh)

**Description**: Biologically-inspired LLM architecture based on a scale-free network of locally-interacting neuron particles with Hebbian learning. Bridges deep learning and neuroscience while matching GPT-2 performance at 10M–1B parameters.

**Tech Stack**: Python, PyTorch

**Key Features**:

- Scale-free network topology with excitatory/inhibitory neuron dynamics
- Hebbian working memory via synaptic plasticity with monosemantic properties
- GPU-optimized state-space formulation
- Sparse, positive, interpretable activations
- Active community: MLX port, Burn framework port, dynamic vocabulary extensions

**Status**: Active

**Stats**: 3,400+ stars, 211 forks, 5 contributors (Pathway)

**Last Updated**: 2025-09

### Cosmos 3: Unified Omnimodal World Model

**URL**: [github.com/nvidia/Cosmos](https://github.com/nvidia/Cosmos)

**Description**: NVIDIA's unified omnimodal world model platform combining vision-language reasoning, video/audio generation, and action prediction in a single Mixture-of-Transformers architecture. Supersedes the separate Predict/Transfer/Reason model repos with a unified framework supporting text, image, video, audio, and action modalities.

**Tech Stack**: Python, PyTorch, Hugging Face Diffusers, vLLM, vLLM-Omni, Qwen3-VL (base for Nano/Super)

**Key Features**:

- Three model scales: Edge (4B), Nano (16B), Super (64B) with dual-tower MoT architecture
- Five open model checkpoints: Super, Nano, Super-Text2Image, Super-Image2Video, Nano-Policy-DROID
- Five curated synthetic datasets (PhyxSim, RobotSim, DriveSim, SynHuman, Warehouse) on HuggingFace
- Cosmos-HUE evaluation benchmark for Physical AI video generation
- OpenMDW-1.1 License (open weights, commercial use permitted)

**Status**: Active

**Stats**: 8,500 stars, 543 forks, 84 watchers (NVIDIA)

**Last Updated**: 2026-06

### Cosmos-Predict2.5: World Simulation Foundation Model

**URL**: [github.com/nvidia-cosmos/cosmos-predict2.5](https://github.com/nvidia-cosmos/cosmos-predict2.5)

**Description**: Latest generation of NVIDIA's Cosmos World Foundation Models, a flow-based model unifying Text2World, Image2World, and Video2World into a single architecture for simulating and predicting future world states as video. Uses Cosmos-Reason1 as text encoder for physically-grounded generation.

**Tech Stack**: Python, PyTorch, CUDA, Hugging Face Diffusers, NeMo Framework

**Key Features**:

- Unified flow-based architecture for text/image/video-conditioned world generation at 2B and 14B scales
- RL-based post-training for improved video quality and instruction alignment
- Distilled 2B checkpoint available via Hugging Face Diffusers
- Post-training recipes for robot policy models and action-conditioned distillation (via cosmos-cookbook)
- NVIDIA Open Model License (commercial use permitted)

**Status**: Active

**Stats**: 855 stars, 94 forks, 14 contributors (NVIDIA)

**Last Updated**: 2026-02

### Cosmos-Transfer2.5: World Translation (Sim2Real/Real2Real)

**URL**: [github.com/nvidia-cosmos/cosmos-transfer2.5](https://github.com/nvidia-cosmos/cosmos-transfer2.5)

**Description**: Multi-controlnet built on Cosmos-Predict2.5 for producing world simulations conditioned on multiple spatial control inputs (RGB, depth, segmentation). Includes general Physical AI/robotics checkpoints and specialized autonomous vehicle checkpoints. 3.5x smaller than predecessor with superior fidelity.

**Tech Stack**: Python, PyTorch, CUDA, NeMo Framework

**Key Features**:

- Multi-modal structured input: RGB, depth, segmentation maps
- General checkpoints for Physical AI/robotics + specialized AV checkpoints
- Sim2Real and Real2Real world translation capabilities
- 3.5x smaller than Transfer1 with superior long-horizon video generation
- NVIDIA Open Model License (commercial use permitted)

**Status**: Active

**Stats**: 477 stars, 74 forks, 18 contributors (NVIDIA)

**Last Updated**: 2026-03

### Cosmos-Reason2: Physical AI Common Sense & Embodied Reasoning

**URL**: [github.com/nvidia-cosmos/cosmos-reason2](https://github.com/nvidia-cosmos/cosmos-reason2)

**Description**: Multimodal language models for physical common sense understanding and embodied decision-making via chain-of-thought reasoning. Based on Qwen3-VL architecture; #1 open model on Physical AI Bench and Physical Reasoning leaderboards. Serves as reasoning backbone for Cosmos world simulation pipeline.

**Tech Stack**: Python, PyTorch, Qwen3-VL, NeMo Framework, Hugging Face

**Key Features**:

- 2B and 8B model variants for Physical AI reasoning
- Chain-of-thought reasoning for physical dynamics understanding without human annotations
- Trained with Physical AI SFT + RL on hierarchical ontology (space, time, physics)
- Top-ranked open model on Physical AI Bench leaderboard
- NVIDIA Open Model License (commercial use permitted)

**Status**: Active

**Stats**: 258 stars, 51 forks, 6 contributors (NVIDIA)

**Last Updated**: 2026-02

### Cosmos-RL: Reinforcement Learning Framework for Physical AI

**URL**: [github.com/nvidia-cosmos/cosmos-rl](https://github.com/nvidia-cosmos/cosmos-rl)

**Description**: Flexible and scalable async post-training framework specialized for RL and SFT in Physical AI applications. Supports training across LLM/VLM, world foundation models, and VLA paradigms with fault-tolerant elastic large-scale training.

**Tech Stack**: Python, PyTorch, CUDA, NeMo Framework

**Key Features**:

- SOTA RL algorithms: GRPO, DAPO for LLM/VLM; FlowGRPO, DDRL, DiffusionNFT for world foundation models; VLA-specific algorithms
- 6D Parallelism: Sequence, Tensor, Context, Pipeline, FSDP, DDP
- Dynamic NCCL Process Groups for on-the-fly GPU registration/unregistration enabling fault-tolerant elastic training
- Native support for OpenVLA, OpenVLA-OFT, PI0.5 series models; integrated with LIBERO and BEHAVIOR-1K simulators
- Apache 2.0 licensed (code), NVIDIA Open Model License (models)

**Status**: Active

**Stats**: 367 stars, 53 forks (NVIDIA)

**Last Updated**: 2026-03

### Cosmos-Tokenizer: Video & Image Neural Tokenizers

**URL**: [github.com/NVIDIA/Cosmos-Tokenizer](https://github.com/NVIDIA/Cosmos-Tokenizer)

**Description**: Suite of image and video neural tokenizers supporting the Cosmos WFM pipeline. Provides the tokenization layer that converts raw video/image data into the token representations consumed by Cosmos world foundation models.

**Tech Stack**: Python, PyTorch, CUDA

**Key Features**:

- Neural tokenizers for both image and video modalities
- Foundation component of the Cosmos WFM pipeline
- Open-source under Apache 2 License

**Status**: Maintained

**Stats**: 1,711 stars, 87 forks (NVIDIA)

**Last Updated**: 2025-02

### Cosmos-Cookbook: Post-Training Recipes & Workflows

**URL**: [github.com/nvidia-cosmos/cosmos-cookbook](https://github.com/nvidia-cosmos/cosmos-cookbook)

**Description**: Community-driven collection of post-training scripts, proven workflows, and domain-specific adaptations for the NVIDIA Cosmos ecosystem. Includes recipes for robot policy training, action-conditioned model distillation, and fine-tuning Cosmos models for specific Physical AI domains.

**Tech Stack**: Python, PyTorch, NeMo Framework, Jupyter notebooks

**Key Features**:

- Post-training recipes for robot policy models (RoboCasa, Libero)
- Action-conditioned distillation guides for Predict2.5
- Domain-specific adaptation workflows for AV and robotics
- Community contribution framework for sharing Physical AI workflows

**Status**: Active

**Stats**: 286 stars, 68 forks, 7 contributors (NVIDIA + community)

**Last Updated**: 2026-02

### PhysicsNeMo: Physics-ML Framework for AI Surrogate Models

**URL**: [github.com/NVIDIA/physicsnemo](https://github.com/NVIDIA/physicsnemo)

**Description**: Open-source framework for building, training, and inferring physics-informed ML models. Provides optimized model architectures (neural operators, graph neural networks, diffusion transformers) and scalable data pipelines for scientific/engineering data (point clouds, meshes). Enables AI surrogate models that combine physics-driven causality with simulation data for real-time predictions — the physics simulation layer underlying NVIDIA's autonomous digital twin vision.

**Tech Stack**: Python, PyTorch, CUDA, PyTorch Geometric

**Key Features**:

- Built-in model families: Neural Operators (FNO), Graph Neural Networks, Diffusion Transformers (DiT), Transformers
- PhysicsNeMo Sym: symbolic PDE integration, domain sampling, physics-informed residual computation
- PhysicsNeMo CFD: inference recipes for pre-trained CFD models (e.g., DoMINO Automotive Aerodynamics NIM)
- Domain parallelism for kNN, radius search; distributed training across multi-GPU/multi-node
- Domain packages: Earth-2 Studio (weather/climate), CFD, Curator (data curation for engineering datasets)
- Apache 2.0 licensed

**Status**: Active

**Stats**: 2,600+ stars, 629 forks (NVIDIA)

**Last Updated**: 2026-03

### Isaac-GR00T: Foundation Model for Generalist Humanoid Robots

**URL**: [github.com/NVIDIA/Isaac-GR00T](https://github.com/NVIDIA/Isaac-GR00T)

**Description**: NVIDIA's open foundation model for generalist humanoid robot skills. VLA model taking multimodal input (language instructions + camera images) and outputting manipulation actions. Dual-system architecture with fast reactive control and slow deliberative planning. Latest version N1.7 (April 2026) built on Cosmos-Reason2-2B backbone with 32-layer DiT for low-level motor control. GR00T N2 (previewed GTC 2026, coming end 2026) will be built on DreamZero WAM architecture with 2x generalization improvement.

**Tech Stack**: Python, PyTorch, CUDA, Isaac Lab, LeRobot integration

**Key Features**:

- Open VLA foundation model for humanoid manipulation with dual-system (reactive + deliberative) architecture
- N1.7 (April 2026): 3B parameters, Cosmos-Reason2-2B backbone, 32-layer DiT for motor control
- N2 Preview (GTC 2026): Based on DreamZero WAM architecture; 2x generalization vs VLAs; #1 on MolmoSpaces and RoboArena
- 40% task success boost from synthetic data (Isaac Lab, MimicGen)
- Adopted by 1X, Agility, Figure AI, Boston Dynamics, Unitree, Sanctuary AI, Humanoid, LG Electronics, NEURA, Noble Machines
- LeRobot integration: NVIDIA + HuggingFace collaboration integrating Isaac/GR00T into LeRobot framework
- Big 4 industrial robotics (ABB, FANUC, YASKAWA, KUKA) integrating Omniverse + Isaac for virtual commissioning
- NVIDIA Open Model License (commercial use permitted)

**Status**: Active

**Stats**: 6,568 stars, 1,095 forks, 34 contributors (NVIDIA)

**Last Updated**: 2026-05

### OpenPI: Open-Source π0 VLA Foundation Models

**URL**: [github.com/Physical-Intelligence/openpi](https://github.com/Physical-Intelligence/openpi)

**Description**: Physical Intelligence's open-source VLA foundation models for general-purpose robot manipulation. Includes model variants: π0 (flow-based VLA), π0-FAST (autoregressive VLA using FAST action tokenizer), π0.5 (knowledge insulation for open-world generalization), and π0.7 (April 2026, compositional generalization). Pre-trained on 10K+ hours of robot data across 7 platforms and 68 tasks. Fine-tuning requires only 1-20 hours of data for new tasks.

**Tech Stack**: Python, JAX (native), PyTorch (HuggingFace port via LeRobot)

**Key Features**:

- Model variants: π0 (flow-based), π0-FAST (autoregressive), π0.5 (open-world), π0.7 (compositional generalization)
- π0.7 (April 2026): Demonstrates compositional generalization — combines skills from different contexts to solve novel problems; air fryer demo with only 2 training episodes
- Pre-trained on 10K+ hours across 7 robot platforms, 68 tasks
- 1-20 hours of data sufficient for fine-tuning to new tasks
- Multi-platform support: ALOHA, DROID, and custom robots
- HuggingFace/LeRobot PyTorch port available for those preferring PyTorch over JAX
- vLLM-Omni targeting OpenPI-style WebSocket API as standard robotics interface ([RFC #1987](https://github.com/vllm-project/vllm-omni/issues/1987))

**Status**: Active

**Stats**: 11,484 stars, 1,817 forks (Physical Intelligence)

**Last Updated**: 2026-04

### DreamZero: World Action Model for Zero-Shot Robot Policies

**URL**: [github.com/dreamzero0/dreamzero](https://github.com/dreamzero0/dreamzero)

**Description**: NVIDIA's 14B-parameter World Action Model (WAM) that jointly predicts video frames and robot actions through shared denoising on a pretrained video diffusion backbone. Unlike VLAs trained on static image-text, WAMs learn physical dynamics from video, achieving 2x better generalization to unseen tasks. DreamZero-Flash achieves single-step inference at ~150ms via decoupled noise schedules (38x speedup). Cross-embodiment transfer adapts to new robots with 30 minutes of play data. GR00T N2 (planned end 2026) will be built on DreamZero architecture.

**Tech Stack**: Python, PyTorch, CUDA

**Key Features**:

- 14B-param WAM jointly predicting video + actions via shared denoising
- 2x better generalization than VLAs on unseen tasks (39.5% vs 16.3% task progress)
- DreamZero-Flash: single-step inference at ~150ms (38x speedup)
- Cross-embodiment: adapts to new robots with 30 min of play data
- P0 priority in vLLM-Omni world model support ([RFC #1987](https://github.com/vllm-project/vllm-omni/issues/1987))
- Apache 2.0 licensed

**Status**: Active

**Stats**: 1,740 stars, 135 forks (NVIDIA)

**Last Updated**: 2026-04

### LingBot-VA: Causal Video-Action World Model for Robot Control

**URL**: [github.com/Robbyant/lingbot-va](https://github.com/robbyant/lingbot-va)

**Description**: Autoregressive diffusion framework from Robbyant (Ant Group) that learns frame prediction and policy execution simultaneously. Features Mixture-of-Transformers (MoT) architecture with shared latent space for vision and action tokens, closed-loop rollout with ground-truth observations, and asynchronous inference pipeline parallelizing action prediction and motor execution. Reportedly outperforms π0.5 by 20% on task success rate.

**Tech Stack**: Python, PyTorch

**Key Features**:

- Autoregressive video-action world modeling: "deduce while acting"
- 20% higher task success rate vs π0.5
- 90%+ success on RoboTwin 2.0 two-arm collaborative benchmark
- 98.5% on LIBERO long-sequence lifelong learning benchmark (industry record)
- Asynchronous inference pipeline for efficient robot control
- Part of LingBot family: LingBot-Depth, LingBot-VLA, LingBot-World, LingBot-VA

**Status**: Active

**Stats**: (Robbyant / Ant Group)

**Last Updated**: 2026-04

### NE-Dreamer: Next Embedding Prediction for World Models

**URL**: [github.com/corl-team/nedreamer](https://github.com/corl-team/nedreamer)

**Description**: Decoder-free MBRL agent using a temporal transformer to predict next-step encoder embeddings from latent state sequences. Matches or exceeds DreamerV3 on DeepMind Control Suite with substantial gains on DMLab memory/reasoning tasks.

**Tech Stack**: Python, PyTorch

**Key Features**:

- Decoder-free architecture — no pixel reconstruction, learns entirely in embedding space
- Temporal transformer with next-step target shift for predictive sequence modeling
- Competitive with DreamerV3 on DMC, superior on DMLab memory tasks
- MIT licensed

**Status**: Active

**Stats**: 31 stars, 1 fork, 1 contributor

**Last Updated**: 2026-03

### RLVR-World: Training World Models with Reinforcement Learning

**URL**: [github.com/thuml/RLVR-World](https://github.com/thuml/RLVR-World)

**Description**: Unified framework applying RL with verifiable rewards (RLVR) to optimize world models for transition prediction metrics. Supports both language-based and video-based world models across text games, web navigation, and robot manipulation. NeurIPS 2025.

**Tech Stack**: Python, PyTorch, Hugging Face Transformers

**Key Features**:

- +30.7% accuracy for text world models (1.5B LLM rivaling GPT-4)
- +15.1% F1 on web navigation; +18.4% relative on WebArena agent success
- Covers language and video modalities with unified RLVR post-training paradigm
- MIT licensed

**Status**: Maintained

**Stats**: 237 stars, 11 forks, 3 contributors (Tsinghua University)

**Last Updated**: 2025-10

### stable-worldmodel: Reproducible World Model Research & Evaluation

**URL**: [github.com/galilai-group/stable-worldmodel](https://github.com/galilai-group/stable-worldmodel)

**Description**: Standardized library for world model research providing integrated data collection, model training, and evaluation with model predictive control. Analogous to Stable Baselines3 but for world models — ships pre-implemented baselines (DINO-WM, GCBC, HILP, GCIVL, GCIQL) across 16 environments with both zeroth-order and gradient-based planning solvers.

**Tech Stack**: Python 3.10+, PyTorch, HDF5/MP4 datasets, uv package manager, Ruff

**Key Features**:

- Pre-implemented baselines: DINO-WM, GCBC, HILP, GCIVL, GCIQL
- Planning solvers: zeroth-order (CEM, MPPI) and gradient-based (SGD, Adam, PGD)
- 16 environments across DeepMind Control Suite, OGBench, PushT, Two-Room
- Optimized data loading (HDF5/MP4) to reduce CPU bottlenecks and maximize GPU utilization
- Gymnasium-compatible interface for custom environments
- `pip install stable-worldmodel`

**Status**: Active

**Stats**: 181 stars, 28 forks, 8 contributors (Galilai group — academic; lead contributors: Lucas Maes, Quentin Llavador, Randall Balestriero)

**Last Updated**: 2026-02

### Genesis World: Multi-Physics Simulation Platform

**URL**: [github.com/Genesis-Embodied-AI/genesis-world](https://github.com/Genesis-Embodied-AI/genesis-world)

**Description**: Open-source simulation platform for physical AI combining a unified multi-physics engine, photo-realistic renderer (Nyx), and cross-platform compiler (Quadrants) behind a Pythonic API. Started as an academic project (Dec 2024), now backed by [Genesis AI](../research/players.md#genesis-ai). Sim-to-real correlation of 0.90 Pearson across 14 tasks.

**Tech Stack**: Python, Quadrants compiler (CUDA, ROCm, Metal, Vulkan, x86/ARM64), Nyx renderer

**Key Features**:

- Unified multi-physics: Rigid, FEM, MPM, Particle (PBD/SPH), uipc, explicit coupler, SAP — all sharing one scene and state
- Quadrants compiler: Python kernels JIT-compiled to CUDA, AMD ROCm, Apple Metal, Vulkan, x86/ARM64 via LLVM (forked from Taichi, June 2025)
- Nyx renderer: real-time path-traced, noise-free 1080p in <4ms; 45% smaller reality gap (FID) than next-best simulator
- Up to 4.6x runtime speedup and 10x startup speedup vs. initial release
- Scales from laptop to datacenter GPUs

**Status**: Active

**Stats**: 29.2K stars, 2.8K forks, multi-contributor ([Genesis AI](../research/players.md#genesis-ai) + community)

**Last Updated**: 2026-06

---

## Inference & Serving

*Frameworks and APIs for serving world models*

### vLLM-Omni: Omni-Modality Model Serving

**URL**: [github.com/vllm-project/vllm-omni](https://github.com/vllm-project/vllm-omni)

**Description**: Extension of vLLM for omni-modality model inference and serving, supporting text, image, video, and audio I/O plus non-autoregressive architectures including Diffusion Transformers (DiT). Reduces job completion time by up to 91.4% vs baselines. Active RFC (#1987) for world model support targeting robotics (DreamZero, Pi0, OpenVLA, GR00T) and interactive video (Genie 3, LingBot-World, Matrix Game) with stateful multi-turn sessions and action I/O.

**Tech Stack**: Python, PyTorch, CUDA, vLLM core

**Key Features**:

- Omni-modality: text, image, video, audio I/O
- Diffusion Transformer (DiT) support for parallel generation
- Disaggregated stage execution for any-to-any model architectures
- 91.4% reduction in job completion time vs baselines
- World Model RFC: targeting OpenPI-style WebSocket API and LeRobot gRPC API as standard robotics interfaces
- Apache 2.0 licensed

**Status**: Active

**Stats**: 4,439 stars, 819 forks (vLLM Project)

**Last Updated**: 2026-04

### LeRobot: End-to-End Learning for Robotics

**URL**: [github.com/huggingface/lerobot](https://github.com/huggingface/lerobot)

**Description**: HuggingFace's framework for making AI for robotics more accessible with end-to-end learning. Provides models, datasets, and tools including a gRPC-based PolicyServer/RobotClient architecture for distributed inference. Supports imitation learning (ACT, Diffusion, VQ-BeT), RL (HIL-SERL, TDMPC), and VLA models (π0-FAST, π0.5, GR00T N1.5, SmolVLA). Emerging as a de facto standard API for robotics model serving.

**Tech Stack**: Python, PyTorch, gRPC, HuggingFace Hub

**Key Features**:

- PolicyServer/RobotClient gRPC architecture (~5x faster than REST)
- Asynchronous inference: robot acts while next chunk computes (~2x task completion speedup)
- Multiple policy architectures: ACT, Diffusion, VQ-BeT, TDMPC, π0, GR00T N1.5
- Hardware-agnostic interface from low-cost arms (SO-100) to humanoids
- Dataset ecosystem on HuggingFace Hub
- vLLM-Omni targeting LeRobot API compatibility

**Status**: Active

**Stats**: 23,488 stars, 4,328 forks (HuggingFace)

**Last Updated**: 2026-04

---

## Datasets & Benchmarks

*Relevant datasets for training and evaluation*

### MolmoSpaces

**URL**: [github.com/allenai/molmospaces](https://github.com/allenai/molmospaces)

**Description**: Large-scale open ecosystem for benchmarking robot navigation and manipulation policies. Provides 230k+ indoor environments, 130k annotated objects (48k manipulable with 42M stable grasps), and an 8-task benchmark suite. Simulator-agnostic across MuJoCo, Isaac Sim, and ManiSkill.

**Tech Stack**: Python, MuJoCo, NVIDIA Isaac Sim, ManiSkill, PyTorch, cuRobo, Open3D

**Key Features**:

- 230k+ environments (handcrafted iTHOR, procedural ProcTHOR, LLM-generated Holodeck)
- 130k annotated object assets with 42M precomputed stable grasps
- MolmoSpaces-Bench: 8-task suite (pick, open, close, etc.) for standardized evaluation
- Sim-to-real correlation R = 0.96, ρ = 0.98
- Scripted data generation pipelines, grasp generation, iPhone teleoperation (TeleDex)
- Supports Franka FR3 and Rainbow Robotics RB-Y1 robots

**Status**: Active

**Stats**: 347 stars, 45 forks; Allen Institute for AI (Ai2)

**Last Updated**: 2026-05 (v0.1.0)

---

## Utilities & Tools

*Supporting tools for research and development*

### Awesome-World-Models: Curated Survey Companion

**URL**: [github.com/JiahuaDong/Awesome-World-Models](https://github.com/JiahuaDong/Awesome-World-Models)

**Description**: Curated list of world model research, companion to the survey "Learning to Model the World: A Survey of World Models in Artificial Intelligence" (TechRxiv, 2026-03). Covers observation-level generative, latent space, RL-based, and object-centric world models across robotics, autonomous driving, scientific discovery, and game simulation.

**Tech Stack**: Markdown (curated list)

**Key Features**:

- Organized by application domain and methodology
- Companion to comprehensive ACM CSUR 2025 survey
- Regularly updated with new papers and resources

**Status**: Active

**Stats**: 165 stars, 3 forks, 3 contributors

**Last Updated**: 2026-03

### Awesome-World-Model-for-Robotics-Policy: Robot Learning Survey Companion

**URL**: [github.com/NTUMARS/Awesome-World-Model-for-Robotics-Policy](https://github.com/NTUMARS/Awesome-World-Model-for-Robotics-Policy)

**Description**: Curated list of world model research for robotic policy learning, companion to the survey "World Model for Robot Learning: A Comprehensive Survey" (arXiv:2605.00080). Policy-centric taxonomy covering world models as policies (IDM-style, single-backbone, MoE/MoT, unified VLA, latent-space), as simulators (for RL, evaluation), and for video generation.

**Tech Stack**: Markdown (curated list)

**Key Features**:

- Policy-centric organization: categorizes by how world models integrate with robot policies
- Covers 100+ papers with links to arXiv, code, project pages, and HuggingFace resources
- Tracks latest entries including GigaBrain, X-WAM, Cortex 2.0, Persistent Robot World Models
- Multi-institutional authorship: NTU, UC Berkeley, Stanford, U. Tokyo, Oxford, ETH Zurich, Princeton, Harvard

**Status**: Active

**Stats**: 581 stars, 10 forks, 33 commits

**Last Updated**: 2026-05

---

**Note**: Each entry follows the project-entry template from `templates/project-entry.md`.
Entries marked as "Archived" are no longer actively maintained.
