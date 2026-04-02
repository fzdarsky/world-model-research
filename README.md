# AI World Models Research Notebook

A personal research notebook tracking AI world models research — both foundational and applied. Guided by my own interests, with no claim to be representative, state-of-the-art, or correct. Content is curated through an AI-assisted workflow: I provide URLs or search terms, and AI extracts information, fills templates, and updates documents. Just markdown files and AI assistance — no external tools required.

## What Are World Models?

World models are AI systems that learn internal representations of how the world works — its dynamics, structure, and rules — enabling prediction, planning, and decision-making without exhaustive trial-and-error in the real world.

**Why they matter**: Current AI systems (LLMs, vision models) excel at pattern recognition but lack causal understanding of physical dynamics. World models aim to close this gap — enabling robots to predict the consequences of actions before executing them, autonomous vehicles to anticipate traffic scenarios, and scientific simulations to run orders of magnitude faster than physics solvers.

**Two broad families**:

- **Generative / pixel-space**: Predict raw observations (video frames, images). Learn to simulate what the world *looks like*. Examples: NVIDIA Cosmos, Google Genie, Wayve GAIA, OpenAI Sora. Strength: rich visual output directly usable for training downstream policies. Challenge: computationally expensive, prone to hallucinating visual details irrelevant to dynamics.

- **Predictive / latent-space**: Predict in learned abstract representation spaces, discarding pixel-level detail. Learn to model what *will happen* without reconstructing every pixel. Examples: JEPA (I-JEPA, V-JEPA), Dreamer, Energy-Based Models. Strength: computationally efficient, focuses on task-relevant dynamics. Challenge: latent representations are harder to interpret and validate.

Many practical systems combine both — using generative models for synthetic data and sim-to-real transfer, while using latent models for real-time planning and control.

## Research Documents

**[concepts.md](research/concepts.md)** - Deep dives into fundamental concepts: JEPA, Energy-Based Models, generative vs. predictive approaches, world model architectures, and how they relate.

**[publications.md](research/publications.md)** - Papers, talks, blog posts, and videos organized by topic: JEPA, EBMs, world models & model-based RL, applications, and foundational theory.

**[players.md](research/players.md)** - Seminal contributors and recognized thought leaders: researchers, institutions, and companies driving world models research and commercialization.

**[projects.md](research/projects.md)** - Open-source implementations, frameworks, datasets, and benchmarks: JEPA variants, world model frameworks (Cosmos, Dreamer, etc.), and supporting tools.

**[use-cases.md](research/use-cases.md)** - Applications by industry: robotics, autonomous vehicles, healthcare, industrial digital twins, telecommunications, gaming, scientific discovery, and agentic AI.

## Getting Started

### Slash Commands

**`/add <url>`** - Add a paper, project, video, or other content

```text
/add https://arxiv.org/abs/2602.03604
/add https://github.com/facebookresearch/jepa
/add https://www.youtube.com/watch?v=...
```

**`/search <topic>`** - Search for papers and projects

```text
/search JEPA
/search world models robotics
/search video prediction autonomous driving
```

**`/sources`** - Check preferred sources for new content (last 30 days)

**`/synthesize`** - Review recent additions, identify patterns, update concepts.md

### Natural Language

```text
"Add this paper: https://arxiv.org/abs/2602.03604"
"Find recent papers on world foundation models"
"What are the key themes across latent world models?"
```

### Search Queries to Try

- "world models", "world foundation models", "physical AI"
- "JEPA" or "joint embedding predictive architecture"
- "energy based models" + "world models"
- "video prediction", "video generation", "Cosmos", "Genie"
- "model based reinforcement learning", "Dreamer"
- Researcher names: "Yann LeCun", "Danijar Hafner", "Fei-Fei Li"

### Templates

All entries follow consistent templates in **[research/templates/](research/templates/)**.

## License

Research notes and summaries for personal/educational use. Papers and external content retain original authors' rights.
