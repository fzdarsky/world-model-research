# Open Source and Open Data Projects

> GitHub repos, frameworks, libraries, tools, and datasets for world models research

**Last Updated**: 2026-04-01

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

**Description**: NVIDIA's open foundation model (N1.6) for generalist humanoid robot skills. VLA model taking multimodal input (language instructions + camera images) and outputting manipulation actions. Dual-system architecture with fast reactive control and slow deliberative planning.

**Tech Stack**: Python, PyTorch, CUDA, Isaac Lab, LeRobot integration

**Key Features**:

- Open VLA foundation model for humanoid manipulation with dual-system (reactive + deliberative) architecture
- 40% task success boost from synthetic data (Isaac Lab, MimicGen)
- Adopted by 1X, Agility, Figure AI, Boston Dynamics, Unitree, Sanctuary AI
- Fine-tuning support for custom manipulation tasks
- NVIDIA Open Model License (commercial use permitted)

**Status**: Active

**Stats**: 6,568 stars, 1,095 forks, 34 contributors (NVIDIA)

**Last Updated**: 2026-03

### OpenPI: Open-Source pi0 VLA Foundation Model

**URL**: [github.com/Physical-Intelligence/openpi](https://github.com/Physical-Intelligence/openpi)

**Description**: Physical Intelligence's open-source implementation of the pi0 VLA foundation model for general-purpose robot manipulation. Enables fine-tuning and deployment of robot policies that take language instructions and visual observations as input and produce motor actions. Supports multiple robot platforms out of the box.

**Tech Stack**: Python, PyTorch

**Key Features**:

- Open implementation of pi0 VLA for general-purpose robot manipulation
- Fine-tuning pipeline for adapting to custom robot setups and tasks
- Multi-robot platform support out of the box
- Active community with extensive documentation

**Status**: Active

**Stats**: 10,992 stars, 1,681 forks, 29 contributors (Physical Intelligence)

**Last Updated**: 2026-03

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

---

## Datasets & Benchmarks

*Relevant datasets for training and evaluation*

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

---

**Note**: Each entry follows the project-entry template from `templates/project-entry.md`.
Entries marked as "Archived" are no longer actively maintained.
