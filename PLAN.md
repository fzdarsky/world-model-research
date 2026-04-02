# World Models Research Plan

> Roadmap for building comprehensive understanding of AI world models research — both foundational and applied

**Created**: 2026-02-26
**Focus**: World models across architectures (predictive/latent, generative/pixel), applications, and industry adoption

## Research Questions

Each research document answers specific questions:

### concepts.md

**Core Question**: What are the fundamental concepts underlying world models research?

**Specific Questions**:

- What defines a "world model"? What approaches exist (generative/pixel vs. predictive/latent)?
- What is JEPA? How does it work? Why does it matter?
- What are Energy-Based Models? How do they differ from likelihood-based models?
- How do generative world models (Cosmos, Genie, GAIA) differ from latent models (JEPA, Dreamer)?
- How do these concepts relate to each other?
- What are the key technical innovations in each area?

**Content**: Deep dives into core concepts with technical detail, equations, architectural diagrams, and comparisons to alternatives.

### publications.md

**Core Question**: What are the important papers, talks, and blog posts? What are the latest developments?

**Specific Questions**:

- What are the foundational papers everyone should read?
- What was published in the last 3-6 months?
- What are emerging trends and debates?
- Which approaches are gaining momentum vs. being abandoned?
- What talks or blog posts provide good explanations?

**Content**: Organized collection of papers/talks/blogs with summaries, key points, and relevance notes. Grouped by topic, not chronology.

### players.md

**Core Question**: Who are the key researchers, institutions, and companies working on world models?

**Specific Questions**:

- Who are the leading researchers in JEPA/EBM/world models?
- Which institutions have strong programs in this area?
- What companies are investing in world model research or products?
- What are their recent contributions and focus areas?
- How do the research groups connect and collaborate?

**Content**: Directory of researchers, labs, and companies with their focus areas, key work, and links.

### projects.md

**Core Question**: What implementations and tools are available?

**Specific Questions**:

- What are the reference implementations of JEPA/EBM?
- Which libraries and frameworks are actively maintained?
- What datasets and benchmarks exist?
- Where are the research communities gathering?
- What's the maturity/quality of available implementations?

**Content**: Catalog of GitHub repos, frameworks, datasets, and communities with status updates.

### use-cases.md

**Core Question**: Where are world models being applied? What are the requirements?

**Specific Questions**:

- What are the killer applications for world models?
- What technical requirements must be met for each use case?
- Who is working on each application area?
- What are the current limitations and research gaps?
- Which industries show most adoption potential?

**Content**: Use cases organized by industry vertical with technical requirements and current solutions.

## Content Collection Strategy

### Sources to Monitor

**Academic Papers**:

- arXiv categories: cs.LG, cs.AI, cs.RO, cs.CV
- Conferences: NeurIPS, ICML, ICLR, CoRL, RSS
- Researcher pages (Yann LeCun, etc.)

**Industry & Blogs**:

- Meta AI Blog
- DeepMind Blog
- OpenAI Blog
- Individual researcher blogs (Karpathy, etc.)

**Open Source**:

- GitHub (search: JEPA, world models, EBM)
- Meta AI Research GitHub
- Active robotics/RL organizations

**Social Media**:

- Twitter/X (researcher announcements)
- Reddit (r/MachineLearning)
- HackerNews

### Collection Methods

**User-Driven (Primary)**:

- User provides specific URLs to add
- User requests searches on specific topics
- User identifies interesting players/projects

**AI-Assisted**:

- AI searches when user requests (WebSearch tool)
- AI extracts and formats content
- AI suggests related content based on patterns

**No Automated Monitoring (Initially)**:

- No RSS feeds or scheduled checks
- No automated GitHub notifications
- Add automation only if manual process becomes tedious

### Search Queries

**For Papers**:

- "joint embedding predictive architecture"
- "energy based models" + "world models"
- "self-supervised learning" + "representation"
- "model based reinforcement learning"
- Author names: "Yann LeCun", "Danijar Hafner", etc.

**For Projects**:

- GitHub: "JEPA", "world model", "dreamer"
- Awesome lists: "awesome-world-models", "awesome-robotics"

**For Use Cases**:

- "world models" + "robotics"
- "predictive models" + industry vertical
- Company tech blogs

## Maintenance Approach

### Continuous (As Content is Discovered)

- User provides URLs → AI adds entries
- New papers mentioned in papers → AI adds to publications.md
- New players mentioned → AI adds to players.md
- Cross-linking as connections emerge

### Weekly Review (If Active)

- Review quality of recent additions
- Move items from "Recent Additions" to topic sections in publications.md
- Check for broken links
- Ensure cross-links are complete

### Monthly Synthesis

- Identify patterns across recent papers
- Update concepts.md with new insights
- Synthesize trends in state-of-the-art
- Update player recent work and affiliations
- Review and update use case current solutions

### Quarterly Review

- Major synthesis of research trends
- Reorganize sections if needed
- Archive outdated content
- Assess whether to add automation tools
