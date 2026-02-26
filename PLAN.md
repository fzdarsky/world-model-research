# World Models Research Plan

> Roadmap for building comprehensive understanding of AI world models, JEPA, and Energy-Based Models

**Created**: 2026-02-26
**Focus**: JEPA, Energy-Based Models, Autonomous Systems

## Research Questions

Each research document answers specific questions:

### concepts.md

**Core Question**: What are the fundamental concepts underlying world models research?

**Specific Questions**:
- What is JEPA? How does it work? Why does it matter?
- What are Energy-Based Models? How do they differ from likelihood-based models?
- What defines a "world model"? What approaches exist?
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

## Deliverable Specifications

### 1. One-Pager: "What are world models and why should you care?"

**Target Audience**: Technical executives, product managers, investors with engineering background

**Purpose**: 5-minute read that motivates further exploration and investment in world models

**Length**: 1-2 pages (800-1200 words)

**Required Sections**:

1. **The Problem** (2-3 paragraphs)
   - Current limitations of AI systems (data efficiency, generalization)
   - Why world models matter now (embodied AI, robotics, autonomous systems)
   - What's different from prior approaches

2. **The Solution** (3-4 paragraphs)
   - What world models are (internal representation of environment dynamics)
   - Key approaches: JEPA, EBM, others
   - Technical differentiators (self-supervised, predictive, latent space)
   - Include 1-2 clear diagrams

3. **The Opportunity** (2-3 paragraphs)
   - Killer applications (robotics manipulation, autonomous navigation, planning)
   - Market sizing and growth potential
   - Who's investing (Meta AI, research labs, companies)

4. **Key Players** (bullet list)
   - Top 5 researchers and their contributions
   - Top 5 institutions/companies

5. **Next Steps** (bullet list)
   - 3-5 must-read papers
   - 2-3 GitHub projects to explore
   - Upcoming conferences/workshops

**Quality Bar**:
- Cite 5-7 key papers
- Include 1-2 clear diagrams
- No jargon without explanation
- Compelling narrative arc
- Factual, not hype-driven

**Source Documents**: Synthesize from concepts.md + publications.md + use-cases.md + players.md

### 2. Investment Brief

**Target Audience**: VCs, corporate strategy, R&D leadership

**Purpose**: Inform investment/partnership decisions in world models space

**Length**: 10-15 pages

**Required Sections**:

1. **Executive Summary** (1 page)
   - Investment thesis in 2-3 sentences
   - Key opportunities and risks
   - Recommended actions

2. **Market Analysis** (3-4 pages)
   - TAM/SAM/SOM for world model applications
   - Market segmentation by vertical
   - Competitive landscape
   - Technology adoption curve positioning
   - 5-year market projections

3. **Technical Assessment** (3-4 pages)
   - Maturity of JEPA/EBM research (TRL levels)
   - Engineering readiness for production
   - Key technical risks and mitigations
   - Comparison of approaches (JEPA vs. others)
   - Open problems and research gaps

4. **Key Players** (2-3 pages)
   - Leading researchers and their trajectories
   - Strong institutions and their focus
   - Companies to watch (research, products, talent)
   - Collaboration networks and influence

5. **Use Cases & Applications** (2-3 pages)
   - Detailed analysis of 3-5 high-potential use cases
   - Technical requirements vs. current capabilities
   - Go-to-market challenges
   - Revenue models and unit economics

6. **Investment Thesis** (2 pages)
   - Why now? (timing factors, recent breakthroughs)
   - Competitive moats and advantages
   - Risk/return profile
   - Recommended investment vehicles (companies, research partnerships, acqui-hires)
   - Exit scenarios and timelines

**Quality Bar**:
- 15+ company profiles
- Financial models and projections (where applicable)
- Competitive analysis with specific differentiation
- Technical accuracy validated against papers
- Clear investment recommendations

**Source Documents**: All research documents + external market data + financial modeling

### 3. Proof of Concept (PoC) Plan

**Target Audience**: Engineering teams, research scientists, technical leadership

**Purpose**: Blueprint for demonstrating world model capabilities

**Length**: 8-12 pages

**Required Sections**:

1. **Executive Summary** (1 page)
   - Selected use case and rationale
   - Success criteria (quantitative metrics)
   - Timeline and resource summary
   - Expected outcomes

2. **Use Case Selection** (2 pages)
   - Evaluation of candidate use cases
   - Selection criteria (feasibility, impact, learning)
   - Chosen use case detailed description
   - Success metrics definition

3. **Requirements** (2 pages)
   - Functional requirements
   - Performance requirements (latency, accuracy, etc.)
   - Data requirements (datasets, volume, quality)
   - Infrastructure requirements (compute, storage)
   - Risk assessment and mitigations

4. **Technical Architecture** (3-4 pages)
   - System design overview (diagram)
   - Model architecture (JEPA/EBM variant selection)
   - Data pipeline design
   - Training approach and hyperparameters
   - Evaluation framework
   - Baseline comparisons

5. **Implementation Plan** (2-3 pages)
   - Phased development approach (milestones)
   - Technology stack and dependencies
   - Open-source components to leverage
   - Team composition and roles
   - Development timeline (weeks)
   - Budget estimate (compute, data, personnel)

6. **Success Criteria** (1 page)
   - Quantitative metrics and targets
   - Qualitative assessment criteria
   - Comparison to baselines
   - Go/no-go decision points

**Quality Bar**:
- Executable in 3-6 months with small team
- Clear, measurable success criteria
- Builds on existing open-source work
- Demonstrates unique capability or insight
- Realistic resource estimates

**Source Documents**: use-cases.md + projects.md + publications.md (technical approaches)

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

### Quarterly Milestones

- Create or update a deliverable
- Major synthesis of research trends
- Reorganize sections if needed
- Archive outdated content
- Assess whether to add automation tools

## Timeline & Milestones

### Month 1: Foundation

**Goal**: Establish core knowledge base

- [ ] Add 10-15 foundational papers
- [ ] Populate concepts.md with JEPA, EBM, World Models sections
- [ ] Identify and add top 10 researchers
- [ ] Find and catalog 5-10 open-source projects
- [ ] Document 3-5 use cases

**Outcome**: Can explain JEPA/EBM at technical level, know the key players

### Month 2: Deep Dive

**Goal**: Develop comprehensive understanding

- [ ] Add 20-30 additional papers (mix of classic and recent)
- [ ] Expand concept files with technical depth
- [ ] Add 20+ more players (researchers, institutions, companies)
- [ ] Catalog 10+ more open-source projects
- [ ] Document 5-10 more use cases across industries

**Outcome**: Expert-level knowledge, ready to create one-pager

### Month 3: First Deliverable

**Goal**: Synthesize knowledge into one-pager

- [ ] Create "What are world models and why should you care?" one-pager
- [ ] Continue adding papers (10-15 new ones)
- [ ] Monitor for recent developments
- [ ] Refine use cases based on new information

**Outcome**: Shareable one-pager, maintained research notebook

### Month 4-6: Market Analysis & PoC Design

**Goal**: Prepare investment brief and PoC plan

- [ ] Deep dive into market sizing and opportunity analysis
- [ ] Company and product research (20+ companies)
- [ ] Technical feasibility assessment
- [ ] Draft investment brief
- [ ] Select and spec PoC use case
- [ ] Draft PoC implementation plan

**Outcome**: Complete investment brief, executable PoC plan

## Success Metrics

### Content Volume

- Papers: 50+ detailed summaries
- Players: 30+ researchers, 10+ institutions, 10+ companies
- Projects: 25+ cataloged with status
- Use cases: 15+ across different industries
- Concepts: 3-5 comprehensive deep dives

### Content Quality

- All entries follow style guide
- Cross-links maintained
- No broken URLs
- Summaries are actionable and technical
- Patterns and relationships identified

### Deliverable Quality

- One-pager: Shareable with executives, clear value prop
- Investment brief: VC-grade analysis, defensible projections
- PoC plan: Engineering team can execute

### Usability

- Can quickly find information on any topic
- Documents are scannable (good headers, organization)
- New content integrates smoothly
- AI workflow is efficient

## Next Steps

1. **Immediately**: Begin adding foundational papers and key players
2. **Week 1**: Add 5 foundational papers, 5 key researchers, 3 projects
3. **Week 2**: Establish weekly review routine
4. **Week 4**: Assess if any automation or tools are needed
5. **Month 3**: Create first deliverable (one-pager)
