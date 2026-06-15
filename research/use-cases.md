# Technical Use Cases

> Physical AI capability patterns — what they require and who serves them

**Last Updated**: 2026-06-15

---

## Robotics

**Description**: Robot manipulation, navigation, and task planning using learned world models to generate synthetic training data, predict action outcomes, and enable zero-shot or few-shot transfer to real-world tasks.

**Common building blocks** (across all verticals):

| Building Block | Role in this use case |
| -------------- | --------------------- |
| [Robot Foundation Models](building-blocks.md#robot-foundation-models) | Required — Policy networks that execute manipulation/navigation tasks |
| [Simulation Engines](building-blocks.md#simulation-engines) | Required — Generate synthetic scenarios for policy training |
| [Sim-to-Real Transfer Pipeline](building-blocks.md#sim-to-real-transfer-pipeline) | Required — Bridge gap between simulated and real-world performance |
| [Robot Middleware](building-blocks.md#robot-middleware) | Required — Connect models to robot hardware (control, sensing) |
| [Sensor Data Ingestion](building-blocks.md#sensor-data-ingestion) | Required — Process camera, proprioceptive, tactile sensor streams |
| [Edge AI Inference Runtime](building-blocks.md#edge-ai-inference-runtime) | Required — Real-time on-robot inference for closed-loop control |
| [Model Serving for Physical AI](building-blocks.md#model-serving-for-physical-ai) | Required — Serve world models during policy training rollouts |

### Manufacturing & Logistics (Robotics)

**Verticals**: Manufacturing | Logistics

**Additional building blocks**: [Robot Fleet Management & Observability](building-blocks.md#robot-fleet-management--observability) (important for factory-scale deployment)

**Vertical-specific requirements**:

- **Functional**: High-fidelity visual generation at sufficient resolution for manipulation (object textures, gripper contact). Action conditioning — the world model must accept robot action inputs to generate plausible outcomes. Zero-shot grasping success for novel objects (V-JEPA 2-AC demonstrated 45% vs. 8% baseline).
- **Non-functional**: GPU clusters for world model inference during policy training. Real-time inference (<50ms) for closed-loop deployment. Reduce real-world data collection budgets by 40-60% through synthetic data generation.
- **Regulatory**: ISO 10218 (industrial robot safety), ISO/TS 15066 (collaborative robots)

**Current solutions**: [NVIDIA](ecosystem.md#nvidia) Cosmos + GR00T N1 (adopted by [Figure AI](ecosystem.md#figure-ai), Agility, 1X, Boston Dynamics, Unitree); [Physical Intelligence](ecosystem.md#physical-intelligence-pi) π0.5 (open-world manipulation); V-JEPA 2-AC (zero-shot grasping via JEPA representations)

**Gaps**: Sim-to-real gap remains significant for contact-rich manipulation (deformable objects, liquids). No standardized benchmark for world model quality as measured by downstream policy performance. Long-horizon multi-step task generation (>30s) still unreliable.

---

## Autonomous Vehicles

**Description**: Self-driving systems using world models to predict future vehicle and environment states, simulate safety-critical scenarios, and train perception-planning-control policies for autonomous navigation.

**Common building blocks** (across all verticals):

| Building Block | Role in this use case |
| -------------- | --------------------- |
| [Video Generation / Prediction Models](building-blocks.md#video-generation--prediction-models) | Required — Generate multi-camera, spatiotemporally consistent driving scenarios |
| [Simulation Engines](building-blocks.md#simulation-engines) | Required — Simulate rare, safety-critical events (collisions, adverse weather) |
| [Sensor Data Ingestion](building-blocks.md#sensor-data-ingestion) | Required — Multi-modal fusion (camera, LiDAR, radar) |
| [Edge AI Inference Runtime](building-blocks.md#edge-ai-inference-runtime) | Required — Real-time occupancy prediction for deployment |
| [Safety, Validation & Certification Frameworks](building-blocks.md#safety-validation--certification-frameworks) | Required — Validate AV systems against regulatory standards |

### Transport & Logistics (Autonomous Vehicles)

**Verticals**: Transport & Logistics

**Additional building blocks**: [Post-Training / Fine-Tuning Pipeline](building-blocks.md#post-training--fine-tuning-pipeline) (important for scenario-specific adaptation)

**Vertical-specific requirements**:

- **Functional**: Multi-camera, spatiotemporally consistent video generation (GAIA-2 achieves this). LiDAR point cloud synthesis alongside camera views. Controllable scenario parameters (weather, traffic density, pedestrian behavior). Real-time occupancy prediction for deployment (Tesla FSD). Minutes-scale scenario generation with geometric consistency.
- **Non-functional**: Real-time inference (<100ms) for occupancy networks in production. 720p+ multi-view generation at 24fps for simulation. Geometric consistency over 30+ second rollouts.
- **Regulatory**: ISO 26262 (functional safety), UNECE WP.29 (automated driving), SAE J3016 (automation levels)

**Current solutions**: Waymo World Model (Genie 3-based, multi-sensor); [Wayve](ecosystem.md#wayve) GAIA-2/3 (controllable multi-view generation); [Tesla](ecosystem.md#tesla) FSD v14 (occupancy networks in production); DriveDreamer-2 (LLM-prompted scene generation); HERMES (unified 3D scene understanding)

**Gaps**: Geometric drift in autoregressive generation over long horizons. No industry-standard fidelity metric for generated driving scenarios. Regulatory acceptance of world-model-generated scenarios for safety validation is undefined.

---

## Digital Twins

**Description**: Autonomous digital twins that continuously simulate, predict, and optimize industrial operations in real time using learned dynamics models coupled to live sensor feeds.

**Common building blocks** (across all verticals):

| Building Block | Role in this use case |
| -------------- | --------------------- |
| [Simulation Engines](building-blocks.md#simulation-engines) | Required — Multi-physics simulation (thermal, structural, fluid dynamics) |
| [Digital Twin Runtime](building-blocks.md#digital-twin-runtime) | Required — Real-time predict-then-act loop with safety verification |
| [Sensor Data Ingestion](building-blocks.md#sensor-data-ingestion) | Required — Process industrial sensors (temperature, pressure, vibration) |
| [Physics-Informed ML Frameworks](building-blocks.md#physics-informed-ml-frameworks) | Important — Incorporate domain physics into learned models |

### Manufacturing (Digital Twins)

**Verticals**: Manufacturing

**Additional building blocks**: [Edge AI Inference Runtime](building-blocks.md#edge-ai-inference-runtime) (important for latency-sensitive control)

**Vertical-specific requirements**:

- **Functional**: Real-time physics simulation coupled to sensor feeds (temperature, pressure, vibration). Predict-then-act loop with safety verification before executing changes. Integration with industrial control systems (PLCs, SCADA). On-premises or sovereign cloud deployment (manufacturing IP sensitivity). Multi-physics simulation (thermal, structural, fluid dynamics).
- **Non-functional**: Real-time update rates for closed-loop control (<1s). High-fidelity physics simulation balancing accuracy and speed. Support for thousands of sensors per factory.
- **Regulatory**: IEC 61508 (functional safety), IEC 62443 (industrial cybersecurity)

**Current solutions**: [Siemens](ecosystem.md#siemens) Digital Twin Composer + [NVIDIA](ecosystem.md#nvidia) Omniverse (Erlangen factory); [Schneider Electric](ecosystem.md#schneider-electric) EcoStruxure + Omniverse (energy/chemicals); PepsiCo factory digital twins (with Siemens)

**Gaps**: Bridging simulation fidelity and real-time update rates for closed-loop control. No standardized interoperability between digital twin platforms. Autonomous decision-making in safety-critical industrial processes requires formal verification. Edge deployment of world models for latency-sensitive manufacturing control.

### Energy & Utilities (Digital Twins)

**Verticals**: Energy & Utilities

**Additional building blocks**: [Physics-Informed ML Frameworks](building-blocks.md#physics-informed-ml-frameworks) (required for grid/plant dynamics)

**Vertical-specific requirements**:

- **Functional**: TBD — Power grid optimization, renewable energy forecasting, plant efficiency prediction
- **Non-functional**: TBD
- **Regulatory**: NERC CIP (grid cybersecurity), IEC 61850 (power systems communication)

**Current solutions**: [Schneider Electric](ecosystem.md#schneider-electric) EcoStruxure (energy management with Omniverse)

**Gaps**: TBD

### Healthcare & Life Sciences (Digital Twins)

**Verticals**: Healthcare & Life Sciences

**Additional building blocks**: [Safety, Validation & Certification Frameworks](building-blocks.md#safety-validation--certification-frameworks) (required for medical devices)

**Vertical-specific requirements**:

- **Functional**: TBD — Patient digital twins, treatment outcome simulation
- **Non-functional**: TBD
- **Regulatory**: FDA 510(k), IEC 62304 (medical device software), EU MDR, HIPAA (data privacy)

**Current solutions**: TBD

**Gaps**: TBD

---

## Medical Diagnostics & Imaging

**Description**: World models learn representations from medical imaging data to predict disease progression, simulate treatment outcomes, and support clinical decisions through learned latent dynamics.

**Common building blocks** (across all verticals):

| Building Block | Role in this use case |
| -------------- | --------------------- |
| [Latent World Models](building-blocks.md#latent-world-models) | Required — Learn representations from imaging data (echocardiograms, CT, MRI) |
| [Simulation Engines](building-blocks.md#simulation-engines) | Important — Simulate post-treatment outcomes (tumor evolution, cardiac function) |
| [Model Serving for Physical AI](building-blocks.md#model-serving-for-physical-ai) | Required — Integrate with clinical workflows (PACS, EHR systems) |
| [Safety, Validation & Certification Frameworks](building-blocks.md#safety-validation--certification-frameworks) | Required — FDA/CE marking for clinical use |

### Healthcare & Life Sciences (Medical Diagnostics & Imaging)

**Verticals**: Healthcare & Life Sciences

**Additional building blocks**: [Data Annotation & Curation for Physical AI](building-blocks.md#data-annotation--curation-for-physical-ai) (required for clinical data labeling)

**Vertical-specific requirements**:

- **Functional**: Foundation-scale training on clinical data (EchoJEPA: 18M studies). Uncertainty quantification — clinicians need confidence bounds, not point predictions. Patient privacy preservation during model training. Integration with clinical workflows (PACS, EHR systems). Multi-modal fusion (imaging + genomics + lab results).
- **Non-functional**: Inference latency <5s for clinical decision support. Support for 300K+ patient cohorts. Uncertainty bounds with 95% confidence intervals.
- **Regulatory**: FDA 510(k) (medical devices), IEC 62304 (medical device software), EU MDR (medical device regulation), HIPAA (data privacy)

**Current solutions**: EchoJEPA (University of Toronto / Vector Institute); MeWM (action-conditioned 3D tumor simulation); Foresight (medical event timeline prediction); [AMI Labs](ecosystem.md#ami-labs) (targeting healthcare applications)

**Gaps**: Regulatory pathway for world-model-based clinical decision support is undefined. Causal reasoning required for treatment planning (beyond correlation). Limited multi-modal fusion (imaging + genomics + lab results). Generalization across patient populations and imaging equipment.

---

## Quality Control / Inspection

**Description**: Visual and sensor-based inspection of manufactured goods, using AI to detect defects, measure dimensions, and ensure compliance with quality standards.

**Common building blocks** (across all verticals):

| Building Block | Role in this use case |
| -------------- | --------------------- |
| [Sensor Data Ingestion](building-blocks.md#sensor-data-ingestion) | Required — Process camera, thermal, ultrasonic sensor streams |
| [Edge AI Inference Runtime](building-blocks.md#edge-ai-inference-runtime) | Required — Real-time defect detection on production lines |
| [Model Serving for Physical AI](building-blocks.md#model-serving-for-physical-ai) | Important — Serve inspection models at scale across factories |
| [Data Annotation & Curation for Physical AI](building-blocks.md#data-annotation--curation-for-physical-ai) | Required — Label defect examples for training |

### Manufacturing (Quality Control)

**Verticals**: Manufacturing

**Additional building blocks**: TBD

**Vertical-specific requirements**:

- **Functional**: TBD — Defect detection, dimensional measurement, surface quality assessment
- **Non-functional**: TBD — Real-time inspection (<100ms per part), 99.9%+ detection accuracy
- **Regulatory**: TBD — ISO 9001 (quality management)

**Current solutions**: TBD

**Gaps**: TBD

### Food & Beverage (Quality Control)

**Verticals**: Food & Beverage

**Additional building blocks**: TBD

**Vertical-specific requirements**:

- **Functional**: TBD — Food safety inspection, contamination detection, packaging quality
- **Non-functional**: TBD
- **Regulatory**: TBD — FDA Food Safety Modernization Act, HACCP

**Current solutions**: TBD

**Gaps**: TBD

---

## Scientific Simulation

**Description**: Autonomous experimentation systems that generate hypotheses, design experiments, execute them robotically, analyze results, and iterate in closed loops for materials discovery, drug development, and fundamental science.

**Common building blocks** (across all verticals):

| Building Block | Role in this use case |
| -------------- | --------------------- |
| [Simulation Engines](building-blocks.md#simulation-engines) | Required — Predict experimental outcomes before physical execution |
| [Physics-Informed ML Frameworks](building-blocks.md#physics-informed-ml-frameworks) | Required — Incorporate domain constraints (chemistry, physics) into models |
| [Post-Training / Fine-Tuning Pipeline](building-blocks.md#post-training--fine-tuning-pipeline) | Important — Adapt foundation models to domain-specific experimental data |

### Pharmaceuticals & Materials Science (Scientific Simulation)

**Verticals**: Pharmaceuticals | Materials Science | Chemistry

**Additional building blocks**: [Robot Middleware](building-blocks.md#robot-middleware) (important for laboratory automation integration)

**Vertical-specific requirements**:

- **Functional**: Robotic laboratory automation (liquid handling, synthesis, characterization). Multi-modal sensing beyond vision (spectroscopy, chromatography, mass spectrometry). Closed-loop integration of hypothesis → experiment → analysis. Long-horizon planning across experiment sequences (days to weeks). Domain-specific world models that predict experimental outcomes under physical/chemical constraints.
- **Non-functional**: Data efficiency — learn from sparse scientific data (not internet-scale). Long-horizon credit assignment over multi-day experiments. Support for symbolic scientific knowledge (equations, constraints).
- **Regulatory**: FDA (drug development), EPA (chemical safety), GLP (Good Laboratory Practice)

**Current solutions**: [Periodic Labs](ecosystem.md#periodic-labs) (AI scientist platform for materials discovery); [Medra](ecosystem.md#medra) Platform (autonomous drug discovery with Genentech); Emerald Cloud Lab (cloud laboratory infrastructure); academic self-driving labs (MIT, Berkeley, Toronto)

**Gaps**: Scientific data is sparse compared to internet-scale datasets — data efficiency is critical. Experimental "credit assignment" over long horizons (which early decision caused a late failure?). Integrating symbolic scientific knowledge (equations, constraints) with learned world models. Regulatory pathway for AI-designed drugs and materials is undefined. Transfer across scientific domains (chemistry → biology → materials) untested.

---

## Autonomous Agents

**Description**: Autonomous agents that use world models for planning, tool use, and reasoning about action consequences in digital and physical environments.

**Common building blocks** (across all verticals):

| Building Block | Role in this use case |
| -------------- | --------------------- |
| [Latent World Models](building-blocks.md#latent-world-models) | Important — Internal simulation for planning and counterfactual reasoning |
| [Model Serving for Physical AI](building-blocks.md#model-serving-for-physical-ai) | Required — Serve world models during agent inference |
| [Robot Foundation Models](building-blocks.md#robot-foundation-models) | Optional — For embodied agents (physical world interaction) |

### Cross-Industry (Autonomous Agents)

**Verticals**: TBD — Cross-industry (web agents, software agents, embodied agents)

**Additional building blocks**: TBD

**Vertical-specific requirements**:

- **Functional**: TBD — Planning with internal simulation, tool use, multi-step reasoning
- **Non-functional**: TBD
- **Regulatory**: TBD

**Current solutions**: TBD

**Gaps**: TBD

---

## Telecommunications

**Description**: Wireless channel prediction and network optimization using world models to forecast channel state information, manage beams, and optimize interference for next-generation wireless systems.

**Common building blocks** (across all verticals):

| Building Block | Role in this use case |
| -------------- | --------------------- |
| [Latent World Models](building-blocks.md#latent-world-models) | Required — Learn representations of wireless channel states (CSI) |
| [Sensor Data Ingestion](building-blocks.md#sensor-data-ingestion) | Required — Process multi-modal data (RF signals, spatial data, user mobility) |
| [Edge AI Inference Runtime](building-blocks.md#edge-ai-inference-runtime) | Required — Real-time inference for beam management decisions |
| [Model Serving for Physical AI](building-blocks.md#model-serving-for-physical-ai) | Required — Deploy across cell sites and frequency bands |

### Telecommunications (Wireless Optimization)

**Verticals**: Telecommunications

**Additional building blocks**: None beyond common set

**Vertical-specific requirements**:

- **Functional**: Real-time inference on CSI data streams (millisecond-scale beam decisions). Multi-modal fusion (RF signals + spatial data + user mobility). Transfer learning across cell sites and frequency bands. On-premises deployment for telco infrastructure (latency, data sovereignty). Support for 6 downstream tasks from a single model (WirelessJEPA).
- **Non-functional**: Inference latency <10ms for beam management. Support for thousands of base stations (dense urban networks). Transfer across cell sites without retraining.
- **Regulatory**: 3GPP standards (5G/6G), ITU-R (radio regulations)

**Current solutions**: WirelessJEPA (JEPA for 6 wireless tasks); JEPA-MSAC (multi-task wireless sensing); Wireless World Model for 6G (China Mobile/Huawei, multi-modal JEPA + MoE)

**Gaps**: No production deployment of JEPA-based wireless models yet (all academic). Scalability to dense urban networks with thousands of base stations untested. Integration with existing O-RAN and network automation frameworks (e.g., ONAP) undefined. Real-time inference latency requirements for beam management may exceed current model serving capabilities.

---

## Gaming & Simulation

**Description**: Interactive world generation from text and image prompts, creating explorable 3D environments with emergent physics for game development, VFX pre-visualization, and architectural design.

**Common building blocks** (across all verticals):

| Building Block | Role in this use case |
| -------------- | --------------------- |
| [Video Generation / Prediction Models](building-blocks.md#video-generation--prediction-models) | Required — Generate spatiotemporally consistent, interactive environments |
| [Simulation Engines](building-blocks.md#simulation-engines) | Important — Emergent physics learned from observation (not hardcoded) |
| [Model Serving for Physical AI](building-blocks.md#model-serving-for-physical-ai) | Required — Real-time generation for interactive experiences |

### Gaming & Creative Media (Interactive World Generation)

**Verticals**: Gaming & Creative Media

**Additional building blocks**: None beyond common set

**Vertical-specific requirements**:

- **Functional**: Real-time generation (24fps minimum for interactivity). Spatial and temporal consistency over minutes of interaction. User control mapping (latent actions → human inputs). 3D persistence (objects maintain state when camera moves away). High visual fidelity (720p+).
- **Non-functional**: 720p+ at 24fps real-time generation. Minutes-scale consistency. Sub-100ms response to user inputs.
- **Regulatory**: None (creative application)

**Current solutions**: [Google DeepMind](ecosystem.md#google-deepmind) Genie 3 (interactive, 720p/24fps); [World Labs](ecosystem.md#world-labs) Marble (persistent 3D, Chisel editing); Oasis AI (dreamlike interactive worlds); GWM-1 (deterministic spatial coherence)

**Gaps**: Minutes-scale consistency degrades in autoregressive generation. No standard benchmark for interactive world model quality. Compute costs for real-time high-fidelity generation remain prohibitive for consumer deployment. Social/NPC behavior modeling within generated worlds is rudimentary.

---

## Other Applications

*Defense, legal, energy, logistics, etc.*

### Autonomous Drone Coordination and Battlefield Awareness

**Industry**: Defense

**Verticals**: Defense

**Description**: World models enable autonomous coordination of drones and unmanned systems in complex, contested environments. Anduril Industries' Lattice platform uses world-aware reasoning to coordinate autonomous drones and manage battlefield technology, building real-time situational awareness from multi-sensor fusion and predicting adversary behavior through internal simulation.

**Technical Requirements**: Real-time multi-sensor fusion (cameras, radar, RF). Adversary behavior prediction under uncertainty. Edge deployment on constrained hardware (drone-mounted compute). Communication-denied operation (models must function without continuous connectivity). Formal safety verification for autonomous weapons decisions.

**Current Solutions**: Anduril Industries Lattice platform

**Research Gaps**: Adversarial robustness — world models must handle deliberate deception. Ethical and regulatory frameworks for autonomous lethal decision-making. Multi-agent coordination with degraded communications. Transfer from simulation to contested real-world environments.

---

### Counterfactual Accident Reconstruction

**Industry**: Legal

**Verticals**: Legal

**Description**: Counterfactual World Simulation Models (CWSMs) reconstruct accidents in high-fidelity 3D and simulate alternative scenarios (e.g., "would the accident have been avoided if the pedestrian had seen the car?"). CWMDT turns standard video diffusion models into counterfactual world models by constructing digital twins of observed scenes and reasoning over object relationships through an LLM. Used as persuasive evidence for legal fact-finders.

**Technical Requirements**: High-fidelity 3D scene reconstruction from limited evidence (dashcam, surveillance footage). Causal reasoning over object relationships (not just visual generation). Counterfactual simulation with controlled variable manipulation. Expert-explainable outputs suitable for courtroom presentation. Temporal precision (exact timing of driver reactions, braking distances).

**Current Solutions**: CWMDT (digital twin-conditioned video diffusion); CausalVAE (causal inference); Pearl theory-based frameworks

**Research Gaps**: Legal admissibility standards for AI-generated reconstructions are undefined. Bias in world model training data could produce systematically skewed reconstructions. Uncertainty quantification for counterfactual claims needed. No established methodology for validating counterfactual accuracy.

---

**Note**: Each entry follows the use-case-entry template from `templates/use-case-entry.md`.
Use cases include technical requirements, current solutions, and research gaps.
