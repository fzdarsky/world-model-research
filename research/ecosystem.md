# Ecosystem

> Players in Physical AI — their solutions, reference architectures, and platform relevance

**Last Updated**: 2026-06-15

---

## Big Tech

*Established technology companies with major Physical AI initiatives*

### NVIDIA

**Type**: `Big Tech`
**About**: Largest industrial investor in world foundation models via the Cosmos platform. Frames world models as "the ChatGPT moment for robotics." Building a full-stack Physical AI platform spanning world models, simulation, robot foundation models, physics ML, edge inference, and digital twins. An investor in SSI and AMI Labs.

**Solutions**:

#### Cosmos Platform

- **What it does**: World foundation models for Physical AI — general-purpose video prediction models trained on 20M hours of real-world data for generating synthetic training data, sim-to-real transfer, and world simulation.
- **Building blocks covered**: [Latent World Models](building-blocks.md#latent-world-models), [Video Generation / Prediction Models](building-blocks.md#video-generation--prediction-models), [Sim-to-Real Transfer Pipeline](building-blocks.md#sim-to-real-transfer-pipeline)
- **Key features (functional)**: Cosmos-Predict2.5 (world simulation), Cosmos-Transfer2.5 (sim2real), Cosmos-Reason2 (physical common sense), Cosmos-Tokenizer
- **Key features (non-functional)**: Trained on 20M hours of video; open-weight models under permissive licensing
- **Competes with**: Genie 3, Sora, GAIA series — on synthetic data generation and world simulation
- **Complements**: Isaac Sim (simulation source), GR00T (policy consumer), Omniverse (rendering)
- **Openness**: `OSS-single-vendor`
- **Lock-in vectors**: NVIDIA GPU dependency, Cosmos tokenizer format, integration with NVIDIA ecosystem
- **Source**: [Cosmos Platform](https://www.nvidia.com/en-us/ai/cosmos/), [GitHub](https://github.com/nvidia-cosmos)

#### Isaac Sim

- **What it does**: Physics-based simulation platform for developing and testing robot applications in photorealistic virtual environments.
- **Building blocks covered**: [Simulation Engines](building-blocks.md#simulation-engines), [Sim-to-Real Transfer Pipeline](building-blocks.md#sim-to-real-transfer-pipeline)
- **Key features (functional)**: High-fidelity physics (PhysX), photorealistic rendering, domain randomization, ROS2 integration, sensor simulation
- **Key features (non-functional)**: GPU-accelerated, multi-robot support, cloud deployment
- **Competes with**: Gazebo, Genesis World, MuJoCo — on fidelity and integration
- **Complements**: Cosmos (synthetic data), GR00T (policy training), Omniverse (rendering backbone)
- **Openness**: `Proprietary` (free for individual use)
- **Lock-in vectors**: NVIDIA GPU required, Omniverse dependency, proprietary scene format
- **Source**: [Isaac Sim](https://developer.nvidia.com/isaac-sim)

#### Isaac ROS

- **What it does**: GPU-accelerated middleware for robot perception and navigation, providing hardware-accelerated ROS2 packages.
- **Building blocks covered**: [Robot Middleware](building-blocks.md#robot-middleware), [Edge AI Inference Runtime](building-blocks.md#edge-ai-inference-runtime)
- **Key features (functional)**: GPU-accelerated perception (stereo depth, visual SLAM, object detection), navigation stack, DNN inference integration
- **Key features (non-functional)**: Jetson-optimized, real-time capable, ROS2 Humble/Iron compatible
- **Competes with**: Standard ROS2 perception stack — on latency and throughput via GPU acceleration
- **Complements**: ROS2 (extends, not replaces), Jetson (target hardware), Isaac Sim (sim-to-real)
- **Openness**: `OSS-single-vendor`
- **Lock-in vectors**: Jetson/NVIDIA GPU required for acceleration benefits
- **Source**: [Isaac ROS](https://developer.nvidia.com/isaac-ros), [GitHub](https://github.com/NVIDIA-ISAAC-ROS)

#### GR00T N1

- **What it does**: Open VLA foundation model for humanoid robots with dual-system architecture — System 1 (fast reactive control) + System 2 (deliberative reasoning via VLM).
- **Building blocks covered**: [Robot Foundation Models](building-blocks.md#robot-foundation-models)
- **Key features (functional)**: Cross-embodiment transfer, bimanual manipulation, dual-system architecture, pre-trained on diverse robot data
- **Key features (non-functional)**: Adopted by 1X, Agility, Figure AI, Boston Dynamics, Unitree, Sanctuary AI
- **Competes with**: pi0/pi0.5, Gemini Robotics, GEN-1 — on generalist robot control
- **Complements**: Isaac Sim (training), Cosmos (synthetic data), Jetson (deployment)
- **Openness**: `OSS-single-vendor`
- **Lock-in vectors**: Optimized for Jetson deployment, NVIDIA training infrastructure
- **Source**: [GR00T](https://developer.nvidia.com/groot)

#### Omniverse

- **What it does**: Platform for building and operating digital twins — connects 3D design tools, simulation, and AI in a shared virtual environment using USD (Universal Scene Description).
- **Building blocks covered**: [Digital Twin Runtime](building-blocks.md#digital-twin-runtime), [Simulation Engines](building-blocks.md#simulation-engines)
- **Key features (functional)**: USD-based interoperability, real-time collaboration, physically accurate rendering, digital twin orchestration, connector ecosystem
- **Key features (non-functional)**: Cloud and on-prem deployment, multi-GPU scaling
- **Competes with**: Siemens Xcelerator, Eclipse Ditto — on industrial digital twin capability
- **Complements**: Isaac Sim (robot simulation layer), Cosmos (world model integration), PhysicsNeMo (physics ML)
- **Openness**: `Proprietary` (free tier available)
- **Lock-in vectors**: NVIDIA GPU required, USD format dependency, connector ecosystem
- **Source**: [Omniverse](https://www.nvidia.com/en-us/omniverse/)

#### Jetson

- **What it does**: Edge AI computing platform for deploying AI models on robots, autonomous machines, and IoT devices.
- **Building blocks covered**: [Edge AI Inference Runtime](building-blocks.md#edge-ai-inference-runtime)
- **Key features (functional)**: TensorRT optimization, CUDA acceleration, JetPack SDK, container support
- **Key features (non-functional)**: Low power (10-75W), real-time inference, industrial temperature range (Orin NX/Nano)
- **Competes with**: Qualcomm RB series, Intel/Mobileye EyeQ — on edge AI performance
- **Complements**: Isaac ROS (middleware), GR00T (model deployment), Isaac Sim (sim-to-real target)
- **Openness**: `Proprietary` (JetPack SDK free)
- **Lock-in vectors**: NVIDIA-only hardware, CUDA dependency, TensorRT model format
- **Source**: [Jetson](https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/)

#### PhysicsNeMo

- **What it does**: Framework for building physics-informed neural network models — surrogate models that approximate physical simulations orders of magnitude faster.
- **Building blocks covered**: [Physics-Informed ML Frameworks](building-blocks.md#physics-informed-ml-frameworks)
- **Key features (functional)**: PDE solvers, mesh-based models, Fourier Neural Operators, physics-informed loss functions
- **Key features (non-functional)**: Multi-GPU training, Omniverse integration
- **Competes with**: JAX-based physics simulators, custom PINN implementations — on ease of use and scale
- **Complements**: Omniverse (digital twin physics), Isaac Sim (simulation fidelity)
- **Openness**: `OSS-single-vendor`
- **Lock-in vectors**: NVIDIA GPU required, integration with NVIDIA stack
- **Source**: [PhysicsNeMo](https://developer.nvidia.com/physicsnemo), [GitHub](https://github.com/NVIDIA/physicsnemo)

**Implied reference architecture**: Full vertical integration from silicon (Jetson) through simulation (Isaac Sim/Omniverse) to foundation models (Cosmos/GR00T). Envisions a loop: Cosmos generates synthetic data, Isaac Sim provides simulation, GR00T trains robot policies, Jetson deploys at the edge, and Omniverse orchestrates digital twins. PhysicsNeMo handles physics-informed components. Every layer is GPU-accelerated and optimized for NVIDIA hardware.

- **Source**: [NVIDIA Physical AI Platform](https://www.nvidia.com/en-us/ai/)

**Platform relevance**:

- **Partnership surface**: Middleware layer (Isaac ROS extends ROS2), model serving, fleet management, safety/certification — areas NVIDIA does not fully own
- **Competitive surface**: Simulation, edge inference, digital twins — wherever NVIDIA's stack overlaps with platform capabilities
- **What they need from a platform**: Standards-based interoperability beyond their ecosystem, fleet-level orchestration, safety certification frameworks, vendor-neutral model serving

---

### Meta AI (FAIR)

**Type**: `Big Tech`
**About**: Largest contributor to the JEPA ecosystem, having developed the full progression from I-JEPA to V-JEPA 2 and VL-JEPA. Post-LeCun departure (Jan 2026), Meta continues physical AI investment through Meta Superintelligence Labs and Meta Robotics Studio. Acquired Assured Robot Intelligence (ARI) in May 2026 for learning-based robot control.

**Solutions**:

#### V-JEPA Family

- **What it does**: Self-supervised video representation learning via joint-embedding predictive architecture — learns visual representations by predicting masked spatiotemporal regions in latent space rather than pixel space.
- **Building blocks covered**: [Latent World Models](building-blocks.md#latent-world-models)
- **Key features (functional)**: I-JEPA (images), V-JEPA (video), V-JEPA 2 (world model with planning), V-JEPA 2.1 (improved), VL-JEPA (vision-language)
- **Key features (non-functional)**: Open-weight models, Apache 2.0 license
- **Competes with**: VideoMAE, Cosmos latent models — on self-supervised video understanding
- **Complements**: EB-JEPA (energy-based training), downstream VLA models
- **Openness**: `OSS-single-vendor`
- **Lock-in vectors**: Minimal — open weights and code, standard PyTorch
- **Source**: [GitHub](https://github.com/facebookresearch)

#### EB-JEPA

- **What it does**: Energy-based training library for JEPA architectures — provides energy-based model primitives and training loops as an alternative to the EMA teacher-student paradigm.
- **Building blocks covered**: [Latent World Models](building-blocks.md#latent-world-models)
- **Key features (functional)**: Energy-based training, VICReg integration, configurable architectures
- **Key features (non-functional)**: Open-source, PyTorch-based
- **Competes with**: Standard SSL frameworks (DINO, MAE) — on JEPA-specific training
- **Complements**: V-JEPA family (shared architecture), downstream policy models
- **Openness**: `OSS-single-vendor`
- **Lock-in vectors**: Minimal
- **Source**: [GitHub](https://github.com/facebookresearch)

**Implied reference architecture**: JEPA as the perception backbone — V-JEPA learns world representations, VL-JEPA adds language grounding, and downstream models consume these representations for planning and action. Meta envisions JEPA replacing contrastive and generative pretraining for physical AI. Post-ARI acquisition, expects to connect JEPA representations to learned robot control.

**Platform relevance**:

- **Partnership surface**: JEPA models as perception building blocks, integration with robot middleware and simulation
- **Competitive surface**: Limited — Meta's focus is research and open-source, not commercial platforms
- **What they need from a platform**: Deployment infrastructure for JEPA models, integration with robot hardware, sim-to-real pipelines

---

### Google DeepMind

**Type**: `Big Tech`
**About**: Leading AI research lab (Alphabet) with multiple world-model-adjacent efforts spanning interactive world models, robotics foundation models, and physics engines. Gemini Omni (May 2026) fuses reasoning, video generation, and world simulation into a unified multimodal model explicitly positioned as a world model.

**Solutions**:

#### Gemini Robotics

- **What it does**: VLA foundation model for robot control — translates visual observations and language instructions into robot actions with embodied reasoning capabilities.
- **Building blocks covered**: [Robot Foundation Models](building-blocks.md#robot-foundation-models)
- **Key features (functional)**: Gemini Robotics 1.5/On-Device (VLA), Gemini Robotics-ER 1.6 (embodied reasoning, spatial understanding, instrument reading), action chunking for high-frequency control
- **Key features (non-functional)**: ~250ms latency, 50Hz via action chunking, on-device deployment option
- **Competes with**: GR00T N1, pi0/pi0.5, GEN-1 — on generalist robot control
- **Complements**: Gemini Omni (reasoning backbone), Newton (physics simulation)
- **Openness**: `Proprietary` (API access)
- **Lock-in vectors**: Google Cloud dependency, Gemini API, proprietary model
- **Source**: [Gemini Robotics](https://deepmind.google/models/gemini-robotics/)

#### Genie 3

- **What it does**: Interactive world model generating playable 720p/24fps environments from text or image prompts — learns physics and dynamics from video data.
- **Building blocks covered**: [Video Generation / Prediction Models](building-blocks.md#video-generation--prediction-models), [Simulation Engines](building-blocks.md#simulation-engines)
- **Key features (functional)**: Interactive generation (responds to actions), 720p resolution, 24fps, physics-aware generation
- **Key features (non-functional)**: Prompt-driven world creation
- **Competes with**: Cosmos, Sora — on interactive world simulation
- **Complements**: Gemini Robotics (training environments), Gemini Omni (unified model)
- **Openness**: `Proprietary`
- **Lock-in vectors**: Google Cloud, no open weights
- **Source**: [DeepMind Research](https://deepmind.google/research/)

#### Newton

- **What it does**: Physics engine co-developed with NVIDIA and Disney Research — aims to provide differentiable physics simulation for training and evaluating world models.
- **Building blocks covered**: [Simulation Engines](building-blocks.md#simulation-engines), [Physics-Informed ML Frameworks](building-blocks.md#physics-informed-ml-frameworks)
- **Key features (functional)**: Differentiable physics, multi-body dynamics, contact simulation
- **Key features (non-functional)**: (to be populated)
- **Competes with**: MuJoCo, PhysX, Genesis World — on differentiable physics simulation
- **Complements**: Genie 3 (physics backbone), Gemini Robotics (sim-to-real)
- **Openness**: (to be populated)
- **Lock-in vectors**: (to be populated)
- **Source**: [DeepMind](https://deepmind.google/research/)

**Implied reference architecture**: Gemini as universal backbone — Gemini Omni provides multimodal reasoning, Genie 3 generates interactive environments for training, Newton handles physics, and Gemini Robotics translates it all into robot actions. Envisions a single model family spanning language, vision, simulation, and control.

**Platform relevance**:

- **Partnership surface**: Newton physics engine (potential open collaboration), Gemini Robotics-ER for industrial inspection
- **Competitive surface**: Full-stack AI platform ambition overlaps broadly with any Physical AI platform
- **What they need from a platform**: Hardware-agnostic deployment (beyond Google Cloud), integration with diverse robot ecosystems, industrial certification

---

### Tesla

**Type**: `Big Tech`
**About**: Applies world model principles at production scale in its Full Self-Driving (FSD) system. Not a standalone world model product, but the largest-scale deployment of world-model-based prediction in production vehicles.

**Solutions**:

#### Full Self-Driving (FSD)

- **What it does**: End-to-end autonomous driving system using Occupancy Networks 2.0 — 3D voxel-based prediction of future occupancy states as a core world model component.
- **Building blocks covered**: [Latent World Models](building-blocks.md#latent-world-models), [Edge AI Inference Runtime](building-blocks.md#edge-ai-inference-runtime)
- **Key features (functional)**: 3D occupancy prediction, end-to-end learned driving, temporal future prediction
- **Key features (non-functional)**: FSD v14 has 10x more parameters than v13; deployed on millions of production vehicles
- **Competes with**: Waymo, GAIA series — on autonomous driving world models
- **Complements**: (fully vertically integrated)
- **Openness**: `Proprietary`
- **Lock-in vectors**: Tesla hardware only, fully closed system
- **Source**: [Tesla AI](https://www.tesla.com/AI)

**Implied reference architecture**: Fully vertical — custom silicon (HW4/5), custom inference stack, custom data engine (fleet-collected video), custom world model (Occupancy Networks), custom planner. No external dependencies or integration points by design.

**Platform relevance**:

- **Partnership surface**: Minimal — Tesla does not partner on AI stack
- **Competitive surface**: Autonomous driving world models
- **What they need from a platform**: Nothing — fully self-contained. Relevant as a benchmark for what production-scale world model deployment looks like.

---

### Siemens

**Type**: `Big Tech`
**About**: Industrial conglomerate building "autonomous digital twins" — AI-driven simulations that optimize manufacturing in real time. Partnership with NVIDIA (CES 2026) to create an "Industrial AI Operating System." First AI-driven adaptive factory in Erlangen, 2026.

**Solutions**:

#### Xcelerator

- **What it does**: Open digital business platform for industrial digital twins — connects IoT data, simulation, and AI for manufacturing optimization, predictive maintenance, and autonomous operations.
- **Building blocks covered**: [Digital Twin Runtime](building-blocks.md#digital-twin-runtime), [Simulation Engines](building-blocks.md#simulation-engines)
- **Key features (functional)**: Industrial IoT integration, CAD/PLM tools, simulation (Simcenter), low-code automation, PepsiCo digital twin reference case
- **Key features (non-functional)**: Cloud and on-prem, industrial-grade reliability
- **Competes with**: Omniverse (digital twins), Eclipse Ditto (open-source), PTC ThingWorx — on industrial digital twin capability
- **Complements**: NVIDIA Omniverse (rendering/physics via partnership), PhysicsNeMo (physics ML)
- **Openness**: `Proprietary` (marketplace with partner apps)
- **Lock-in vectors**: Siemens tool ecosystem (NX, Teamcenter), proprietary data formats, Siemens Cloud
- **Source**: [Xcelerator](https://xcelerator.siemens.com)

**Implied reference architecture**: Industrial AI Operating System built on Xcelerator + NVIDIA Omniverse. Siemens provides domain expertise (manufacturing processes, PLM, MES), NVIDIA provides GPU-accelerated simulation and AI. Digital twins feed autonomous control loops for factory optimization.

**Platform relevance**:

- **Partnership surface**: Industrial domain expertise, manufacturing process knowledge, OT integration
- **Competitive surface**: Industrial digital twins, factory automation AI
- **What they need from a platform**: AI model management for industrial models, safety/certification frameworks, cross-vendor interoperability

---

### Schneider Electric

**Type**: `Big Tech`
**About**: Energy management and industrial automation company deploying AI-driven digital twins for autonomous industrial operations. Targets 80% operational autonomy by 2030 across energy and chemicals verticals.

**Solutions**:

#### EcoStruxure

- **What it does**: IoT-enabled platform for energy management and industrial automation — integrates connected products, edge control, and cloud analytics with AI-driven digital twins.
- **Building blocks covered**: [Digital Twin Runtime](building-blocks.md#digital-twin-runtime), [Edge AI Inference Runtime](building-blocks.md#edge-ai-inference-runtime)
- **Key features (functional)**: AI factory power digital twin (with ETAP on Omniverse), generative AI co-pilot for automation engineering, energy optimization, predictive maintenance
- **Key features (non-functional)**: Industrial-grade, targets 80% operational autonomy by 2030
- **Competes with**: Siemens Xcelerator, Honeywell Forge — on industrial automation and energy management
- **Complements**: NVIDIA Omniverse (rendering/physics), ETAP (power systems)
- **Openness**: `Proprietary`
- **Lock-in vectors**: Schneider hardware ecosystem, proprietary protocols, EcoStruxure platform dependency
- **Source**: [EcoStruxure](https://www.se.com/ww/en/work/campaign/innovation/overview.jsp)

**Implied reference architecture**: Connected products at the edge feeding data to EcoStruxure cloud, with AI digital twins for autonomous decision-making. NVIDIA Omniverse provides simulation backbone for power and process digital twins. Generative AI co-pilot assists human operators during transition to autonomous operations.

**Platform relevance**:

- **Partnership surface**: Energy/utilities domain expertise, OT integration, edge deployment
- **Competitive surface**: Industrial digital twins for energy and process industries
- **What they need from a platform**: AI model lifecycle management, cross-vendor digital twin interoperability, safety certification for autonomous operations

---

## Startups

*Venture-backed companies building Physical AI products*

### AMI Labs

**Type**: `Startup`
**Stage/Scale**: Seed — $1.03B raised (March 2026) at $3.5B pre-money valuation (largest European seed round ever)
**About**: Paris-based startup founded by [Yann LeCun](#yann-lecun) (Chairman) in Jan 2026 after leaving Meta FAIR. Building JEPA-based world models for industrial, robotic, and healthcare applications as an alternative to the LLM paradigm. Offices in Paris, New York, Montreal, and Singapore.

**Key People**: Alex LeBrun (CEO), Laurent Solly (COO, ex-Meta VP Europe), Saining Xie (Chief Science Officer), Pascale Fung (Chief Research & Innovation Officer), Michael Rabbat (VP World Models)

**Focus Areas**: World models, JEPA, autonomous machine intelligence, robotics, industrial AI, healthcare

**Key Work**: Founded Jan 2026; focused on JEPA-based world models for Physical AI

**Collaborations**: NVIDIA (investor), Samsung (investor), Toyota Ventures (investor), Bezos Expeditions (investor)

**Platform relevance**:

- **Partnership surface**: JEPA world models as perception building blocks, potential early adopter of platform infrastructure
- **Competitive surface**: Could build own platform if successful at scale
- **What they need from a platform**: Deployment infrastructure, robot middleware integration, industrial data pipelines

**Links**: [MIT Tech Review announcement](https://www.technologyreview.com/2026/01/22/1131661/yann-lecuns-new-venture-ami-labs/), [TechCrunch $1B raise](https://techcrunch.com/2026/03/09/yann-lecuns-ami-labs-raises-1-03-billion-to-build-world-models/)

---

### Physical Intelligence (pi)

**Type**: `Startup`
**Stage/Scale**: $400M+ raised
**About**: Robotics foundation model company building vision-language-action (VLA) models for general-purpose robot manipulation. Co-founded by [Sergey Levine](#sergey-levine) and [Chelsea Finn](#chelsea-finn). pi0/pi0.5 are policy models (not dynamics predictors) that represent a key consumer of world model outputs.

**Solutions**:

#### pi0 / pi0.5 / pi0.7

- **What it does**: VLA foundation models that translate visual observations and language instructions into dexterous robot actions. pi0.5 enables open-world generalization.
- **Building blocks covered**: [Robot Foundation Models](building-blocks.md#robot-foundation-models)
- **Key features (functional)**: Cross-embodiment transfer, bimanual manipulation, open-world generalization (pi0.5), multi-task learning
- **Key features (non-functional)**: (to be populated)
- **Competes with**: GR00T N1, Gemini Robotics, GEN-1 — on generalist robot policy
- **Complements**: World models (upstream perception), simulation platforms (training)
- **Openness**: `OSS-single-vendor` (via OpenPI)
- **Lock-in vectors**: Minimal — open-source release via OpenPI
- **Source**: [Website](https://www.physicalintelligence.company), [GitHub (OpenPI)](https://github.com/Physical-Intelligence/openpi)

**Platform relevance**:

- **Partnership surface**: VLA models as policy layer, OpenPI as integration point
- **Competitive surface**: Minimal — focused on models, not platforms
- **What they need from a platform**: Sim-to-real pipelines, model serving, robot middleware integration

**Links**: [Website](https://www.physicalintelligence.company), [GitHub (OpenPI)](https://github.com/Physical-Intelligence/openpi)

---

### Wayve

**Type**: `Startup`
**Stage/Scale**: $1.5B raised
**About**: UK-based autonomous driving company that built the GAIA series of generative world models (GAIA-1/2/3, 9B-15B params) for AV development. Deploying robotaxi service with Uber/Nissan (Tokyo pilot, late 2026). [Yann LeCun](#yann-lecun) is an investor.

**Solutions**:

#### GAIA Series

- **What it does**: Generative world models for autonomous driving — generates realistic driving scenarios for training and evaluating end-to-end driving systems.
- **Building blocks covered**: [Video Generation / Prediction Models](building-blocks.md#video-generation--prediction-models), [Sim-to-Real Transfer Pipeline](building-blocks.md#sim-to-real-transfer-pipeline)
- **Key features (functional)**: GAIA-1 (2023), GAIA-2 (2024), GAIA-3 (Dec 2025, 15B params, driving system evaluation), controllable scenario generation
- **Key features (non-functional)**: 9B-15B parameters, purpose-built for AV evaluation
- **Competes with**: Cosmos, Genie 3 — on driving world simulation
- **Complements**: End-to-end driving policies (downstream consumer)
- **Openness**: `Proprietary`
- **Lock-in vectors**: Wayve driving stack dependency
- **Source**: [Research](https://wayve.ai/thinking/)

**Collaborations**: Uber, Nissan (robotaxi deployment), [Yann LeCun](#yann-lecun) (investor)

**Links**: [Website](https://wayve.ai), [Research](https://wayve.ai/thinking/)

---

### World Labs

**Type**: `Startup`
**Stage/Scale**: (to be researched)
**About**: Founded by [Fei-Fei Li](#fei-fei-li) to pursue "Spatial Intelligence" as the scaffolding for cognition. Targeting VFX pre-visualization, architectural design, and synthetic data generation for robot training.

**Solutions**:

#### Marble

- **What it does**: Reconstructs persistent 3D worlds from multimodal inputs (text, images, 360-degree panoramas) with human-AI co-creation via "Chisel" feature.
- **Building blocks covered**: [Simulation Engines](building-blocks.md#simulation-engines), [Video Generation / Prediction Models](building-blocks.md#video-generation--prediction-models)
- **Key features (functional)**: Multimodal 3D world reconstruction, persistent worlds, Chisel (interactive 3D editing by humans before AI visual fill)
- **Key features (non-functional)**: (to be populated)
- **Competes with**: Genie 3 — on 3D world generation from prompts
- **Complements**: Robot training pipelines (synthetic 3D data)
- **Openness**: `Proprietary`
- **Lock-in vectors**: Proprietary model and platform
- **Source**: [Marble Blog](https://www.worldlabs.ai/blog/marble-world-model)

**Collaborations**: [Stanford](#stanford-svl--sail) (via [Fei-Fei Li](#fei-fei-li))

**Links**: [Website](https://www.worldlabs.ai/), [Marble Blog](https://www.worldlabs.ai/blog/marble-world-model)

---

### Figure AI

**Type**: `Startup`
**Stage/Scale**: (to be researched)
**About**: Humanoid robotics company building general-purpose humanoid robots (Figure 01, Figure 02) for manufacturing and logistics. Uses visuomotor transformers combining conversational AI with bimanual manipulation. Adopter of NVIDIA Cosmos and GR00T N1.

**Focus Areas**: Humanoid robotics, visuomotor transformers, bimanual manipulation, manufacturing automation

**Key Work**: Figure 01/02 humanoid robots, conversational AI + manipulation integration

**Collaborations**: [NVIDIA](#nvidia) (Cosmos, GR00T N1 adopter), OpenAI (conversational AI integration)

**Links**: [Website](https://www.figure.ai/)

---

### Generalist AI

**Type**: `Startup`
**Stage/Scale**: (to be researched)
**About**: Robotics foundation model company pursuing a "native embodied" approach — training directly on physical interaction data from wearable devices rather than internet images or teleoperation. Represents an alternative paradigm to VLAs (internet pretraining) and WAMs (video diffusion).

**Solutions**:

#### GEN-1

- **What it does**: Native embodied foundation model trained on 500K+ hours of human movement data captured via low-cost "data hands" (UMIs) for production manipulation tasks.
- **Building blocks covered**: [Robot Foundation Models](building-blocks.md#robot-foundation-models), [Data Annotation & Curation for Physical AI](building-blocks.md#data-annotation--curation-for-physical-ai)
- **Key features (functional)**: Native embodied training (not internet pretraining), wearable data collection, production manipulation
- **Key features (non-functional)**: 99% success rates on production tasks, 3x faster than SOTA (GEN-1, April 2026)
- **Competes with**: pi0/pi0.5, GR00T N1, Gemini Robotics — on robot manipulation
- **Complements**: Wearable data collection devices (data engine)
- **Openness**: `Proprietary`
- **Lock-in vectors**: Proprietary data collection pipeline, closed model
- **Source**: [GEN-1 Blog](https://generalistai.com/blog/apr-02-2026-GEN-1)

**Links**: [Website](https://generalistai.com/), [GEN-1 Blog](https://generalistai.com/blog/apr-02-2026-GEN-1)

---

### Genesis AI

**Type**: `Startup`
**Stage/Scale**: Seed — $105M raised (one of the largest French seeds, matching Mistral's). Backers: Eclipse, Khosla Ventures, Bpifrance, Eric Schmidt, Daniela Rus, Vladlen Koltun
**About**: Full-stack robotics company building general-purpose robots with human-level physical manipulation. Founded Dec 2024 by Zhou Xian (PhD CMU) and Theophile Gervet (ex-Mistral). Offices in Paris, San Carlos CA, and London. Owns the full stack: foundation model (GENE), dexterous hands, simulation (Genesis World), and data engine (sensor gloves + egocentric video).

**Solutions**:

#### Genesis World

- **What it does**: Open-source multi-physics simulation platform with cross-platform compilation and path-traced rendering.
- **Building blocks covered**: [Simulation Engines](building-blocks.md#simulation-engines), [Sim-to-Real Transfer Pipeline](building-blocks.md#sim-to-real-transfer-pipeline)
- **Key features (functional)**: Multi-physics simulation, Quadrants compiler (CUDA, ROCm, Metal, Vulkan, x86/ARM64), Nyx renderer (path-traced, noise-free 1080p in <4ms)
- **Key features (non-functional)**: 29K GitHub stars, Apache 2.0 license, cross-platform
- **Competes with**: Isaac Sim, MuJoCo, Gazebo — on physics simulation for robotics
- **Complements**: GENE (training environment), robot hardware (sim-to-real)
- **Openness**: `OSS-single-vendor`
- **Lock-in vectors**: Minimal — Apache 2.0, cross-platform
- **Source**: [GitHub](https://github.com/Genesis-Embodied-AI)

#### GENE

- **What it does**: Flow-matching foundation model for dexterous manipulation — trained on proprietary data from sensor gloves and egocentric video.
- **Building blocks covered**: [Robot Foundation Models](building-blocks.md#robot-foundation-models)
- **Key features (functional)**: GENE-26.5 (May 2026): 20-step cooking, Rubik's Cube solving, lab automation
- **Key features (non-functional)**: Human-level manipulation benchmarks
- **Competes with**: pi0/pi0.5, GR00T N1, GEN-1 — on dexterous manipulation
- **Complements**: Genesis World (simulation training), custom dexterous hands (hardware)
- **Openness**: `Proprietary`
- **Lock-in vectors**: Proprietary data pipeline, Genesis hardware ecosystem
- **Source**: [Blog](https://www.genesis.ai/blog/gene-26-5-advancing-robotic-manipulation-to-human-level)

**Links**: [Website](https://www.genesis.ai), [GitHub](https://github.com/Genesis-Embodied-AI)

---

### Periodic Labs

**Type**: `Startup`
**Stage/Scale**: Seed — $300M raised (Oct 2025). Led by Andreessen Horowitz; backed by Jeff Bezos, Eric Schmidt, Jeff Dean, NVentures
**About**: Building autonomous "AI scientists" — closed-loop self-driving laboratories where AI agents propose hypotheses, run physical experiments, and analyze results with minimal human intervention. Founders William Fedus and Ekin Dogus Cubuk cite contributions to ChatGPT, GNoME, and MatterGen.

**Focus Areas**: Autonomous science, self-driving labs, materials discovery, physical AI for scientific research

**Key Work**: AI scientist platform for materials discovery (high-temperature superconductors, chip designs)

**Links**: [Website](https://periodic.com/)

---

### Medra

**Type**: `Startup`
**Stage/Scale**: $52M raised
**About**: Building autonomous self-driving labs for drug discovery — integrating AI with robotic laboratory automation in closed-loop systems that design, execute, and learn from biological experiments.

**Focus Areas**: Autonomous drug discovery, self-driving labs, laboratory robotics, closed-loop experimentation

**Key Work**: Medra Platform (autonomous robotic system for biological experiments), Genentech partnership

**Collaborations**: Genentech (drug discovery partnership)

**Links**: [Website](https://www.medra.ai/)

---

### Robbyant (Ant Group)

**Type**: `Startup`
**Stage/Scale**: Division of Ant Group (Alibaba affiliate)
**About**: Embodied AI division of Ant Group building a comprehensive foundation model stack for robotics. The LingBot family covers spatial perception, VLAs, world models, and video-action models.

**Solutions**:

#### LingBot Family

- **What it does**: Comprehensive foundation model stack: LingBot-Depth (spatial perception), LingBot-VLA (vision-language-action), LingBot-World (interactive world model), LingBot-VA (video-action model).
- **Building blocks covered**: [Robot Foundation Models](building-blocks.md#robot-foundation-models), [Latent World Models](building-blocks.md#latent-world-models), [Video Generation / Prediction Models](building-blocks.md#video-generation--prediction-models)
- **Key features (functional)**: LingBot-VA (autoregressive video-action, 20% better than pi0.5), LingBot-World (interactive simulator), LingBot-Depth (spatial perception), LingBot-Map (streaming 3D reconstruction)
- **Key features (non-functional)**: LingBot-VA: 98.5% on LIBERO benchmark (industry record); LingBot-World: 16 FPS, sub-second interaction latency
- **Competes with**: pi0/pi0.5, GR00T N1, Cosmos — across multiple building blocks
- **Complements**: vLLM-Omni community (LingBot-VA targeted for P1 integration)
- **Openness**: `OSS-single-vendor` (partially open)
- **Lock-in vectors**: Ant Group ecosystem, partially open-source
- **Source**: [GitHub](https://github.com/Robbyant), [LingBot-VA](https://github.com/Robbyant/lingbot-va)

**Links**: [Website](https://technology.robbyant.com/), [GitHub](https://github.com/Robbyant)

---

### Logical Intelligence

**Type**: `Startup`
**Stage/Scale**: (to be researched). Investors: Pantera Capital
**About**: Building Energy-Based Reasoning Models (EBRMs) as an alternative to LLMs for critical systems. [Yann LeCun](#yann-lecun) serves as Founding Chair of the Technical Research Board, connecting directly to the JEPA/EBM research lineage.

**Solutions**:

#### Kona

- **What it does**: Energy-based reasoning model using energy minimization rather than next-token prediction — operates in continuous latent space with non-autoregressive trace generation for mathematical and logical reasoning.
- **Building blocks covered**: [Latent World Models](building-blocks.md#latent-world-models)
- **Key features (functional)**: Energy-based reasoning, constraint satisfaction, mathematical verification, deterministic outputs for critical systems
- **Key features (non-functional)**: (to be populated)
- **Competes with**: LLM-based reasoning (GPT, Claude, Gemini) — on deterministic reasoning for critical systems
- **Complements**: Aleph (verified coding AI, near-perfect PutnamBench score)
- **Openness**: `Proprietary`
- **Lock-in vectors**: Proprietary model and API
- **Source**: [Kona Technical](https://logicalintelligence.com/kona-ebms-energy-based-models)

**Links**: [Website](https://logicalintelligence.com/), [Blog](https://logicalintelligence.com/blog/energy-based-models-for-reasoning)

---

### Verses AI

**Type**: `Startup`
**Stage/Scale**: (to be researched)
**About**: Pursues a biology-inspired approach to world models based on Active Inference and the Free Energy Principle. Key differentiator: creates a hierarchy of intelligent agents within a single robot body — every joint is an agent with its own local understanding.

**Solutions**:

#### AXIOM

- **What it does**: Active Inference architecture (Active eXpanding Inference with Object-centric Models) that unifies perception, planning, and control in a single generative model where agents actively seek to resolve epistemic uncertainty.
- **Building blocks covered**: [Latent World Models](building-blocks.md#latent-world-models), [Robot Foundation Models](building-blocks.md#robot-foundation-models)
- **Key features (functional)**: Hierarchical agent architecture (per-joint agents), active uncertainty resolution, object-centric modeling, recovery from unexpected problems without retraining
- **Key features (non-functional)**: (to be populated)
- **Competes with**: Standard VLA/world model approaches — on adaptive, uncertainty-aware control
- **Complements**: Karl Friston's Free Energy Principle (theoretical foundation)
- **Openness**: (to be populated)
- **Lock-in vectors**: (to be populated)
- **Source**: [Research](https://www.verses.ai/research)

**Collaborations**: Karl Friston (scientific advisor, Free Energy Principle originator)

**Links**: [Website](https://www.verses.ai/), [Research](https://www.verses.ai/research)

---

### Pathway

**Type**: `Startup`
**Stage/Scale**: (to be researched)
**About**: Company behind the Baby Dragon Hatchling (BDH) architecture — a biologically-inspired alternative to transformers demonstrating that scale-free spiking networks with Hebbian learning can match GPT-2 performance while providing built-in interpretability.

**Solutions**:

#### BDH (Baby Dragon Hatchling)

- **What it does**: Biologically-inspired language model using scale-free spiking networks with Hebbian learning as an alternative to transformers.
- **Building blocks covered**: [Latent World Models](building-blocks.md#latent-world-models)
- **Key features (functional)**: Scale-free spiking network, Hebbian learning, neuroscience-grounded interpretability, matches GPT-2 performance
- **Key features (non-functional)**: Open-source implementation
- **Competes with**: Transformers (GPT, Llama) — on interpretable language modeling
- **Complements**: Neuroscience research (biological plausibility)
- **Openness**: `OSS-single-vendor`
- **Lock-in vectors**: Minimal — open-source
- **Source**: [GitHub](https://github.com/pathwaycom/bdh)

**Collaborations**: [Adrian Kosowski](#adrian-kosowski) (lead researcher), University of Wroclaw

**Links**: [GitHub](https://github.com/pathwaycom/bdh), [Website](https://pathway.com)

---

### Safe Superintelligence Inc. (SSI)

**Type**: `Startup`
**Stage/Scale**: $3B raised at $32B valuation (as of April 2025)
**About**: Israeli-American AI research company co-founded by [Ilya Sutskever](#ilya-sutskever), Daniel Gross, and Daniel Levy in June 2024. Single-mission company focused solely on building safe superintelligence — no products, no revenue, pure research. Sutskever advocates a "post-scaling" paradigm, betting on JEPA-style architectures and continual learning.

**Focus Areas**: Safe superintelligence, continual learning, generalization, alignment-as-generalization

**Key Work**: No publications (extremely secretive); Sutskever's public statements point to JEPA-style architectures, continual learning, and the "Big World Hypothesis" as research directions

**Collaborations**: Google Cloud (TPU access partnership, April 2025)

**Links**: [Website](https://ssi.inc/), [Wikipedia](https://en.wikipedia.org/wiki/Safe_Superintelligence_Inc.)

---

### OpenAI

**Type**: `Startup`
**Stage/Scale**: (to be researched)
**About**: Built Sora/Sora 2, diffusion transformer models for video generation positioned as "teaching AI to understand and simulate the physical world." Illustrates both the ambition and the commercial challenge of pixel-space world simulation at scale.

**Solutions**:

#### Sora

- **What it does**: Diffusion transformer for video generation — generates realistic video from text/image prompts with physical world simulation capabilities. Standalone product discontinued March 2026 due to unsustainable compute costs; model continues to exist.
- **Building blocks covered**: [Video Generation / Prediction Models](building-blocks.md#video-generation--prediction-models)
- **Key features (functional)**: Text-to-video generation, image-to-video, physics-aware generation (Sora 2 improved coherence)
- **Key features (non-functional)**: Sora 2 (Sept 2025) improved physics; product discontinued March 2026
- **Competes with**: Cosmos, Genie 3, Veo — on video generation
- **Complements**: (standalone, no integration ecosystem)
- **Openness**: `Proprietary`
- **Lock-in vectors**: OpenAI API dependency (while product existed)
- **Source**: [Website](https://openai.com)

**Links**: [Website](https://openai.com), [Research](https://openai.com/research)

---

## OSS Communities

*Open-source communities and foundations governing key Physical AI infrastructure*

### Open Robotics / OSRA

**Type**: `OSS Community`
**About**: Governs ROS2 (Robot Operating System 2) and Gazebo — the de facto standard middleware and simulation platform for robotics research and increasingly for production deployments. ROS2 provides the publish-subscribe communication layer, hardware abstraction, and tool ecosystem that most robot software builds on. Gazebo provides physics-based simulation integrated with ROS2.

**Focus Areas**: Robot middleware, simulation, hardware abstraction, interoperability standards

**Key Projects**:

- **ROS2**: Middleware framework — DDS-based communication, lifecycle management, real-time capable. Building block: [Robot Middleware](building-blocks.md#robot-middleware)
- **Gazebo**: Multi-physics simulation with ROS2 integration, sensor simulation, environment modeling. Building block: [Simulation Engines](building-blocks.md#simulation-engines)

**Openness**: `OSS-community` (Apache 2.0)

**Platform relevance**:

- **Partnership surface**: ROS2 is the integration layer most robot platforms must support; Gazebo is baseline simulation
- **Competitive surface**: Minimal — community-governed, not commercially competitive
- **What they need from a platform**: Better cloud deployment, fleet management, model serving integration, real-time performance improvements

**Links**: [ROS2](https://www.ros.org/), [Gazebo](https://gazebosim.org/), [GitHub](https://github.com/ros2)

---

### vLLM Community

**Type**: `OSS Community`
**About**: Community developing vLLM — the leading open-source inference engine for large language models — and vLLM-Omni, which extends it to serve multimodal and Physical AI models (world models, VLAs, video-action models). Relevant as the emerging model serving layer for Physical AI workloads.

**Focus Areas**: Model serving, inference optimization, multimodal serving, Physical AI model deployment

**Key Projects**:

- **vLLM**: High-throughput LLM inference engine with PagedAttention. Building block: [Model Serving for Physical AI](building-blocks.md#model-serving-for-physical-ai)
- **vLLM-Omni**: Extension for multimodal and Physical AI model serving. Building block: [Model Serving for Physical AI](building-blocks.md#model-serving-for-physical-ai)

**Openness**: `OSS-community` (Apache 2.0)

**Platform relevance**:

- **Partnership surface**: Model serving backbone for Physical AI platforms, integration with robot middleware
- **Competitive surface**: Minimal — open-source serving layer
- **What they need from a platform**: Real-time serving guarantees, edge deployment support, integration with robot middleware and simulation

**Links**: [GitHub (vLLM)](https://github.com/vllm-project/vllm), [GitHub (vLLM-Omni)](https://github.com/vllm-project/vllm-omni)

---

### HuggingFace

**Type**: `OSS Community`
**About**: AI model hub and open-source ecosystem provider. Increasingly relevant to Physical AI through LeRobot (open-source robot learning framework), model hosting for robot foundation models, and datasets for embodied AI.

**Focus Areas**: Model hub, open-source ML tooling, robot learning, datasets

**Key Projects**:

- **LeRobot**: Open-source robot learning framework — standardized training, evaluation, and deployment of robot policies. Building block: [Robot Foundation Models](building-blocks.md#robot-foundation-models), [Post-Training / Fine-Tuning Pipeline](building-blocks.md#post-training--fine-tuning-pipeline)
- **Model Hub**: Hosting for world models, VLAs, and robot foundation models
- **Datasets**: Hosting for robot demonstration datasets, simulation data

**Openness**: `OSS-community` (Apache 2.0 for tools; hub is a mix)

**Platform relevance**:

- **Partnership surface**: Model distribution, dataset hosting, LeRobot as training framework
- **Competitive surface**: Model hub could compete with platform model management
- **What they need from a platform**: Deployment infrastructure beyond hosting, real-time serving, robot hardware integration

**Links**: [Website](https://huggingface.co/), [LeRobot](https://github.com/huggingface/lerobot)

---

### Eclipse Foundation

**Type**: `OSS Community`
**About**: Open-source foundation governing Eclipse Ditto — a framework for digital twins in IoT and industrial applications. Provides vendor-neutral digital twin infrastructure as an alternative to proprietary platforms.

**Focus Areas**: Digital twins, IoT, industrial open-source

**Key Projects**:

- **Eclipse Ditto**: Digital twin framework for IoT — manages digital representations of physical devices with APIs for state management, search, and change notification. Building block: [Digital Twin Runtime](building-blocks.md#digital-twin-runtime)

**Openness**: `OSS-community` (Eclipse Public License)

**Platform relevance**:

- **Partnership surface**: Vendor-neutral digital twin layer, integration with industrial IoT
- **Competitive surface**: Minimal — community-governed alternative to proprietary digital twins
- **What they need from a platform**: AI integration (current focus is state management, not AI), physics simulation, scale beyond IoT to full Physical AI twins

**Links**: [Eclipse Ditto](https://www.eclipse.org/ditto/), [GitHub](https://github.com/eclipse-ditto/ditto)

---

## Research Labs

*Universities and research institutions advancing Physical AI foundations*

### Meta FAIR / AMI Labs

**About**: Meta's Fundamental AI Research lab developed the JEPA ecosystem. Post-LeCun departure (Jan 2026), FAIR continues JEPA research while AMI Labs pursues commercial applications. The Galilai group (Randall Balestriero) leads theoretical foundations work.

**Focus Areas**: JEPA architectures, self-supervised learning, energy-based models, world models, identifiability theory

**Key Work**: I-JEPA, V-JEPA, V-JEPA 2, VL-JEPA, EB-JEPA, VICReg, LeJEPA, SIGReg, LeWorldModel, identifiability theory

**Key People**:

#### Yann LeCun

Turing Award laureate (2018) and originator of JEPA and the energy-based model framework. His 2022 position paper "A Path Towards Autonomous Machine Intelligence" laid out the JEPA vision. Former Chief AI Scientist at Meta FAIR; founded [AMI Labs](#ami-labs) in Jan 2026.

- **Focus**: JEPA, self-supervised learning, energy-based models, world models
- **Key Work**: I-JEPA, V-JEPA, V-JEPA 2, VL-JEPA, EB-JEPA; "A Path Towards Autonomous Machine Intelligence" (2022)
- **Links**: [Google Scholar](https://scholar.google.com/citations?user=WLN3QrAAAAAJ), [Twitter](https://twitter.com/ylecun)

#### Adrien Bardes

Research Scientist at Meta FAIR and key architect of the JEPA ecosystem. Creator of VICReg — the variance-invariance-covariance regularization that solved collapse prevention for joint-embedding architectures. Co-author on V-JEPA 2, V-JEPA 2.1, VL-JEPA, JEPA-WMs ablation, and Hierarchical World Models.

- **Focus**: Self-supervised learning, JEPA, VICReg, world models for planning
- **Key Work**: VICReg (ICLR 2022), VICRegL (NeurIPS 2022), V-JEPA 2, VL-JEPA, Hierarchical Planning with Latent World Models
- **Links**: [Google Scholar](https://scholar.google.com/citations?user=SvRU8F8AAAAJ), [Website](https://adrien987k.github.io/), [GitHub](https://github.com/Adrien987k)

#### Randall Balestriero

Research Scientist at Meta FAIR leading the Galilai group. Originated LeJEPA and SIGReg — a Gaussian regularization approach replacing the EMA teacher-student paradigm with explicit distributional constraints. Co-developed LeWorldModel, the first JEPA trained end-to-end from raw pixels with only two loss terms. Proved (with Klindt) that Gaussian regularization is necessary and sufficient for linear identifiability in JEPA architectures.

- **Focus**: LeJEPA, SIGReg, identifiability theory, self-supervised learning
- **Key Work**: LeJEPA (2025), SIGReg, LeWorldModel (2026-03), identifiability theory (2026-05), Le MuMo JEPA (2026-03)
- **Links**: [Google Scholar](https://scholar.google.com/citations?user=osi2F5IAAAAJ), [GitHub](https://github.com/galilai-group)

**Links**: [FAIR GitHub](https://github.com/facebookresearch), [FAIR Blog](https://ai.meta.com/blog/)

---

### MIT CSAIL

**About**: MIT's Computer Science and Artificial Intelligence Laboratory hosts the Embodied Intelligence community, bringing together researchers working on physically grounded AI. Key groups: Computational Cognitive Science (commonsense reasoning, CLEVRER benchmark) and Distributed Robotics Laboratory (liquid neural networks, VISTA simulation).

**Focus Areas**: Embodied intelligence, commonsense reasoning, intuitive physics, distributed robotics, autonomous driving simulation

**Key Work**: CLEVRER benchmark (counterfactual video reasoning), liquid neural networks, VISTA simulation, Embodied Intelligence Summit

**Key People**:

#### Josh Tenenbaum

Professor studying how humans acquire commonsense understanding of the physical and social world from remarkably little data. His work on intuitive physics and probabilistic programs of thought has directly influenced world model benchmarks and evaluation methodology.

- **Focus**: Commonsense reasoning, intuitive physics, probabilistic programming, cognitive science
- **Key Work**: CLEVRER benchmark, BabyAI, probabilistic programs of thought, Bayesian models of cognition
- **Links**: [Google Scholar](https://scholar.google.com/citations?user=rRJ9wTJMUB8C), [Homepage](https://cocosci.mit.edu/)

#### Daniela Rus

Director of MIT CSAIL and leader of the Distributed Robotics Laboratory. Pioneered liquid neural networks and VISTA simulations for safe autonomous driving training. Her "Science of Autonomy" research focuses on scalable multi-robot systems.

- **Focus**: Distributed robotics, liquid neural networks, autonomous driving simulation, science of autonomy
- **Key Work**: Liquid neural networks, VISTA simulation platform, distributed robotics systems
- **Links**: [Google Scholar](https://scholar.google.com/citations?user=910z20QAAAAJ), [Homepage](https://www.csail.mit.edu/person/daniela-rus)

**Links**: [Website](https://www.csail.mit.edu/), [Embodied Intelligence](https://www.csail.mit.edu/research/embodied-intelligence-community-research)

---

### Stanford SVL / SAIL

**About**: Stanford's Vision and Learning Lab (SVL) and AI Lab (SAIL) develop methods for robot perception in real-world variability. Key research includes "Motion Intelligence" for humanoid robots and the "Common Ground" problem — how to create stable shared representations between humans and AI systems.

**Focus Areas**: Spatial intelligence, motion intelligence, common ground, humanoid robotics, visual understanding

**Key Work**: Motion Intelligence for humanoids, Common Ground research, Stanford HAI AI Index Report

**Key People**:

#### Fei-Fei Li

Stanford professor and co-director of Stanford HAI. Founded [World Labs](#world-labs) to pursue "Spatial Intelligence." Creator of ImageNet. Pioneered the Marble model for persistent 3D world reconstruction.

- **Focus**: Spatial intelligence, 3D world models, computer vision
- **Key Work**: ImageNet (2009), [World Labs](#world-labs) (founded 2024), Marble, Stanford HAI (co-director)
- **Links**: [Google Scholar](https://scholar.google.com/citations?user=rDfyQnIAAAAJ), [Homepage](https://profiles.stanford.edu/fei-fei-li)

#### Chelsea Finn

Associate Professor, co-founder of [Physical Intelligence](#physical-intelligence-pi). Leads the IRIS lab (Intelligence through Robotic Interaction at Scale). Pioneer in meta-learning for robotics and few-shot adaptation.

- **Focus**: Robot learning, meta-learning, world models for manipulation, few-shot adaptation
- **Key Work**: MAML, Ctrl-World, RoboReward, co-founder of [Physical Intelligence](#physical-intelligence-pi)
- **Links**: [Google Scholar](https://scholar.google.com/citations?user=vfPE6hgAAAAJ), [Homepage](https://ai.stanford.edu/~cbfinn/)

**Links**: [SVL](https://svl.stanford.edu/), [SAIL](https://ai.stanford.edu/), [HAI](https://hai.stanford.edu/)

---

### UC Berkeley RAIL

**About**: The Robotic AI and Learning Lab argues that robots will eventually outpace LLMs in data because they can autonomously collect physical experience cheaply. Pioneered offline RL and "extreme" robot designs that test architectures without hand-engineered crutches. Directly tied to [Physical Intelligence](#physical-intelligence-pi).

**Focus Areas**: Offline RL, robot learning, model-based RL, autonomous data collection, bimanual manipulation

**Key Work**: Offline RL methods, pi0/pi0.5 (via Physical Intelligence), extreme robot manipulation, "World Model for Robot Learning" survey (2026)

**Key People**:

#### Sergey Levine

Professor and co-founder of [Physical Intelligence](#physical-intelligence-pi). Argues robots will have a data advantage over language models. Pioneered offline RL methods for safe deployment.

- **Focus**: Offline RL, robot learning, model-based RL, autonomous data collection
- **Key Work**: Offline RL, pi0/pi0.5 (via Physical Intelligence), extreme robot designs
- **Links**: [Google Scholar](https://scholar.google.com/citations?user=8R35rCwAAAAJ), [Homepage](https://people.eecs.berkeley.edu/~svlevine/)

#### Pieter Abbeel

Professor, co-founder of Covariant (robot learning for warehouses). Co-authored the "World Model for Robot Learning" survey (2026) unifying the fragmented world model literature for robotics.

- **Focus**: Robot learning, deep RL, sim-to-real transfer, world models for robotics
- **Key Work**: World Model for Robot Learning survey (2026, with Jitendra Malik), Covariant (co-founder)
- **Links**: [Google Scholar](https://scholar.google.com/citations?user=X4Qth8YAAAAJ), [Homepage](https://people.eecs.berkeley.edu/~pabbeel/)

#### Jitendra Malik

Professor and Research Director at Meta. Pioneer in computer vision spanning four decades. Co-authored the "World Model for Robot Learning" survey (2026) bridging vision, world models, and robot policy learning.

- **Focus**: Computer vision, 3D understanding, embodied perception, world models for robotics
- **Key Work**: World Model for Robot Learning survey (2026, with Pieter Abbeel), Mesh R-CNN
- **Links**: [Google Scholar](https://scholar.google.com/citations?user=oY9R5YQAAAAJ), [Homepage](https://people.eecs.berkeley.edu/~malik/)

**Links**: [Website](https://rail.eecs.berkeley.edu/)

---

### CMU Robotics Institute

**About**: Carnegie Mellon's Robotics Institute has been a birthplace of autonomous vehicle technology since 1984. Current research includes "World Modeling" (temporally abstract world models from offline demonstrations), "Physical Perception" using physics as meta-supervision, and error propagation analysis for navigation.

**Focus Areas**: World modeling, field robotics, autonomous vehicles, physical perception, error propagation

**Key Work**: World Modeling archive, temporally abstract world models, physical perception, AV technology

**Key People**:

#### Shubham Tulsiani

Assistant Professor focusing on "Physical Perception" — leveraging the laws of the physical world as meta-supervisory signals to reduce reliance on human annotation. Enables robots to build 3D understanding from minimal labeled data.

- **Focus**: Physical perception, 3D understanding, self-supervised learning from physics
- **Key Work**: Physical perception research, physics-as-supervision for 3D understanding
- **Links**: [Google Scholar](https://scholar.google.com/citations?user=gPyFsMQAAAAJ), [Homepage](https://shubhtuls.github.io/)

#### Alonzo Kelly

Professor specializing in how errors accumulate and propagate in world models used for robot navigation. Research on odometry and triangulation error propagation is foundational to understanding world model prediction degradation.

- **Focus**: Error propagation, odometry, triangulation, mobile robotics, field robotics
- **Key Work**: Error propagation analysis for navigation systems, mobile robot localization
- **Links**: [Homepage](https://www.ri.cmu.edu/ri-faculty/alonzo-kelly/)

**Links**: [Website](https://www.ri.cmu.edu/), [World Modeling](https://www.ri.cmu.edu/research-topic/world-modeling/)

---

### Oxford OATML

**About**: The Oxford Applied and Theoretical Machine Learning group specializes in uncertainty quantification (UQ) for deep learning and world models. Their "Deep Ignorance" framework addresses when AI systems should recognize they lack sufficient knowledge to act — critical for safety in world-model-driven autonomous systems.

**Focus Areas**: Uncertainty quantification, Bayesian deep learning, verification, safe AI, autonomous discovery

**Key Work**: Bayesian UQ for LLMs and world models, step-wise verification for reasoning, Deep Ignorance framework

**Key People**:

#### Yarin Gal

Associate Professor and head of OATML. Specializes in uncertainty quantification applying Bayesian principles to build reliable verification for reasoning models and autonomous systems.

- **Focus**: Uncertainty quantification, Bayesian deep learning, safe AI, verification
- **Key Work**: Concrete Dropout, Bayesian deep learning framework, uncertainty-aware verification
- **Links**: [Google Scholar](https://scholar.google.com/citations?user=H2BVqkwAAAAJ), [Homepage](https://www.cs.ox.ac.uk/people/yarin.gal/website/)

**Links**: [Website](https://oatml.cs.ox.ac.uk/), [Blog](https://oatml.cs.ox.ac.uk/blog.html)

---

### Mila

**About**: Quebec AI Institute, founded by Yoshua Bengio. Focuses on "System 2" deep learning — architectures that move beyond statistical correlation to causal reasoning. Bengio's "Scientist AI" proposal envisions non-agentic world models for understanding rather than acting.

**Focus Areas**: System 2 thinking, causal reasoning, scientific AI, safe AGI, compositional learning

**Key Work**: GFlowNets, System 2 deep learning, Scientist AI proposal

**Key People**:

#### Yoshua Bengio

Turing Award laureate (2018), founder and scientific director of Mila. Advocates for "System 2" deep learning and causal reasoning. His "Scientist AI" proposal envisions non-agentic world models focused on understanding, targeting "Scientific and Safe" AGI.

- **Focus**: System 2 thinking, causal reasoning, scientific AI, world models for understanding
- **Key Work**: "Scientist AI" proposal, GFlowNets, System 2 deep learning position papers
- **Links**: [Google Scholar](https://scholar.google.com/citations?user=kukA0LcAAAAJ), [Homepage](https://yoshuabengio.org/)

**Links**: [Website](https://mila.quebec/), [Research](https://mila.quebec/en/publications/)

---

### Additional Researchers

*Key researchers not primarily affiliated with the labs above*

#### Ilya Sutskever

Co-founder and CEO of [Safe Superintelligence Inc. (SSI)](#safe-superintelligence-inc-ssi). Former chief scientist of OpenAI; co-inventor of AlexNet. Advocates a "post-scaling" paradigm shift — new learning methods over bigger models — with emphasis on continual learning, generalization, and JEPA-style architectures.

- **Focus**: Safe superintelligence, continual learning, generalization, post-scaling paradigm
- **Key Work**: AlexNet (2012), sequence-to-sequence learning (2014), co-founded OpenAI (2015), co-founded SSI (2024); "Big World Hypothesis"
- **Links**: [Google Scholar](https://scholar.google.com/citations?user=x04W_mMAAAAJ&hl=en), [Twitter](https://twitter.com/ilyasut), [Homepage](https://www.cs.toronto.edu/~ilya/)

#### Adrian Kosowski

Lead researcher behind the BDH architecture at [Pathway](#pathway). Originated the biologically-inspired LLM design bridging transformers and neuroscience models.

- **Focus**: BDH, biologically-inspired architectures, spiking neural networks, interpretability
- **Key Work**: "The Dragon Hatchling: The Missing Link between the Transformer and Models of the Brain" (2025-09)
- **Links**: [GitHub](https://github.com/pathwaycom/bdh)

#### Yair Carmon

ML researcher at [SSI](#safe-superintelligence-inc-ssi) (Tel Aviv office). PhD from Stanford; background in adversarial robustness and optimization.

- **Focus**: Machine learning, adversarial robustness, optimization
- **Key Work**: Research at SSI (details undisclosed)
- **Links**: [Google Scholar](https://scholar.google.com/citations?user=LyA_iI0AAAAJ)

#### Demis Hassabis

CEO of [Google DeepMind](#google-deepmind), Nobel Prize in Chemistry (2024, with John Jumper for AlphaFold). Publicly frames world models as the critical next step toward a universal AI assistant — plans to extend Gemini into a world model capable of planning and simulating physical dynamics.

- **Focus**: AGI, world models as path to universal AI, physics simulation, scientific discovery
- **Key Work**: AlphaGo/AlphaZero, AlphaFold (Nobel Prize 2024), Genie 3, Gemini, vision for Gemini as world model
- **Links**: [Google Scholar](https://scholar.google.com/citations?user=dYpPMQEAAAAJ), [Homepage](https://www.demishassabis.com/)

---

**Note**: Only includes seminal contributors and recognized thought leaders. Each entry follows the ecosystem-entry template from `templates/ecosystem-entry.md`. Solution entries follow `templates/solution-entry.md`.
