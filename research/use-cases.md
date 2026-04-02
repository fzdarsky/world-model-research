# Use Cases

> Applications of world models across industries

**Last Updated**: 2026-04-02

---

## Robotics

*Manipulation, navigation, task planning*

### Synthetic Training Data Generation for Robot Manipulation

**Industry**: Manufacturing | Robotics

**Description**: World models generate large volumes of synthetic training scenarios for robot manipulation policies, reducing the need for expensive and dangerous real-world data collection. A world model (e.g., Cosmos-Predict) generates future visual states conditioned on robot actions; these synthetic rollouts train manipulation policies (e.g., GR00T N1, π0.5) that transfer to real robots. [NVIDIA](players.md#nvidia) claims Cosmos can reduce real-world data collection budgets by up to 60%. V-JEPA 2-AC demonstrated 45% zero-shot grasping success (vs. 8% baseline) after action conditioning with only 62 hours of robot video.

**Technical Requirements**: High-fidelity visual generation at sufficient resolution for manipulation (object textures, gripper contact). Action conditioning — the world model must accept robot action inputs to generate plausible outcomes. Sim-to-real transfer fidelity (Cosmos-Transfer addresses this). GPU clusters for world model inference during policy training; real-time inference for closed-loop deployment.

**Current Solutions**: [NVIDIA](players.md#nvidia) Cosmos + GR00T N1 (adopted by [Figure AI](players.md#figure-ai), Agility, 1X, Boston Dynamics, Unitree); [Physical Intelligence](players.md#physical-intelligence-π) π0.5 (open-world manipulation); V-JEPA 2-AC (zero-shot grasping via JEPA representations)

**Research Gaps**: Sim-to-real gap remains significant for contact-rich manipulation (deformable objects, liquids). No standardized benchmark for world model quality as measured by downstream policy performance. Long-horizon multi-step task generation (>30s) still unreliable.

---

## Autonomous Vehicles

*Self-driving, path planning, sim-to-real transfer*

### Safety-Critical Scenario Simulation for Autonomous Driving

**Industry**: Transport&Logistics

**Description**: World models generate rare, safety-critical driving scenarios (e.g., near-collisions, adverse weather, animal encounters) that are too dangerous or infrequent to capture at scale in real-world driving. Waymo's world model generates multi-sensor outputs (camera + LiDAR) for long-tail events. [Wayve](players.md#wayve)'s GAIA-3 is purpose-built for evaluating end-to-end driving systems by generating controllable, parametrically varied driving scenarios. [Tesla](players.md#tesla)'s FSD v14 uses occupancy networks to predict 3D voxel-based future states.

**Technical Requirements**: Multi-camera, spatiotemporally consistent video generation (GAIA-2 achieves this). LiDAR point cloud synthesis alongside camera views. Controllable scenario parameters (weather, traffic density, pedestrian behavior). Real-time occupancy prediction for deployment (Tesla FSD). Minutes-scale scenario generation with geometric consistency.

**Current Solutions**: Waymo World Model (Genie 3-based, multi-sensor); [Wayve](players.md#wayve) GAIA-2/3 (controllable multi-view generation); [Tesla](players.md#tesla) FSD v14 (occupancy networks in production); DriveDreamer-2 (LLM-prompted scene generation); HERMES (unified 3D scene understanding)

**Research Gaps**: Geometric drift in autoregressive generation over long horizons. No industry-standard fidelity metric for generated driving scenarios. Regulatory acceptance of world-model-generated scenarios for safety validation is undefined.

---

## Healthcare & Medical Imaging

*Diagnostics, clinical decision support, surgical planning*

### Clinical Outcome Simulation and Diagnostics

**Industry**: Healthcare

**Description**: World models learn representations from medical imaging data (echocardiograms, CT scans, MRI) to predict disease progression, simulate treatment outcomes, and support clinical decisions. EchoJEPA (trained on 18M echocardiograms across 300K patients) demonstrates JEPA representations transfer to cardiac diagnostics. MeWM simulates post-treatment tumor evolution to help clinicians select optimal protocols. Foresight forecasts medical event timelines from patient histories.

**Technical Requirements**: Foundation-scale training on clinical data (EchoJEPA: 18M studies). Regulatory compliance (FDA/CE marking for clinical use). Uncertainty quantification — clinicians need confidence bounds, not point predictions. Patient privacy preservation during model training. Integration with clinical workflows (PACS, EHR systems).

**Current Solutions**: EchoJEPA (University of Toronto / Vector Institute); MeWM (action-conditioned 3D tumor simulation); Foresight (medical event timeline prediction); [AMI Labs](players.md#ami-labs) (targeting healthcare applications)

**Research Gaps**: Regulatory pathway for world-model-based clinical decision support is undefined. Causal reasoning required for treatment planning (beyond correlation). Limited multi-modal fusion (imaging + genomics + lab results). Generalization across patient populations and imaging equipment.

---

## Industrial & Manufacturing

*Digital twins, process optimization, predictive maintenance*

### Autonomous Digital Twins for Factory Optimization

**Industry**: Manufacturing

**Description**: World models power "autonomous digital twins" that continuously simulate, predict, and optimize manufacturing operations in real time. [Siemens](players.md#siemens) is building the first AI-driven adaptive factory (Erlangen, 2026) using [NVIDIA](players.md#nvidia) Omniverse + PhysicsNeMo for generative physics simulation. [Schneider Electric](players.md#schneider-electric) targets 80% autonomous operations by 2030 across energy and chemicals. PepsiCo digitizes factories as high-fidelity 3D digital twins with Siemens. Industrial players use the term "autonomous digital twins" rather than "world models," but the underlying workload pattern — learn dynamics, predict, plan — is identical.

**Technical Requirements**: Real-time physics simulation coupled to sensor feeds (temperature, pressure, vibration). Predict-then-act loop with safety verification before executing changes. Integration with industrial control systems (PLCs, SCADA). On-premises or sovereign cloud deployment (manufacturing IP sensitivity). Multi-physics simulation (thermal, structural, fluid dynamics).

**Current Solutions**: [Siemens](players.md#siemens) Digital Twin Composer + [NVIDIA](players.md#nvidia) Omniverse (Erlangen factory); [Schneider Electric](players.md#schneider-electric) EcoStruxure + Omniverse (energy/chemicals); PepsiCo factory digital twins (with Siemens)

**Research Gaps**: Bridging simulation fidelity and real-time update rates for closed-loop control. No standardized interoperability between digital twin platforms. Autonomous decision-making in safety-critical industrial processes requires formal verification. Edge deployment of world models for latency-sensitive manufacturing control.

---

## Telecommunications

*Wireless channel modeling, network optimization, beam prediction*

### Wireless Channel Prediction and Network Optimization

**Industry**: Telecommunications

**Description**: World models predict the evolution of wireless channel states for beam management, localization, and interference classification. WirelessJEPA applies JEPA's masking strategy to antenna-time blocks in channel state information (CSI), learning representations that transfer across 6 downstream tasks. JEPA-MSAC addresses multi-task wireless sensing. China Mobile/Huawei's Wireless World Model for 6G fuses CSI, 3D point clouds, and user trajectories via multi-modal JEPA + MoE Transformer.

**Technical Requirements**: Real-time inference on CSI data streams (millisecond-scale beam decisions). Multi-modal fusion (RF signals + spatial data + user mobility). Transfer learning across cell sites and frequency bands. On-premises deployment for telco infrastructure (latency, data sovereignty). Support for 6 downstream tasks from a single model (WirelessJEPA).

**Current Solutions**: WirelessJEPA (JEPA for 6 wireless tasks); JEPA-MSAC (multi-task wireless sensing); Wireless World Model for 6G (China Mobile/Huawei, multi-modal JEPA + MoE)

**Research Gaps**: No production deployment of JEPA-based wireless models yet (all academic). Scalability to dense urban networks with thousands of base stations untested. Integration with existing O-RAN and network automation frameworks (e.g., ONAP) undefined. Real-time inference latency requirements for beam management may exceed current model serving capabilities.

---

## Gaming & Simulation

*Game AI, virtual worlds, procedural generation*

### Interactive World Generation from Text and Image

**Industry**: Gaming & Creative Media

**Description**: World models generate interactive, explorable 3D environments from text prompts, images, or sketches — replacing or augmenting traditional game engines. [Google DeepMind](players.md#google-deepmind)'s Genie 3 generates 720p/24fps interactive environments with "emergent physics" learned from observation (no hardcoded physics libraries). [World Labs](players.md#world-labs)' Marble reconstructs persistent 3D worlds from multimodal inputs with a "Chisel" feature for human-AI co-creation. Used for VFX pre-visualization, game prototyping, and architectural design.

**Technical Requirements**: Real-time generation (24fps minimum for interactivity). Spatial and temporal consistency over minutes of interaction. User control mapping (latent actions → human inputs). 3D persistence (objects maintain state when camera moves away). High visual fidelity (720p+).

**Current Solutions**: [Google DeepMind](players.md#google-deepmind) Genie 3 (interactive, 720p/24fps); [World Labs](players.md#world-labs) Marble (persistent 3D, Chisel editing); Oasis AI (dreamlike interactive worlds); GWM-1 (deterministic spatial coherence)

**Research Gaps**: Minutes-scale consistency degrades in autoregressive generation. No standard benchmark for interactive world model quality. Compute costs for real-time high-fidelity generation remain prohibitive for consumer deployment. Social/NPC behavior modeling within generated worlds is rudimentary.

---

## Scientific Discovery

*Physics simulation, molecular modeling, materials design*

---

## Agentic AI

*Autonomous agents, web agents, tool use, planning with world models*

---

## Other Applications

*Defense, legal, energy, logistics, etc.*

### Autonomous Drone Coordination and Battlefield Awareness

**Industry**: Defense

**Description**: World models enable autonomous coordination of drones and unmanned systems in complex, contested environments. Anduril Industries' Lattice platform uses world-aware reasoning to coordinate autonomous drones and manage battlefield technology, building real-time situational awareness from multi-sensor fusion and predicting adversary behavior through internal simulation.

**Technical Requirements**: Real-time multi-sensor fusion (cameras, radar, RF). Adversary behavior prediction under uncertainty. Edge deployment on constrained hardware (drone-mounted compute). Communication-denied operation (models must function without continuous connectivity). Formal safety verification for autonomous weapons decisions.

**Current Solutions**: Anduril Industries Lattice platform

**Research Gaps**: Adversarial robustness — world models must handle deliberate deception. Ethical and regulatory frameworks for autonomous lethal decision-making. Multi-agent coordination with degraded communications. Transfer from simulation to contested real-world environments.

### Counterfactual Accident Reconstruction

**Industry**: Legal

**Description**: Counterfactual World Simulation Models (CWSMs) reconstruct accidents in high-fidelity 3D and simulate alternative scenarios (e.g., "would the accident have been avoided if the pedestrian had seen the car?"). CWMDT turns standard video diffusion models into counterfactual world models by constructing digital twins of observed scenes and reasoning over object relationships through an LLM. Used as persuasive evidence for legal fact-finders.

**Technical Requirements**: High-fidelity 3D scene reconstruction from limited evidence (dashcam, surveillance footage). Causal reasoning over object relationships (not just visual generation). Counterfactual simulation with controlled variable manipulation. Expert-explainable outputs suitable for courtroom presentation. Temporal precision (exact timing of driver reactions, braking distances).

**Current Solutions**: CWMDT (digital twin-conditioned video diffusion); CausalVAE (causal inference); Pearl theory-based frameworks

**Research Gaps**: Legal admissibility standards for AI-generated reconstructions are undefined. Bias in world model training data could produce systematically skewed reconstructions. Uncertainty quantification for counterfactual claims needed. No established methodology for validating counterfactual accuracy.

---

**Note**: Each entry follows the use-case-entry template from `templates/use-case-entry.md`.
Use cases include technical requirements, current solutions, and research gaps.
