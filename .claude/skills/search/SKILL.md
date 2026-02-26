---
name: search
description: Search for papers/projects on a topic and add them
user-invokable: true
---

# Search for Research Content

Search for papers, projects, or other content on a specific topic.

## Usage

```
/search <topic>
```

## Examples

```
/search JEPA
/search energy based models
/search world models robotics
/search recent papers on self-supervised learning
```

## Instructions

When this command is invoked:

1. **Parse the topic** to understand what to search for
2. **Determine search strategy**:
   - For papers: Use WebSearch with arXiv and Google Scholar
   - For projects: Search GitHub via WebSearch
   - For general content: Multi-source search
3. **Execute searches**:
   - **arXiv**: Search with topic keywords + filter last 3-6 months
   - **GitHub**: Search repos matching topic with stars>10
   - **Blogs**: Search company blogs and researcher pages
   - Use search queries from `research/_tools/preferred-sources.md`
4. **Rank and filter results**:
   - Relevance to world models research
   - Recency (prefer last 6 months for papers)
   - Quality indicators (citations, stars, author reputation)
   - Avoid duplicates already in research documents
5. **Present findings** to user:
   - Show top 5-10 results
   - Include: title, source, date, 1-sentence description
   - Format as numbered list for easy selection
6. **Ask which to add**: "Which of these would you like me to add? (e.g., '1, 3, 5')"
7. **Add selected items** using the `/add` workflow for each

## Search Sources Priority

1. **arXiv** - For academic papers
2. **GitHub** - For open-source projects
3. **Google Scholar** - For older foundational papers
4. **Company blogs** - For industry perspectives
5. **Researcher pages** - For latest work from key people

Refer to `research/_tools/preferred-sources.md` for specific search queries and sources.

## Output Format

```
Found 8 results for "JEPA":

Papers:
1. [2024-02] "V-JEPA: Latent Video Prediction for Visual Representation Learning" - Meta AI
   arXiv:2402.08563 - Joint-embedding architecture for video prediction

2. [2024-11] "I-JEPA: Self-Supervised Learning from Images with a Joint-Embedding Predictive Architecture" - Meta AI
   arXiv:2411.xxxxx - Image-based JEPA with masking strategy

Projects:
3. [Active] facebookresearch/jepa - Official JEPA implementation (1.2k stars)
   Python/PyTorch - Reference implementation of I-JEPA

Which would you like me to add? (e.g., '1, 3')
```

## Error Handling

- If no results found, suggest related search terms
- If too many results (>20), ask user to narrow the search
- If search fails, try alternative search methods
