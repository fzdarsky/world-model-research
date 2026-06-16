---
name: search
description: Search for papers, projects, ecosystem players, or solutions on a topic
user-invocable: true
argument-hint: "<topic>"
---

# Search for Content

Search for papers, projects, ecosystem players, or solutions on a specific topic.

## Usage

```text
/search <topic>
```

## Examples

```text
/search JEPA
/search robot foundation models
/search digital twin open source
/search Isaac ROS competitors
/search Physical AI startups funding 2026
```

## Instructions

When this command is invoked:

1. **Parse the topic** to understand what to search for
2. **Determine search strategy**:
   - For papers: Use WebSearch with arXiv and Google Scholar
   - For projects: Search GitHub via WebSearch
   - For ecosystem players/solutions: Search vendor blogs, TechCrunch, The Robot Report, Crunchbase
   - For general content: Multi-source search
3. **Execute searches**:
   - **arXiv + TechRxiv**: Search with topic keywords + filter last 3-6 months
   - **Google Scholar**: For applied/engineering papers
   - **GitHub**: Search repos matching topic with stars>10
   - **Research blogs**: Research lab blogs (Meta AI, Google DeepMind, etc.)
   - **Industry sources**: TechCrunch, The Robot Report, IEEE Spectrum for startups and industry news
   - **Vendor pages**: Product documentation and developer portals
   - Use search queries from `research/tools/preferred-sources.md`
4. **Rank and filter results**:
   - Relevance to Physical AI platform intelligence
   - Recency (prefer last 6 months for papers)
   - Quality indicators (citations, stars, author reputation, deployment evidence)
   - Avoid duplicates already in research documents
5. **Present findings** to user:
   - Show top 5-10 results
   - Include: title, source, date, 1-sentence description
   - Format as numbered list for easy selection
   - Group by category: Papers, Projects, Ecosystem Players, Solutions
6. **Ask which to add**: "Which of these would you like me to add? (e.g., '1, 3, 5')"
7. **Add selected items** using the `/add` workflow for each

## Search Sources Priority

1. **arXiv + TechRxiv** - Research papers (foundational and applied)
2. **Google Scholar** - Applied/engineering papers, conference proceedings
3. **GitHub** - Open-source projects and implementations
4. **Industry news** - The Robot Report, TechCrunch, IEEE Spectrum for startups and product launches
5. **Company blogs** - Research labs and vendor product announcements
6. **Crunchbase** (via WebSearch) - Startup funding and company profiles
7. **Researcher pages** - Latest work from key people

Refer to `research/tools/preferred-sources.md` for specific search queries and sources.

## Output Format

```text
Found 10 results for "robot foundation models":

Papers:
1. [2026-05] "OpenPI: Open-Source Policy for Robot Manipulation" - Physical Intelligence
   arXiv:2605.xxxxx - Open VLA model achieving 85% success on 24 tasks

2. [2026-04] "GR00T N1.7: Generalist Robot Policy" - NVIDIA
   arXiv:2604.xxxxx - Multi-embodiment foundation model

Projects:
3. [Active] Physical-Intelligence/openpi - Official OpenPI implementation (2.1k stars)
   Python/JAX - Open-source VLA with gRPC serving

Ecosystem:
4. [Startup] Skild AI - $300M Series A, building general-purpose robot FM
   Founded 2023, CMU spinout, claims 4x data efficiency

Solutions:
5. [Product] NVIDIA Isaac Manipulator - Manipulation pipeline on Isaac ROS
   GPU-accelerated grasping, integrates with Omniverse

Which would you like me to add? (e.g., '1, 3, 5')
```

## Error Handling

- If no results found, suggest related search terms
- If too many results (>20), ask user to narrow the search
- If search fails, try alternative search methods
