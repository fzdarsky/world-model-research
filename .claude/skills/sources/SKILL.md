---
name: sources
description: Check preferred sources for new content in last 30 days
user-invocable: true
---

# Check Preferred Sources

Monitor preferred sources for new research content.

## Usage

```text
/sources
```

## Examples

```text
/sources
```

## Instructions

When this command is invoked:

1. **Read preferred sources** from `research/tools/preferred-sources.md`
2. **Check each source category**:

   **Preprint Searches — Architectures & Methods** (Priority 1):
   - Search arXiv and TechRxiv for architecture/method queries (JEPA, EBM, world models, BDH)
   - Filter to last 30 days only
   - Identify papers not yet in publications.md

   **Preprint Searches — Applications & Use Cases** (Priority 2):
   - Search arXiv, TechRxiv, and Google Scholar for application queries (robotics, AV, healthcare, industrial, telecom, scientific discovery)
   - Filter to last 30 days
   - Identify applied papers not yet in publications.md

   **GitHub Organizations** (Priority 3):
   - Check listed GitHub orgs for new repos
   - Check for new releases on watched repos
   - Filter to last 30 days

   **Company Blogs — Research Labs & Industry** (Priority 4):
   - Scan recent posts (last 30 days) from both research lab and applied/industry blogs
   - Look for mentions of JEPA, EBM, world models, digital twins, Physical AI

   **Researcher Pages** (Priority 5):
   - Check Google Scholar pages for new publications
   - Check personal websites/blogs for new content

3. **Rank findings**:
   - Relevance to world models/JEPA/EBM
   - Recency
   - Source credibility (known researchers, top institutions)
   - Potential impact (citations, engagement)

4. **Present top findings**:
   - Group by category (Papers, Projects, Blog Posts)
   - Show top 3-5 from each category
   - Include: title, source, date, 1-sentence description

5. **Ask which to add**: "Which would you like me to add? (e.g., 'P1, P3, B1' for Papers 1,3 and Blog 1)"

6. **Add selected items** using `/add` workflow

## Output Format

```text
Checked preferred sources (last 30 days):

📄 PAPERS (arXiv)
P1. [2024-02-20] "Energy-Based JEPA for Robust Representation Learning"
    Authors: Smith et al. (Stanford)
    Uses energy-based formulation for JEPA, achieves 15% improvement on robustness benchmarks

P2. [2024-02-15] "World Models for Autonomous Navigation"
    Authors: Johnson et al. (Meta AI)
    Applies world models to real-robot navigation, reduces sample complexity by 10x

💻 PROJECTS (GitHub)
G1. [2024-02-18] awesome-world-models/awesome-world-models
    New curated list of world model resources (230 stars in 2 weeks)

G2. [2024-02-10] facebookresearch/eb-jepa v1.0 release
    Official energy-based JEPA implementation, includes pretrained models

📝 BLOG POSTS
B1. [2024-02-22] "JEPA: The Next Step in Self-Supervised Learning" - Meta AI Blog
    Explains JEPA architecture and recent advances, includes demo

🔬 RESEARCHERS
R1. Yann LeCun - New preprint on generalized JEPA framework
    Extends JEPA to multimodal settings

Which would you like me to add? (e.g., 'P1, G1, B1')
```

## Time Range

- Default: Last 30 days
- User can specify different range if desired

## Avoiding Duplicates

Before presenting results:
- Check if paper title/URL already exists in publications.md
- Check if project already exists in projects.md
- Check if player already exists in players.md
- Only show genuinely new content

## Error Handling

- If a source is unavailable, skip and note it
- If no new content found, inform user: "No new content in preferred sources (last 30 days)"
- If many results (>15), present top-ranked only
