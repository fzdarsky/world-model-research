# Physical AI Platform Intelligence Plan

> Roadmap for understanding how an enterprise platform vendor could build a Physical AI platform and partner ecosystem

**Created**: 2026-02-26
**Updated**: 2026-06-15
**Focus**: Platform intelligence for Physical AI — building blocks, ecosystem players, use cases, and research depth

## Mission

Understand the Physical AI ecosystem from an **enterprise platform vendor perspective**:

- Which capabilities does a Physical AI platform need? (building blocks)
- Who are the players and what do they offer? (ecosystem)
- What use cases drive adoption? (use cases + technical requirements)
- Where are OSS implementations vs. proprietary solutions? (projects)
- What research breakthroughs are coming? (publications + concepts)

**Goal**: Inform Build vs. Partner vs. Integrate decisions for a Physical AI platform and ecosystem strategy.

## Two-Layer Architecture

### Platform Intelligence Layer

These documents answer **platform strategy questions**:

- **building-blocks.md** - Capability map and solution landscape
- **ecosystem.md** - Players, solutions, reference architectures
- **use-cases.md** - Technical use cases with requirements
- **projects.md** - OSS implementations organized by building block

### Research Depth Layer

These documents provide **technical depth** and **forward-looking intelligence**:

- **publications.md** - Papers, talks, videos on Physical AI
- **concepts.md** - Architectural patterns and technical concepts

## Research Questions

Each document answers specific questions:

### building-blocks.md

**Core Question**: Which capabilities does a Physical AI platform need?

**Specific Questions**:

- What are the essential building blocks? (perception, world models, reasoning, planning, control, simulation, etc.)
- Where is the OSS vs. proprietary divide for each block?
- Which blocks should an enterprise platform vendor Build vs. Partner vs. Integrate?
- What demand matrices show which blocks are critical for which use cases?
- What solution landscapes exist for each block? (vendor offerings, OSS projects, maturity)

**Content**: Platform capability map with demand matrices (use-case × building-block), solution landscapes (vendor/OSS per block), and Build/Partner/Integrate recommendations.

### ecosystem.md

**Core Question**: Who are the key players? What solutions do they offer?

**Specific Questions**:

- Who are the Big Tech players? (NVIDIA, AWS, Microsoft, Google, Meta, etc.)
- Who are the emerging startups? (Physical AI, robotics, simulation, foundation models)
- What OSS communities and research labs drive innovation?
- How do players compete and complement each other?
- What reference architectures are emerging?
- What platform relevance does each player have?

**Content**: Player directory organized by category (Big Tech, startups, OSS, research labs) with solutions, reference architectures, and platform implications.

### use-cases.md

**Core Question**: What technical use cases drive Physical AI adoption?

**Specific Questions**:

- What are the key use cases by industry vertical? (robotics, AVs, healthcare, industrial, telecom, etc.)
- Which building blocks does each use case require?
- What are the quantitative performance objectives and constraints?
- What regulatory requirements apply per vertical?
- Who is working on each use case today?

**Content**: Use cases organized by industry with building-block requirements, regulatory constraints, and current solution providers.

### projects.md

**Core Question**: Which OSS projects implement each building block?

**Specific Questions**:

- What are the reference OSS implementations for each building block?
- What is their community health? (stars, contributors, controlling companies)
- What is their openness? (license, governance, contribution model)
- Where is vendor lock-in risk?
- Which libraries and frameworks are actively maintained?

**Content**: OSS catalog organized by building block with community health metrics, openness analysis, and vendor lock-in risk assessment.

### publications.md

**Core Question**: What research breakthroughs are coming?

**Specific Questions**:

- What are the foundational papers everyone should read?
- What was published in the last 3-6 months?
- What are emerging trends in world models, robot foundation models, sim-to-real?
- Which approaches are gaining momentum vs. being abandoned?
- What talks or blog posts provide good explanations?

**Content**: Papers, talks, videos organized by topic (JEPA, world models, robot foundation models, applications) with summaries and relevance notes.

### concepts.md

**Core Question**: How do world model architectures compare?

**Specific Questions**:

- What defines a "world model"? Generative/pixel vs. predictive/latent?
- What is JEPA? EBMs? How do they work?
- How do different world model architectures compare?
- What is the state of robot foundation models?
- What are the key technical innovations in each area?

**Content**: Deep dives into architectural patterns with technical detail, comparisons, and implications for platform design.

## Content Collection Strategy

### Sources to Monitor

**Academic Papers**:

- arXiv categories: cs.LG, cs.AI, cs.RO, cs.CV
- Conferences: NeurIPS, ICML, ICLR, CoRL, RSS, CVPR
- Researcher pages (Yann LeCun, Fei-Fei Li, Danijar Hafner, etc.)

**Industry & Blogs**:

- Big Tech: NVIDIA, AWS, Microsoft, Google, Meta AI blogs
- Startup blogs: Physical Intelligence, Covariant, Skild AI, Figure AI
- Individual researcher blogs (Karpathy, etc.)

**Ecosystem Intelligence**:

- Startup trackers: Crunchbase, PitchBook (Physical AI, robotics, simulation)
- Industry analyst reports (Gartner, Forrester)
- Platform vendor announcements (NVIDIA Omniverse, AWS RoboMaker, etc.)

**Open Source**:

- GitHub (search: JEPA, world models, robot foundation models, simulation)
- OSS governance bodies: LF AI & Data, ROS, Gazebo ecosystem
- Awesome lists: awesome-world-models, awesome-robotics, awesome-simulation

**Social Media**:

- Twitter/X (researcher and startup announcements)
- Reddit (r/MachineLearning, r/robotics)
- HackerNews

### Collection Methods

**User-Driven (Primary)**:

- User provides specific URLs to add
- User requests searches on specific topics
- User identifies interesting players/projects/use cases

**AI-Assisted**:

- AI searches when user requests (WebSearch tool)
- AI extracts and formats content
- AI suggests related content based on patterns
- AI identifies platform implications and Build/Partner/Integrate opportunities

**No Automated Monitoring (Initially)**:

- No RSS feeds or scheduled checks
- No automated GitHub notifications
- Add automation only if manual process becomes tedious

### Search Queries

**For Papers**:

- "joint embedding predictive architecture", "JEPA"
- "world models", "world foundation models"
- "robot foundation models", "physical AI"
- "model based reinforcement learning"
- "sim-to-real", "digital twin", "embodied AI"
- Author names: "Yann LeCun", "Danijar Hafner", "Fei-Fei Li", etc.

**For Ecosystem Players**:

- "Physical AI startups", "robotics foundation models"
- "NVIDIA Omniverse", "AWS RoboMaker", "Microsoft AirSim"
- "humanoid robotics", "warehouse automation"

**For Projects**:

- GitHub: "JEPA", "world model", "dreamer", "Isaac Sim"
- Awesome lists: "awesome-world-models", "awesome-robotics", "awesome-simulation"
- OSS foundations: ROS 2, Gazebo, PyBullet

**For Use Cases**:

- "world models" + industry vertical
- "robot foundation models" + vertical
- Company tech blogs + "Physical AI" or "robotics"

## Maintenance Approach

### Continuous (As Content is Discovered)

- User provides URLs → AI adds entries
- New papers mentioned → AI adds to publications.md
- New players mentioned → AI adds to ecosystem.md
- New OSS projects → AI adds to projects.md with community health analysis
- Cross-linking as connections emerge

### Weekly Review (If Active)

- Review quality of recent additions
- Move items from "Recent Additions" to topic sections in publications.md
- Check for broken links
- Ensure cross-links are complete
- Update OSS project stats (stars, contributors, last commit)

### Bi-Weekly Ecosystem Check

- Scan startup news (acquisitions, funding rounds, product launches)
- Update ecosystem.md with new players or major developments
- Check for new reference architectures or platform announcements

### Monthly Synthesis

**Research Depth**:

- Identify patterns across recent papers
- Update concepts.md with new architectural insights
- Synthesize trends in world models and robot foundation models

**Platform Intelligence**:

- Review building-block landscape: any new OSS solutions? vendor offerings?
- Update use-case demand matrices: which use cases are gaining traction?
- Update Build/Partner/Integrate recommendations based on new data

**Ecosystem**:

- Update player recent work and affiliations
- Review competitive dynamics and reference architectures

### Quarterly Review

- Major synthesis of research and ecosystem trends
- Reorganize sections if needed
- Archive outdated content
- Assess whether to add automation tools
- Review platform strategy implications: any shifts in Build/Partner/Integrate recommendations?
