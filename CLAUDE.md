# AI Assistant Guidelines for World Models Research Notebook

## Project Purpose

This is a living research notebook tracking AI world models research — both foundational and applied — with focus on:

**Architectures & Methods** (examples, not exhaustive):

- **Predictive / latent-space models** - JEPA, Dreamer, Energy-Based Models — predict in abstract representation spaces
- **Generative / pixel-space models** - Cosmos, Genie, GAIA, Sora — generate raw video/image observations
- **Model-based RL** - DreamerV3, TD-MPC, MBPO — learn dynamics for planning and control
- **Foundation models for Physical AI** - GR00T, pi0, world foundation models for robotics
- **Biologically-inspired architectures** - BDH, Active Inference, spiking networks

**Applications & Industry Use Cases**:

- **Robotics** - Manipulation, navigation, task planning with world models
- **Autonomous vehicles** - Driving, sim-to-real transfer, scene prediction
- **Healthcare & medical imaging** - Clinical decision support, diagnostic AI
- **Industrial & manufacturing** - Digital twins, process optimization, predictive maintenance
- **Telecommunications** - Wireless channel modeling, network optimization
- **Scientific discovery** - Physics simulation, molecular modeling
- **Agentic AI** - Autonomous agents, web agents, tool use, planning with world models

### Goals

1. Maintain current understanding of SOTA research and key players
2. Track open-source implementations and communities
3. Identify practical use cases, technical requirements, and industry adoption
4. Support synthesis and analysis of research trends

### Workflow Philosophy

This notebook is **AI-driven**: the user provides URLs or search terms, and AI assistants extract information, fill templates, and update documents. The goal is minimal manual intervention while maintaining high quality and consistency.

## AI Workflow for Adding Content

### Adding a Publication

When the user provides a publication URL (paper, blog post, video, etc.):

1. **Fetch Content**: Use WebFetch tool to retrieve the content
2. **Extract Information**:
   - Title
   - Authors/Presenter
   - Publication date (YYYY-MM format)
   - URL
   - Type (Paper | Talk | Blog Post | Video)
   - Duration (for videos, format: MM:SS or HH:MM:SS)
   - 2-3 sentence summary (following style guide)
   - 3-5 key points (technical contributions, methods, results, key insights)
   - Relevance to world models research
3. **For YouTube Videos**:
   - Only include videos from well-known players/institutions
   - Types: talks, interviews, news about key players, tutorials
   - Include key timestamps if valuable sections are identified
4. **Fill Template**: Use `research/templates/publication-entry.md` as structure
   - Add a 32x32 icon behind the title that links to the source. Pick the icon from `research/templates/icons/` depending on the source type.
5. **Add to publications.md**: Insert under appropriate section (see Content Organization below)
6. **Cross-link**:
   - If paper mentions new researchers/institutions → add to ecosystem.md
   - If paper describes new use cases → add to use-cases.md
   - If paper presents new concept → note in concepts.md
   - If any authors/presenters already exist in ecosystem.md, link their names: `[Name](ecosystem.md#anchor)`

### Adding a Player

Only add researchers, institutions, or companies that have made **seminal contributions** to the field or are **recognized as thought leaders**. Do not add authors merely because they co-authored a tracked paper.

When extracting researcher, institution, or company information:

1. **Assess Inclusion**: Only add if the person/organization meets at least one criterion:
   - Originated or significantly advanced a key concept (JEPA, EBMs, world models, BDH)
   - Leads a major research group or company in the field
   - Has a body of highly-cited, influential work in the area
2. **Extract Information**:
   - Name/Organization
   - About (1-3 sentences: bio, why particularly relevant to the field)
   - Focus areas (specific topics like "JEPA, self-supervised learning")
   - Key work (notable papers, projects, products)
   - Collaborations (with other key players)
   - Links (website, GitHub, Google Scholar, Twitter)
3. **Fill Template**: Use `research/templates/ecosystem-entry.md`
4. **Add to ecosystem.md**: Insert under appropriate section (Big Tech | Startups | OSS Communities | Research Labs)
5. **Avoid Duplicates**: Check if entry already exists before adding

### Adding a Project

When the user provides a GitHub URL or project website:

1. **Fetch Information**: Use WebFetch or Bash to get repo/project details
2. **Extract Information**:
   - Project name
   - URL (GitHub or website)
   - Description (what it does, 1-2 sentences)
   - Tech Stack (which technologies does it use or depend on)
   - Key features (what makes it notable)
   - Status (Active | Maintained | Archived) - check last commit/release date
   - Stats (stars, forks, number of recent contributors, key contributing companies - to understand community health and controlling companies)
   - Last updated date
3. **Fill Template**: Use `research/templates/project-entry.md`
4. **Add to projects.md**: Insert under appropriate category

### Adding a Use Case

When identifying an application or industry use of world models:

1. **Structure Information**:
   - Use case name
   - Industry vertical (Manufacturing, Transport&Logistics, Energy&Utilities, Healthcare, Telecommunications, Retail, FSI, etc.)
   - Description
   - Technical requirements (functionality it requires, quantitative performance objectives or constraints, etc.)
   - Current solutions (companies/projects working on this)
   - Research gaps (what's missing or needs improvement)
2. **Fill Template**: Use `research/templates/use-case-entry.md`
3. **Add to use-cases.md**: Insert under appropriate industry section

## Search Strategy

When the user asks to find content on a topic (e.g., "find recent papers on JEPA"):

1. **Use WebSearch** for:
   - Recent papers and preprints
   - Blog posts and articles
   - News and announcements
   - Industry developments

2. **Search GitHub** (via WebSearch or direct queries) for:
   - Open-source implementations
   - Research code releases
   - Popular frameworks

3. **Search arXiv** specifically:
   - Use search terms like: `"joint embedding predictive architecture"`, `"energy based models"`, `"world models"`, `"dragon hatchling"`
   - Filter by recent submissions (last 3-6 months)
   - Look for papers from key researchers

4. **Present Findings**: Show user a list of top 5-10 results with titles and brief descriptions, ask which to add

## Content Organization

### publications.md Structure

Organize by **topic**, not chronologically:

```markdown
# Publications: Papers, Talks, Videos, and Blog Posts

## JEPA (Joint-Embedding Predictive Architecture)
[Papers, talks, videos related to JEPA]

## Energy-Based Models
[Papers, talks, videos on EBMs]

## Dragon Hatchling (BDH)
[Research on Baby Dragon Hatchling models]

## World Models & Model-Based RL
[Papers on world models, DreamerV3, etc.]

## Applications & Use Cases
[Papers demonstrating practical applications — robotics, AV, healthcare, industrial, telecom, scientific discovery]

## Foundational / Theory
[Theoretical foundations, surveys, position papers]

## Recent Additions
[Last 30 days - move to topic sections after monthly review]
```

**Video Guidelines**:

- Only include videos from well-known researchers, institutions, or reputable channels
- Types: conference talks, interviews, news coverage, technical tutorials
- Include duration and key timestamps if applicable

### ecosystem.md Structure

Organize by **player type**:

```markdown
# Ecosystem

## Big Tech
[Established tech companies with Physical AI initiatives — with solution sub-entries]

## Startups
[Venture-backed companies building Physical AI products]

## OSS Communities
[Open-source communities and foundations]

## Research Labs
[Universities and research institutions — with key researchers grouped under their labs]
```

### projects.md Structure

Organize by **category**:

```markdown
# Open Source and Open Data Projects

## JEPA Implementations
[Projects implementing JEPA]

## EBM Libraries & Frameworks
[EBM-related tools]

## World Model Frameworks
[DreamerV3, etc.]

## Datasets & Benchmarks
[Relevant datasets]

## Utilities & Tools
[Supporting tools]
```

### use-cases.md Structure

Organize by **industry vertical**:

```markdown
# Use Cases

## Robotics
[Manipulation, navigation, task planning]

## Autonomous Vehicles
[Self-driving, path planning, sim-to-real]

## Healthcare & Medical Imaging
[Diagnostics, clinical decision support, surgical planning]

## Industrial & Manufacturing
[Digital twins, process optimization, predictive maintenance]

## Telecommunications
[Wireless channel modeling, network optimization, beam prediction]

## Gaming & Simulation
[Game AI, virtual worlds, procedural generation]

## Scientific Discovery
[Physics simulation, molecular modeling, materials design]

## Agentic AI
[Autonomous agents, web agents, tool use, planning with world models]

## Other Applications
[Finance, energy, logistics, etc.]
```

## Style Guide

All content must follow these principles:

### 1. Sober and Factual

**Do**: State facts, cite specific results, use measured language
**Don't**: Use hype, marketing language, superlatives without evidence

- ❌ "This groundbreaking paper revolutionizes AI..."
- ✅ "Introduces variance-invariance-covariance regularization, achieving 72.3% on ImageNet without labels"

### 2. Concise

**Do**: Dense information, respect reader's time
**Don't**: Verbose explanations, unnecessary background

- ❌ "The paper explores various approaches and after extensive experimentation, the authors found that..."
- ✅ "Compares contrastive, predictive, and masked approaches; finds joint-embedding + variance regularization most effective"

### 3. Pattern-Oriented

**Do**: Highlight connections, relationships, recurring themes
**Don't**: Treat each paper/project in isolation

- ❌ "This paper uses a transformer architecture"
- ✅ "Extends V-JEPA's masking strategy to text-image pairs, similar to CLIP but with predictive rather than contrastive loss"

### 4. Assume Experience

**Audience**: Decades of research/engineering experience, new to AI

**Do explain**:

- AI-specific terminology (embeddings, attention, latent space)
- Why an approach differs from alternatives
- Architectural innovations

**Don't explain**:

- Basic programming concepts
- General research methodology
- Standard math/statistics

### 5. Technical Precision

**Do**: Use precise technical terms, cite specific architectures, include key equations
**Don't**: Vague descriptions, hand-waving

- ❌ "Uses a clever trick to prevent mode collapse"
- ✅ "Prevents collapse via VICReg regularization: variance preservation (hinge loss), invariance to augmentations (MSE), and covariance decorrelation"

### 6. Actionable

**Do**: Include enough detail for reader to dive deeper or implement
**Don't**: Surface-level summaries without substance

**Good summary includes**:

- Specific method names/architectures
- Key hyperparameters or design choices
- Links to code if available
- Performance metrics with dataset context

### 7. Markdown Formatting

Follow standard markdown linting rules (markdownlint). In particular:

- Blank lines before and after headings, fenced code blocks, and lists
- Language specifier on all fenced code blocks (e.g. ` ```python `, ` ```markdown `, ` ```text `)
- No trailing whitespace or multiple consecutive blank lines

**After making changes to Markdown files**: Run `npx markdownlint-cli "**/*.md" --ignore node_modules` to check for linting issues. Fix all errors before committing.

## Quality Standards

Before adding content, verify:

- [ ] **Accurate extraction**: Information matches source material
- [ ] **Concise summary**: 2-3 sentences, no fluff
- [ ] **Clear relevance**: Obvious connection to world models research
- [ ] **Proper linking**: Cross-references to related entries
- [ ] **Style guide adherence**: Follows all 6 principles above
- [ ] **No duplicates**: Entry doesn't already exist

## When to Update vs. Add

### Add New Entry When

- First time encountering a paper, project, or player
- Genuinely new use case or application
- New development from existing player (e.g., new paper from known researcher)

### Update Existing Entry When

- Project status changes (Active → Archived)
- Player changes affiliation or focus
- Use case evolves or new solutions emerge
- Correcting errors or adding missing information

## Maintenance Tasks

### Weekly (If Active)

- Review recent additions for quality
- Move items from "Recent Additions" to topic sections
- Check for broken links

### Monthly

- Synthesize new insights into concepts.md
- Update player affiliations and recent work
- Archive or update stale use cases

### As Needed

- Reorganize sections if structure becomes unwieldy
- Add new categories as research expands

## Getting Started

The user can interact with this notebook through:

### Slash Commands (Preferred)

- **`/add <url>`** - Add a paper, project, or other content from a URL
- **`/search <topic>`** - Search for papers/projects on a topic, present results, ask which to add
- **`/sources`** - Check preferred sources (arXiv, GitHub, blogs) for new content in last 30 days
- **`/synthesize`** - Review recent additions, identify patterns, update concepts.md, organize entries

See `.claude/skills/` for detailed implementation of each command.

### Natural Language

1. **Providing URLs**: "Add this paper: `https://arxiv.org/abs/...`"
2. **Requesting searches**: "Find recent papers on JEPA"
3. **Asking for synthesis**: "What are the key themes in EBM research?"

## AI Assistant Role

As AI assistant, your role is to:

- Fetch and extract information accurately
- Apply templates consistently
- Maintain style guide standards
- Cross-link related content
- Keep documents organized and scannable

When using slash commands, follow the detailed instructions in the skill files (`.claude/skills/`).
