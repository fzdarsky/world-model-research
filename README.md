# AI World Models Research Notebook

> A living knowledge base tracking research in AI world models, with focus on JEPA, Energy-Based Models, and BDH.

**Last Updated**: 2026-02-26
**Primary Focus**: JEPA, Energy-Based Models, Autonomous Systems

## What Are World Models?

World models are AI systems that learn internal representations of how the world works, enabling prediction, planning, and decision-making. They're crucial for:

- **Autonomous agents** (robotics, self-driving)
- **Video prediction** and understanding
- **Model-based reinforcement learning**
- **Efficient learning** from limited data

Key approaches include Joint-Embedding Predictive Architecture (JEPA) and Energy-Based Models (EBMs), which learn representations through self-supervised predictive learning rather than explicit labels.

## How This Notebook Works

This is an **AI-driven research notebook**. The workflow is simple:

1. **You provide URLs** to papers, projects, blog posts, or ask AI to search for content
2. **AI extracts** information and fills markdown templates
3. **AI updates** the appropriate research documents automatically
4. **Documents grow** organically over time through AI-assisted curation

No external tools required (no Zotero, Obsidian, RSS readers). Just markdown files and AI assistance.

## Research Documents

### Core Concepts

📖 **[concepts.md](research/concepts.md)** - Deep dives into fundamental concepts

- What is JEPA? How does it work?
- What are Energy-Based Models?
- What is Dragon Hatchling (BDH)?
- What defines a world model?
- How do these concepts relate?

### Papers, Talks, & Blogs

📄 **[publications.md](research/publications.md)** - Papers, talks, blog posts, and videos organized by topic

- Foundational papers
- Recent developments (last 3-6 months)
- Talks and presentations
- Technical blog posts
- Organized by topic: JEPA, EBMs, World Models, Applications

### Key Players

👥 **[players.md](research/players.md)** - Seminal contributors and thought leaders

- Researchers who originated or significantly advanced key concepts
- Research institutions leading the field
- Companies with major world models initiatives
- Only includes recognized thought leaders, not all paper co-authors

### Open Source and Open Data

💻 **[projects.md](research/projects.md)** - GitHub repos, frameworks, tools, datasets

- JEPA implementations
- EBM libraries and frameworks
- World model frameworks (DreamerV3, etc.)
- Datasets and benchmarks
- Status: Active | Maintained | Archived

### Use Cases

🎯 **[use-cases.md](research/use-cases.md)** - Applications by industry

- Robotics (manipulation, navigation)
- Autonomous vehicles
- Gaming and simulation
- Other applications
- Technical requirements and current solutions

## Deliverables

📊 **[deliverables/](deliverables/)** - Synthesized outputs

Planned deliverables:

- **One-pager**: "What are world models and why should you care?" (1-2 pages for executives/investors)
- **Investment brief**: Market analysis, technical assessment, opportunities (10-15 pages)
- **PoC plan**: Blueprint for proof-of-concept implementation (8-12 pages)

## Project Documentation

📋 **[CLAUDE.md](CLAUDE.md)** - AI assistant guidelines

- How AI should help maintain this notebook
- Workflow for adding papers, players, projects, use cases
- Style guide (sober, factual, concise, pattern-oriented)
- Content organization standards
- Quality standards

📅 **[PLAN.md](PLAN.md)** - Research roadmap

- Research questions each document answers
- Deliverable specifications
- Content collection strategy
- Timeline and milestones
- Success metrics

## Getting Started

### Slash Commands

The easiest way to interact with this notebook:

**`/add <url>`** - Add a paper, project, video, or other content
```
/add https://arxiv.org/abs/2602.03604
/add https://github.com/facebookresearch/jepa
/add https://www.youtube.com/watch?v=...
/add https://ai.meta.com/blog/yann-lecun-ai-model-i-jepa/
```

**`/search <topic>`** - Search for papers and projects
```
/search JEPA
/search energy based models robotics
/search recent self-supervised learning papers
```

**`/sources`** - Check preferred sources for new content
```
/sources
```
Monitors arXiv, GitHub, company blogs, and researcher pages for new content (last 30 days).

**`/synthesize`** - Synthesize insights from recent additions
```
/synthesize
```
Reviews recent papers, identifies patterns/themes, updates concepts.md, and organizes entries into topic sections.

### Natural Language

You can also use natural language:

```
"Add this paper: https://arxiv.org/abs/2602.03604"
"Find recent papers on JEPA"
"What are the key themes in EBM research?"
```

AI will fetch content, extract information, fill templates, and update documents.

### Search Queries to Try

- "JEPA" or "joint embedding predictive architecture"
- "energy based models" + "world models"
- "self-supervised learning" + "representation"
- "model based reinforcement learning"
- Researcher names: "Yann LeCun", "Danijar Hafner"

### Templates

All entries follow consistent templates in **[research/_templates/](research/_templates/)**:

- `publication-entry.md` - For papers, talks, videos, blog posts
- `player-entry.md` - For researchers, institutions, companies
- `project-entry.md` - For GitHub repos and projects
- `use-case-entry.md` - For applications and use cases

**Video Guidelines**: Only include videos from well-known researchers, institutions, or reputable channels (conference talks, interviews, tutorials).

## Current Status

**Phase**: Foundation Building (Month 1)

**Next Steps**:

- [ ] Add 10-15 foundational papers
- [ ] Populate concepts.md with JEPA, EBM, World Models
- [ ] Identify top 10 researchers
- [ ] Catalog 5-10 open-source projects
- [ ] Document 3-5 use cases

## Style Guide Summary

All content follows these principles:

- **Sober and Factual**: State facts, avoid hype
- **Concise**: Dense information, respect reader's time
- **Pattern-Oriented**: Highlight connections and relationships
- **Assume Experience**: Write for experienced engineer/researcher new to AI
- **Technical Precision**: Use precise terms, cite specific architectures
- **Actionable**: Include enough detail to dive deeper or implement

See [CLAUDE.md](CLAUDE.md) for full style guide and examples.

## Maintenance

- **Continuous**: Add content as discovered
- **Weekly**: Review recent additions, ensure quality
- **Monthly**: Synthesize insights into concepts.md
- **As needed**: Create/update deliverables

## License

Research notes and summaries for personal/educational use. Papers and external content retain original authors' rights.
