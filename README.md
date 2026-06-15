# Physical AI Platform Intelligence Notebook

A research notebook for understanding the Physical AI ecosystem — architectures, building blocks, players, and platforms — from an enterprise platform vendor perspective. Tracks both foundational research and applied systems to inform Build vs. Partner vs. Integrate decisions. Guided by my own interests, with no claim to be representative, state-of-the-art, or correct. Content is curated through an AI-assisted workflow: I provide URLs or search terms, and AI extracts information, fills templates, and updates documents. Just markdown files and AI assistance — no external tools required.

## What Is Physical AI?

Physical AI refers to AI systems that perceive, reason about, and interact with the physical world — enabling robots, autonomous vehicles, industrial systems, and embodied agents to operate in unstructured, dynamic environments. Unlike purely digital AI (LLMs, recommender systems), Physical AI must:

- **Perceive** the world through sensors (cameras, lidar, proprioception)
- **Build internal models** of dynamics, physics, and causality
- **Reason and plan** about actions in a physical space
- **Control** actuators (robot arms, wheels, drones) with precision
- **Learn from interaction** in the real world or high-fidelity simulation

**Why it matters for enterprise platforms**: Physical AI is emerging as a platform opportunity — similar to how cloud platforms enabled web/mobile apps, Physical AI platforms could enable a new generation of robotics, industrial automation, and embodied AI applications. Understanding the ecosystem is critical for Build vs. Partner vs. Integrate decisions.

## What Are World Models?

World models are a **core building block** of Physical AI. They are AI systems that learn internal representations of how the world works — its dynamics, structure, and rules — enabling prediction, planning, and decision-making without exhaustive trial-and-error in the real world.

**Why they matter**: Current AI systems (LLMs, vision models) excel at pattern recognition but lack causal understanding of physical dynamics. World models aim to close this gap — enabling robots to predict the consequences of actions before executing them, autonomous vehicles to anticipate traffic scenarios, and scientific simulations to run orders of magnitude faster than physics solvers.

**Two broad families**:

- **Generative / pixel-space**: Predict raw observations (video frames, images). Learn to simulate what the world *looks like*. Examples: NVIDIA Cosmos, Google Genie, Wayve GAIA, OpenAI Sora. Strength: rich visual output directly usable for training downstream policies. Challenge: computationally expensive, prone to hallucinating visual details irrelevant to dynamics.

- **Predictive / latent-space**: Predict in learned abstract representation spaces, discarding pixel-level detail. Learn to model what *will happen* without reconstructing every pixel. Examples: JEPA (I-JEPA, V-JEPA), Dreamer, Energy-Based Models. Strength: computationally efficient, focuses on task-relevant dynamics. Challenge: latent representations are harder to interpret and validate.

Many practical systems combine both — using generative models for synthetic data and sim-to-real transfer, while using latent models for real-time planning and control.

## Research Documents

### Platform Intelligence Layer

These documents answer **platform strategy questions**:

**[building-blocks.md](research/building-blocks.md)** - Platform capability map with demand matrices (use-case × building-block), solution landscapes (vendor/OSS per block), and Build/Partner/Integrate recommendations.

**[ecosystem.md](research/ecosystem.md)** - Players in Physical AI — Big Tech, startups, OSS communities, and research labs — their solutions, reference architectures, and platform relevance.

**[use-cases.md](research/use-cases.md)** - Technical use cases by industry vertical with building-block requirements, regulatory constraints, and current solution providers.

**[projects.md](research/projects.md)** - Open-source implementations organized by building block, with community health metrics, openness analysis, and vendor lock-in risk assessment.

### Research Depth Layer

These documents provide **technical depth** and **forward-looking intelligence**:

**[publications.md](research/publications.md)** - Papers, talks, blog posts, and videos on Physical AI: world models, robot foundation models, sim-to-real, applications, and foundational theory.

**[concepts.md](research/concepts.md)** - Deep dives into architectural patterns: JEPA, Energy-Based Models, generative vs. predictive world models, robot foundation models, and how they relate.

## Getting Started

### Slash Commands

**`/add <url>`** - Add a paper, project, player, video, or other content

```text
/add https://arxiv.org/abs/2602.03604
/add https://github.com/NVlabs/Cosmos
/add https://www.youtube.com/watch?v=...
/add https://www.nvidia.com/en-us/solutions/robotics/
```

**`/search <topic>`** - Search for papers, projects, and players

```text
/search robot foundation models
/search Physical AI startups
/search NVIDIA Omniverse
/search world models healthcare
```

**`/sources`** - Check preferred sources for new content (last 30 days)

**`/synthesize`** - Review recent additions, identify patterns, update concepts.md and building-blocks.md

**Specialist skills** available for targeted research:

- Use `/add` for individual items
- Use `/search` for broader topic exploration
- Use natural language for synthesis, analysis, and platform strategy questions

### Natural Language

```text
"Add this paper: https://arxiv.org/abs/2602.03604"
"Find recent Physical AI startups"
"What are the key ecosystem players in simulation?"
"Which building blocks should we Build vs. Partner for warehouse robotics?"
"What are the emerging trends in robot foundation models?"
```

### Search Queries to Try

**Research & Concepts**:

- "world models", "world foundation models", "physical AI"
- "robot foundation models", "embodied AI"
- "JEPA", "energy based models"
- "video prediction", "Cosmos", "Genie"
- "sim-to-real", "digital twin"

**Ecosystem & Players**:

- "Physical AI startups", "robotics foundation models"
- "NVIDIA Omniverse", "AWS RoboMaker", "Microsoft AirSim"
- "humanoid robotics", "warehouse automation"
- Researcher names: "Yann LeCun", "Danijar Hafner", "Fei-Fei Li"

**Use Cases & Applications**:

- "world models robotics", "robot foundation models healthcare"
- "autonomous vehicles world models", "industrial digital twin"
- "warehouse robotics", "surgical robotics"

### Templates

All entries follow consistent templates in **[research/templates/](research/templates/)**.

## License

Research notes and summaries for personal/educational use. Papers and external content retain original authors' rights.
