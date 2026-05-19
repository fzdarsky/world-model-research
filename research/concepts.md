# Key Concepts in World Models Research

> Deep dives into fundamental concepts underlying AI world models

**Last Updated**: 2026-05-18
**Last Synthesized**: 2026-05-18

---

## JEPA (Joint-Embedding Predictive Architecture)

### Overview

Joint-Embedding Predictive Architecture is Yann LeCun's framework for self-supervised learning that learns representations by predicting in an abstract representation space rather than pixel space. Originated in LeCun's 2022 position paper "A Path Towards Autonomous Machine Intelligence." Core idea: an encoder maps inputs to embeddings, a predictor maps context embeddings to target embeddings, and a target encoder (often EMA-updated) provides training signal — all without generating pixels.

### Key Technical Details

**Core Components** (per the JEPA Tutorial, Monemi et al. 2025):

1. **Context-target generation**: Masking strategy determines what the model must predict from what it observes. Patch-level masking (I-JEPA, V-JEPA), object-level masking (Causal-JEPA), antenna-time block masking (WirelessJEPA)
2. **Encoding**: Context and target encoders map inputs to representations. Target encoder typically uses exponential moving average (EMA) of context encoder weights — though LeWorldModel eliminates this requirement
3. **Latent-space prediction**: Predictor network maps context embeddings to predicted target embeddings. AdaLN-zero architecture identified as critical design choice (JEPA-WMs ablation study)
4. **Regularization**: Prevents representation collapse. VICReg-style (variance-invariance-covariance), SIGReg, or Gaussian latent regularization (LeWorldModel's 2-term approach)
5. **Energy minimization**: Compatible (context, target) pairs receive low energy; incompatible pairs receive high energy

**Collapse Prevention** — the central engineering challenge:

- **VICReg**: Variance preservation (hinge loss), invariance to augmentations (MSE), covariance decorrelation. Used in EB-JEPA, V-JEPA family
- **SIGReg**: Modality-agnostic shared target distribution. Used in Le MuMo JEPA for cross-modal alignment
- **Gaussian regularization**: Enforces Gaussian-distributed latent embeddings. LeWorldModel achieves stability with only this + prediction loss (2 terms vs. 6)
- **Barlow Twins-style redundancy reduction**: Used in R2-Dreamer; conceptually parallel to VICReg

**JEPA Variant Lineage**:

- I-JEPA (images) → V-JEPA (video) → V-JEPA 2 (world model + action conditioning) → V-JEPA 2.1 (dense features)
- VL-JEPA (vision-language, continuous embedding prediction replacing autoregressive tokens)
- Le MuMo JEPA (multi-modal: RGB + LiDAR/thermal via learnable fusion tokens)
- Causal-JEPA (object-centric masking for causal reasoning)
- LeWorldModel (stable end-to-end from pixels, 2 loss terms, ~15M params)
- VJEPA/BJEPA (probabilistic/Bayesian extensions for uncertainty quantification)
- ACT-JEPA (unified policy + world model learning)
- Domain-specific: WirelessJEPA, JEPA-MSAC, EchoJEPA, 3D-JEPA

### How JEPA Differs

**vs. Contrastive Learning** (CLIP, SimCLR): Contrastive methods require explicit negative pairs and learn to push apart non-matching samples. JEPA avoids negatives entirely — it predicts target representations from context, using regularization to prevent collapse. This eliminates the need for carefully constructed negative sampling strategies.

**vs. Masked Autoencoders** (MAE): MAE reconstructs raw pixels/tokens from masked inputs. JEPA predicts in representation space, which (a) filters task-irrelevant variation (e.g., ultrasound speckle in EchoJEPA), (b) operates at higher abstraction enabling efficient planning, and (c) avoids the computational cost of pixel-level reconstruction.

**vs. Autoregressive Models** (GPT, LLMs): Autoregressive models predict next tokens sequentially. JEPA predicts representations of masked regions in parallel. However, Blondel et al. (2025) proved an explicit bijection between ARMs and EBMs, suggesting autoregressive models implicitly learn energy landscapes — the paradigms are more connected than they appear.

**vs. Diffusion/Flow Models** (Cosmos, Genie): Diffusion/flow models generate in pixel space — producing inspectable video outputs. JEPA operates in latent space — more efficient for planning (48x faster, per LeWorldModel) but outputs are not directly visualizable. The two approaches are complementary: Cosmos for synthetic data generation, JEPA for efficient planning and control.

### JEPA Current State (as of 2026-04)

**Maturation signals**:

- Training stability solved: LeWorldModel achieves stable end-to-end training with minimal hyperparameters
- Systematic engineering guidance available: JEPA-WMs ablation study identifies critical design choices
- Accessible tooling: EB-JEPA library, stable-worldmodel framework, LeWM implementation
- AMI Labs ($1.03B seed) commercializing JEPA-based world models

**Active frontiers**:

- Dense features (V-JEPA 2.1): Addressing weakness in per-patch feature quality for fine-grained tasks
- Causal reasoning (Causal-JEPA): Object-level masking for counterfactual understanding; 100x reduction in required latent features
- Probabilistic extensions (VJEPA/BJEPA): Uncertainty quantification for planning under stochastic dynamics
- Multi-modal fusion (Le MuMo JEPA, VL-JEPA): Integrating heterogeneous sensor inputs and language
- Domain expansion: Telecommunications (3 papers), healthcare (EchoJEPA), autonomous driving (Le MuMo JEPA on Waymo/nuScenes)

**Open questions**:

- Optimal latent dimensionality remains unclear across papers and domains
- Scaling laws for JEPA-based world models not yet established (unlike LLMs)
- Long-horizon consistency in multi-step rollouts still challenging
- How to best integrate language reasoning with JEPA's latent prediction (VL-JEPA vs. MLLM-WM fusion)

---

## Energy-Based Models (EBMs)

### EBM Overview

Energy-Based Models learn a scalar energy function E(x, y) that assigns low energy to compatible (x, y) configurations and high energy to incompatible ones. Unlike probabilistic models that must normalize over all possible outputs, EBMs only need to compare relative energies — enabling flexible modeling of complex, multi-modal distributions without tractable partition functions.

### EBM Technical Details

**Connection to JEPA**: JEPA is fundamentally an energy-based architecture. The prediction error between predicted and actual target embeddings defines an energy landscape. Compatible (context, target) pairs receive low prediction error (low energy); incompatible pairs receive high error (high energy). The EB-JEPA library makes this connection explicit.

**ARM-EBM Bijection** (Blondel et al. 2025): Autoregressive language models are secretly energy-based models. The paper establishes an explicit bijection in function space, showing this correspondence is a special case of soft Bellman equations in maximum entropy RL. This explains how next-token prediction enables lookahead planning — the autoregressive model implicitly learns an energy function over sequences.

**Quasimetric Structure** (Kobanda & Radji 2026): Intrinsic (least-action) energies in JEPAs constitute quasimetrics under closure and additivity conditions. This links JEPA energy functions to Quasimetric Reinforcement Learning's value class, providing theoretical grounding for using energy functions in goal-reaching control. Symmetric finite energies are structurally incompatible with one-way reachability, motivating asymmetric formulations.

### How EBMs Differ

**vs. Likelihood-Based Models** (VAEs, normalizing flows): Likelihood-based models must compute or approximate the partition function Z for normalization. EBMs avoid this — they only need relative energy comparisons, enabling more flexible architectures. The trade-off: sampling from EBMs requires MCMC or other iterative methods.

**vs. GANs**: Both avoid explicit likelihood computation. GANs use adversarial training (generator vs. discriminator), while EBMs use contrastive divergence or score matching. EBMs provide a more principled energy landscape that can be used directly for planning and inference.

**vs. Diffusion Models**: Diffusion models learn score functions (gradients of log-probability), which are closely related to energy gradients. Score-based diffusion can be viewed as a specific instantiation of EBM training. The Cosmos family uses flow-based (related to diffusion) generation in pixel space, while JEPA-style EBMs operate in latent space.

### EBM Current State (as of 2026-04)

The EBM framework is converging with JEPA — both use energy-based formulations, both avoid explicit reconstruction, and both use regularization to prevent collapse. The ARM-EBM connection bridges the autoregressive and energy-based paradigms theoretically, while JEPA provides the practical architecture. Key open question: whether EBM-style energy landscapes can enable more principled planning than current rollout-based approaches.

---

## Dragon Hatchling (BDH)

### BDH Overview

Baby Dragon Hatchling (BDH) is a biologically-inspired LLM architecture from Pathway that replaces the transformer's attention mechanism with a scale-free network of locally-interacting neuron particles. Uses Hebbian learning for working memory via synaptic plasticity, producing models that match GPT-2 performance at 10M-1B parameters while providing built-in interpretability.

### BDH Technical Details

- Scale-free network topology with heavy-tailed degree distributions and high modularity matching biological neural networks
- Hebbian working memory via synaptic plasticity; individual synapses strengthen for specific concepts during processing
- Spiking neurons with excitatory/inhibitory dynamics and sparse, positive activation vectors
- Built-in monosemanticity at the architecture level — sparse activations on language tasks provide interpretability without post-hoc analysis (unlike transformers requiring mechanistic interpretability)
- GPU-optimized state-space formulation enables efficient execution despite non-standard architecture

### How BDH Differs

**vs. Transformers**: Transformers use global attention (all-to-all token interaction); BDH uses local interactions in a scale-free topology. Transformers store context in KV cache; BDH uses synaptic plasticity. Transformers require post-hoc interpretability analysis; BDH provides built-in monosemantic activations.

**vs. Other Bio-Inspired Approaches**: Unlike previous spiking neural network research that focused on neuromorphic hardware efficiency, BDH targets competitive language modeling performance at scale, demonstrating that biological principles can match transformer performance rather than merely offering hardware advantages.

### BDH Current State (as of 2026-04)

Single paper (2025-09) with active open-source community (3,400+ GitHub stars). MLX and Burn framework ports underway. Represents an alternative foundation architecture that could eventually be applied to world modeling, though current work focuses on language tasks. The interpretability advantage — knowing which synapses encode which concepts — could be valuable for world models that need transparent causal representations.

---

## World Models

### World Models Overview

World models are internal representations of environment dynamics that enable agents to predict future states, plan actions, and make decisions. They learn "how the world works" from observation, providing a mental simulation capability that allows reasoning about consequences without physical interaction. The term encompasses both the cognitive science concept (humans build internal models of reality) and the technical AI systems that implement this.

### World Model Approaches

**Four-branch taxonomy** (Dong et al. 2026 survey):

1. **Observation-level generative** (Cosmos, Genie): Generate future observations (video frames) directly. Inspectable outputs, useful for synthetic data generation, but computationally expensive for planning. Cosmos-Predict2.5 uses flow-based architecture at 2B/14B parameters; Genie 3 enables real-time interactive world generation at 720p/24fps.
2. **Latent space** (JEPA, Dreamer family): Predict in learned representation space. Efficient for planning (up to 48x faster than observation-level), filter task-irrelevant variation, but outputs are not directly visualizable. JEPA is the primary architecture; DreamerV3/NE-Dreamer/R2-Dreamer are RL-focused variants.
3. **RL-based** (DreamerV3, Optimistic World Models): Task-optimized world models trained within RL loops. Optimistic World Models integrate classical adaptive control (RBMLE) with deep RL for efficient exploration. RLVR-World applies RL post-training to optimize for transition quality rather than maximum likelihood.
4. **Object-centric** (Causal-JEPA): Operate on object-level representations rather than pixel patches. Enable compositional reasoning and causal understanding. Causal-JEPA achieves comparable planning with 1% of the latent features required by patch-based models.

**Integration paradigms** with action systems (VLA survey):

- **Modular**: World model and policy as separate modules (interpretable but error-propagating)
- **Sequential**: Plan-then-execute hierarchical workflows (latency overhead)
- **Unified**: End-to-end fusion of prediction and action (ACT-JEPA, harder to debug)

**Classification axes** (from survey analysis, complementary to the four-branch taxonomy above):

1. **Representation Dimensionality** — the domain in which predictions are computed:
   - *Pixel-space (Visual Simulators)*: Sora, Genie 3, GAIA-2 — high-fidelity video output, indispensable for human-in-the-loop training and visual verification, but computationally intensive
   - *Latent-space (Abstract Dynamics)*: JEPA family, DreamerV3 — compressed embedding spaces, optimized for planning efficiency (up to 48x faster), ignore irrelevant visual variation (lighting, shadows)
   - *3D-space (Geometric Reconstructors)*: [World Labs](players.md#world-labs) Marble, InfiniCube — lift 2D inputs into persistent 3D layouts (Gaussian splats, meshes), serve as structural foundations for VR/AR and game engines

2. **Functional Coupling** — how tightly the world model is integrated with decision-making:
   - *Decision-coupled*: Intrinsically linked to a controller/policy; purpose is MBRL or MPC. Examples: [Tesla](players.md#tesla) FSD, [Wayve](players.md#wayve) AV 2.0
   - *Foundation/General-purpose*: Broad physical knowledge repositories fine-tunable for diverse tasks. Examples: [NVIDIA](players.md#nvidia) Cosmos, [Google DeepMind](players.md#google-deepmind) Genie 3
   - *Observational*: Learn representations from passive observation without action conditioning; used as pre-trained backbones. Examples: I-JEPA, early V-JEPA variants

3. **Temporal Processing** — mechanism for state transition and future rollout:
   - *Sequential (Autoregressive)*: Frame-by-frame generation, high local consistency but prone to geometric drift over long horizons. Examples: Genie 3, GAIA-1
   - *Global (Diffusion/Flow)*: Predict distribution of possible futures in one or more steps, better global structural stability. Examples: Sora, GAIA-2, Cosmos-Predict2.5

### World Model Technical Details

**Five functional roles** (Abbeel & Malik et al. 2026 survey): World models serve robotics across policy learning, planning, simulation, evaluation, and data generation. This taxonomy clarifies that world models are not monolithic — a single model may serve multiple roles, and different architectures suit different roles. JEPA excels at planning; pixel-space models (Cosmos) excel at data generation. Ctrl-World (Finn et al. 2026) demonstrates the evaluation role: ranking policy performance via imagined rollouts without real-world testing, with synthetic trajectories improving policy success by 44.7%.

**Decoder-free trend**: R2-Dreamer and NE-Dreamer both eliminate pixel reconstruction, predicting in embedding space instead. This parallels JEPA's core principle and suggests convergent design across the field. Both use redundancy reduction (Barlow Twins, predictive alignment) to prevent collapse — the same challenge JEPA addresses with VICReg.

**RL post-training**: Emerging paradigm where world models are first pre-trained (self-supervised) then post-trained with RL for task-relevant quality. RLVR-World (+30.7% accuracy), WorldCompass (long-horizon improvement), and RWML (sim-to-real gap rewards) demonstrate this across text, video, and embodied domains.

**Safety verification**: Oracle-efficient ADMM framework (Sapenov 2026) combines fast JEPA planning with deterministic simulator verification, achieving 125x reduction in verification calls. Addresses the deployment barrier that learned world models can produce unsafe plans.

**Physical reasoning**: Cosmos-Reason1 adds explicit physical common sense via hierarchical ontology (space, time, physics). Complementary to JEPA's implicit physics learning — explicit ontologies can guide and constrain predictions. The proposed MLLM-WM fusion architecture (Feng et al. 2025) combines language grounding with physics simulation.

### World Models Current State (as of 2026-05)

**Three paradigms crystallizing**:

- **Pixel-space** (Cosmos, Genie): Industrial deployment for synthetic data generation, scenario simulation. NVIDIA Cosmos adopted by Agility, Figure AI, 1X, Uber, Waabi. Waymo uses Genie 3-based world model for AV simulation.
- **Latent-space** (JEPA): Efficient planning and control for robotics. AMI Labs commercializing. Research community producing accessible tooling (EB-JEPA, stable-worldmodel, LeWM).
- **3D-space** ([World Labs](players.md#world-labs) Marble): Persistent 3D world reconstruction from multimodal inputs. Human-AI co-creation via Chisel editing. Adopted for VFX, architecture, and robot training data generation. Distinct from pixel-space (generates navigable 3D structures, not video) and latent-space (outputs are directly inspectable and editable).

**Embodied AI architecture taxonomy** (a16z framing, complementary to world model paradigms):

The a16z "Frontier Systems for the Physical World" essay proposes a three-way classification for how physical AI systems acquire world knowledge:

- **Vision-Language-Action (VLA) Models**: Scale pretrained vision-language models (internet images + text) with action decoders. *Examples*: [Physical Intelligence](players.md#physical-intelligence-π) π0/π0.5, [NVIDIA](players.md#nvidia) GR00T N1
- **World Action Models (WAMs)**: Build on video diffusion transformers, inheriting physical dynamics priors from video prediction. The world model is embedded in the video backbone — jointly predicts future frames and actions through shared denoising. *Examples*: [NVIDIA](players.md#nvidia) DreamZero (14B params, 2x generalization vs. VLAs), planned GR00T N2
- **Native Embodied Foundation Models**: Train from scratch on physical interaction data (wearables, teleoperation) rather than internet images. *Examples*: [Generalist AI](players.md#generalist-ai) GEN-1 (500K hours of wearable data, 99% task success)

*Key insight*: WAMs represent a fusion of world models and policy learning — treating video generation as an implicit visual planner that guides action production. This contrasts with modular approaches where world model and policy are trained separately.

**Emerging alternative paradigm**: [Active Inference](concepts.md#active-inference) ([Verses AI](players.md#verses-ai) AXIOM) — unifies perception, planning, and control via the Free Energy Principle. Object-centric, hierarchical agent structure. Theoretically distinct from all three paradigms above but with potential complementarity. See dedicated Active Inference section below.

**Convergence signals**:

- Decoder-free Dreamer variants converge toward JEPA principles
- RL post-training applicable to both paradigms
- Physical reasoning (Cosmos-Reason) could enhance either approach
- ARM-EBM bijection suggests autoregressive and energy-based approaches are theoretically unified
- Counterfactual reasoning emerging as new frontier (CWMDT combines digital twins + diffusion + LLM causal reasoning)

**Domain expansion beyond vision/robotics**:

- Telecommunications: WirelessJEPA, JEPA-MSAC, Wireless World Model for 6G — 3 papers in 3 months
- Healthcare: EchoJEPA (18M echocardiograms, 300K patients)
- Autonomous vehicles: Waymo World Model, DWM robustness framework, Le MuMo JEPA sensor fusion
- Agentic AI: AWM (synthetic environments for agent RL), WebWorld (web agent training), "Agentic World Modeling" survey (400+ works). World models for digital agents emerging as distinct subfield — governed by digital rather than physical laws
- Industrial / Digital Twins: Two papers (2601.01321, 2603.17420) chart the digital twin → world model transition. Key insight: digital twins mirror and monitor; world models internalize dynamics for autonomous reasoning. Four-stage lifecycle (Modeling → Mirroring → Intervention → Autonomous Management) maps to world model capability levels

**Competing capability taxonomies** (as of 2026-05):

- **Our primer**: L1-L4 (representation → prediction → action-conditioned → planning/control)
- **Agentic World Modeling** (Chu et al. 2026): L1 Predictor → L2 Simulator → L3 Evolver. L3 "Evolver" directly addresses the continual learning gap — world models that self-correct
- **Healthcare survey** (2511.16333): L1-L4 similar to ours, applied to clinical prediction
- **Robot Learning survey** (2605.00080): Five functional roles (policy learning, planning, simulation, evaluation, data generation) — orthogonal to capability levels
- **Governing laws axis** (Chu et al. 2026): Physical, digital, social, scientific — recognizes that world models for web agents face fundamentally different constraints than those for robotics

**Google's convergence bet**: Hassabis (2025-05) explicitly frames extending Gemini 2.5 Pro into a world model — betting on LLM→WM integration rather than purpose-built WM architectures. If realized, validates the thesis that LLMs and world models converge. Contrasts with Meta's JEPA-centric approach (purpose-built architecture for physical world modeling).

**Open challenges**:

- Long-horizon consistency: video-based models limited to minutes; latent-space models accumulate prediction error
- Causal understanding: Causal-JEPA is a step, but systematic causal reasoning remains nascent
- Sim-to-real transfer: Cosmos addresses with Transfer2.5; JEPA approaches lack equivalent
- Evaluation standards: No consensus benchmarks for world model quality across domains
- Scaling laws: Established for LLMs but not for world models of either paradigm

---

## Active Inference

### Active Inference Overview

Active Inference is a biology-inspired framework for world models based on Karl Friston's Free Energy Principle. Unlike standard RL (which maximizes reward) or JEPA (which minimizes prediction error in latent space), Active Inference agents minimize *free energy* — a unified objective that combines prediction accuracy with epistemic value (reducing uncertainty). Agents don't just predict the world; they actively seek observations that resolve their uncertainty about it.

### Active Inference Technical Details

[Verses AI](players.md#verses-ai)'s AXIOM (Active eXpanding Inference with Object-centric Models) is the primary implementation:

- **Unified perception-planning-control**: A single generative model handles all three, unlike modular architectures that separate world model from policy
- **Hierarchical agent architecture**: Every joint in a robot body is an agent with its own local world model. "Shared intelligence" emerges from coordination rather than centralized control
- **Object-centric representations**: AXIOM creates explicit object-level representations, enabling compositional reasoning similar to Causal-JEPA but derived from different theoretical foundations
- **Epistemic foraging**: Agents actively seek observations that maximize information gain, not just reward — moving from "what will happen if I do this?" to "what will I *believe* if I do this?" (termed "Sophisticated Intelligence" or S2)
- **Recovery without retraining**: Hierarchical local models dynamically adjust to unexpected perturbations by resolving prediction errors locally

### How Active Inference Differs

**vs. JEPA**: JEPA predicts in latent space to learn representations; Active Inference uses prediction error as a drive for action selection. JEPA is primarily a learning architecture; Active Inference is a complete perception-action framework. Both avoid pixel reconstruction.

**vs. Standard RL (DreamerV3)**: RL maximizes expected reward; Active Inference minimizes expected free energy (which includes both reward-seeking and uncertainty-reducing terms). This makes Active Inference agents naturally curious and robust to sparse reward.

**vs. LLM-based planning**: LLMs plan via token generation; Active Inference plans via variational inference over future trajectories. Active Inference has principled uncertainty quantification built in; LLMs do not.

### Active Inference Current State (as of 2026-04)

Emerging paradigm with strong theoretical foundations but limited scale demonstrations. [Verses AI](players.md#verses-ai) reported AXIOM outperforming [Google DeepMind](players.md#google-deepmind) on Atari "Gameworld 10k" challenge. The hierarchical agent architecture is a fundamentally different approach to robot control — if validated at scale, it could complement JEPA (for representation learning) and Cosmos (for synthetic data) as a third paradigm for embodied AI. Karl Friston's involvement provides deep neuroscience grounding. Key open question: whether the framework can scale to complex, high-dimensional real-world tasks beyond arcade games and simple robotics.

---

## Related Concepts

### Self-Supervised Learning (SSL)

The training paradigm underlying both JEPA and decoder-free world models. Creates learning signal from data structure (masking, prediction) rather than human labels. JEPA's contribution: predicting in representation space rather than input space, filtering irrelevant variation.

### Latent Representations

Learned compressed representations of inputs. In world models, the quality of latent representations determines planning effectiveness. Key insight from tracked papers: dense features (V-JEPA 2.1) matter for fine-grained tasks like robotic grasping — global representations alone are insufficient.

### Contrastive Learning

Alternative SSL paradigm that JEPA explicitly avoids. Contrastive methods (SimCLR, CLIP) learn by pulling positive pairs together and pushing negative pairs apart. JEPA replaces this with predictive objectives + regularization, eliminating the need for negative sampling. However, VL-JEPA shows JEPA can match contrastive baselines (CLIP, SigLIP2) on vision-language tasks.

### Model-Based Reinforcement Learning (MBRL)

Using learned world models to generate imagined trajectories for policy optimization. Dreamer family (DreamerV3, R2-Dreamer, NE-Dreamer) is the primary MBRL framework. Key trend: MBRL converging with JEPA as decoder-free variants adopt latent prediction. Optimistic World Models integrate classical control theory (RBMLE) with deep MBRL.

### Predictive Coding

Neuroscience theory that the brain continuously predicts sensory inputs and learns from prediction errors. JEPA can be viewed as implementing predictive coding in representation space. BDH's Hebbian learning provides a more directly biological implementation of similar principles.

### VICReg (Variance-Invariance-Covariance Regularization)

The dominant regularization technique in JEPA architectures. Prevents representation collapse through three terms: variance preservation (hinge loss ensures embedding dimensions maintain spread), invariance (MSE between augmented views), and covariance decorrelation (reduces redundancy between embedding dimensions). Conceptually parallel to Barlow Twins, which R2-Dreamer uses in the Dreamer family.

### World Foundation Models (WFMs)

NVIDIA's framing: general-purpose world models pre-trained on massive data, fine-tunable for domain-specific applications. Analogous to LLMs but for physical world simulation. Cosmos is the primary implementation. Contrasts with JEPA's approach of training domain-specific models from scratch (though AMI Labs may change this with scaled JEPA WFMs).

### Physical AI

Umbrella term for AI systems that interact with the physical world — robotics, autonomous vehicles, embodied agents. World models are positioned as the enabling technology: they provide the "digital twin of the environment" that Physical AI systems need for safe, efficient learning. Cosmos-Reason1 adds explicit physical reasoning; JEPA provides efficient latent planning.

### Scientist AI

Yoshua Bengio's proposal (2025) for non-agentic AI built around a world model that explains observations and answers questions rather than autonomously pursuing goals. Deliberately avoids agency — focuses on accurate world representation with uncertainty quantification. Safety-motivated alternative to the autonomous agent paradigm.

---

**Note**: This document grows as papers are added and understanding deepens. Each section is expanded with technical details, equations, architectures, and comparisons synthesized from tracked publications.
