---
name: add
description: Add a paper, project, ecosystem entry, or other content to the notebook from a URL
user-invocable: true
argument-hint: "<url>"
---

# Add Content

Add a paper, project, ecosystem entry, or other content to the notebook.

## Usage

```text
/add <url>
```

## Examples

```text
/add https://arxiv.org/abs/2602.03604
/add https://github.com/facebookresearch/jepa
/add https://developer.nvidia.com/isaac-ros
/add https://www.physicalintelligence.company/blog/pi0
```

## Instructions

When this command is invoked:

1. **Fetch the URL content** using WebFetch tool
2. **Determine content type and target**:
   - arXiv/paper/video URL → publication-entry template → `research/publications.md`
   - GitHub URL → project-entry template → `research/projects.md` (invoke `oss-health` specialist)
   - Company/product page → ecosystem-entry + solution-entry templates → `research/ecosystem.md` (invoke `solution-analyzer` specialist)
   - Researcher/institution page → ecosystem-entry template → `research/ecosystem.md`
   - Blog post about use case → use-case-entry template → `research/use-cases.md`
3. **Extract information** according to the template:
   - For publications: title, authors, date, summary, key points, relevance
   - For projects: name, description, tech stack, features, status, stats, building block(s), maturity, openness assessment
   - For ecosystem entries: name, type, about, solutions (with competitive analysis), reference architecture, platform relevance
   - For use cases: technical use case, verticals, building blocks, requirements, gaps
4. **Fill the appropriate template** from `research/templates/`
5. **Add to the correct document** under appropriate section
6. **Archive source material**:
   - For arXiv papers: download PDF to `research/library/papers/` using naming convention `{arxiv-id}-{slugified-short-title}.pdf`
   - For vendor/product pages: capture screenshot to `research/library/screenshots/` if feasible
   - For non-arXiv papers with direct PDF link: download to `research/library/papers/`
   - Verify downloads are valid (file size > 10KB)
7. **Cross-link**:
   - New ecosystem players → add to `research/ecosystem.md` (only seminal contributors / thought leaders)
   - New use cases identified → add to `research/use-cases.md`
   - Related concepts → note in `research/concepts.md`
   - If authors/presenters already exist in ecosystem.md, link their names: `[Name](ecosystem.md#anchor)`
   - Invoke `block-mapper` to update `research/building-blocks.md` cross-references
8. **Confirm** with user what was added and where

## Specialist Skill Dispatch

- **GitHub projects**: After adding, invoke `/oss-health <github-url>` to generate the openness assessment table
- **Company/product pages**: Invoke `/solution-analyzer <url>` to extract competitive intelligence for solution entries
- **Any addition**: Invoke `block-mapper` (internal) to update building-blocks.md with new solutions, players, or demand evidence

## Style Guide Compliance

All extracted content must follow the style guide in CLAUDE.md:

- Sober and factual
- Concise (2-3 sentences for summaries)
- Pattern-oriented (highlight connections)
- Assume experienced audience
- Technical precision
- Actionable detail
- Use controlled vocabulary for structured fields (Demand, Maturity, Platform fit, Openness)

## Error Handling

- If URL cannot be fetched, inform user and suggest alternatives
- If content type is ambiguous, ask user which template to use
- If entry already exists, ask whether to update or skip
