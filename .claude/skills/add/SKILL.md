---
name: add
description: Add a paper, project, or other research content to the notebook from a URL
user-invocable: true
argument-hint: "<url>"
---

# Add Research Content

Add a paper, project, or other research content to the notebook.

## Usage

```text
/add <url>
```

## Examples

```text
/add https://arxiv.org/abs/2602.03604
/add https://github.com/facebookresearch/jepa
/add https://ai.meta.com/blog/yann-lecun-ai-model-i-jepa/
```

## Instructions

When this command is invoked:

1. **Fetch the URL content** using WebFetch tool
2. **Determine content type**:
   - arXiv/paper/video URL → Use publication-entry template
   - GitHub URL → Use project-entry template
   - Researcher/institution page → Use player-entry template
   - Blog post about use case → Use use-case-entry template
3. **Extract information** according to the template:
   - For publications: title, authors, date, summary, key points, relevance
   - For projects: name, description, teck stack, features, status, stats, last update
   - For players: name, type, focus areas, key work, key collaborators, links
   - For use cases: industry, description, technical requirements, solutions, gaps
4. **Fill the appropriate template** from `research/templates/`
5. **Add to the correct document**:
   - Publications → `research/publications.md` under appropriate topic section
   - Projects → `research/projects.md` under appropriate category
   - Players → `research/players.md` under appropriate type
   - Use cases → `research/use-cases.md` under appropriate industry
6. **Download PDF to library** (for arXiv and other paper URLs):
   - Download the PDF to `research/library/` using curl
   - Naming convention: `{arxiv-id}-{slugified-short-title}.pdf` (e.g., `2508.10104-dinov3.pdf`)
   - For arXiv papers, the PDF URL is `https://arxiv.org/pdf/{id}.pdf`
   - For non-arXiv papers with a direct PDF link, download using that link
   - Verify the download is a valid PDF (check file size > 10KB)
   - Skip this step for non-paper content (GitHub projects, player pages, etc.)
7. **Cross-link** if needed:
   - New researchers mentioned → add to players.md (only seminal contributors / thought leaders)
   - New use cases identified → add to use-cases.md
   - Related concepts → note in concepts.md
   - If any authors/presenters already exist in players.md, link their names: `[Name](players.md#anchor)`
8. **Confirm** with user what was added and where

## Style Guide Compliance

All extracted content must follow the style guide in CLAUDE.md:

- Sober and factual
- Concise (2-3 sentences for summaries)
- Pattern-oriented (highlight connections)
- Assume experienced audience
- Technical precision
- Actionable detail

## Error Handling

- If URL cannot be fetched, inform user and suggest alternatives
- If content type is ambiguous, ask user which template to use
- If entry already exists, ask whether to update or skip
