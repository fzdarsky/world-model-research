---
name: synthesize
description: Review recent additions, identify patterns, organize entries
user-invokable: true
---

# Synthesize Research Insights

Review recent additions and synthesize insights into key concepts.

## Usage

```
/synthesize
```

## Examples

```
/synthesize
```

## Instructions

When this command is invoked:

1. **Review recent additions**:
   - Read `research/publications.md` "Recent Additions" section
   - Identify papers added in last 30 days (check dates)
   - Also scan topic sections for recent entries (look for recent dates)

2. **Identify patterns and themes**:
   - Common methods across papers
   - Emerging trends (e.g., "shift toward predictive vs. contrastive")
   - Technical innovations (new architectures, regularization techniques)
   - Connections between concepts (how JEPA relates to EBM, etc.)
   - Open problems or debates in the literature
   - Surprising results or contradictions

3. **Update concepts.md**:
   - Read current state of `research/concepts.md`
   - For each major concept (JEPA, EBM, World Models):
     - Add new technical details learned from recent papers
     - Update "Current State" sections with latest developments
     - Add equations/architectures if referenced in papers
     - Update "How It Differs" with new comparisons
     - Note open questions discovered
   - Add connections in "Related Concepts" section
   - Preserve existing content (don't delete, only add/update)

4. **Move entries from "Recent Additions"**:
   - After synthesizing, move entries from "Recent Additions" in publications.md
   - Place each entry under appropriate topic section
   - Preserve all entry content
   - Update "Recent Additions" to note: "Last synthesized: YYYY-MM-DD"

5. **Generate synthesis summary**:
   - Provide user with summary of what was synthesized:
     - Number of papers reviewed
     - Key themes identified
     - What was added to concepts.md
     - Entries moved to topic sections

## Synthesis Focus Areas

Look for:

**Technical Patterns**:
- Common architectural components across papers
- Shared regularization or training techniques
- Convergent vs. divergent approaches

**Trends**:
- What's gaining momentum (more recent papers)
- What's being abandoned or superseded
- New application areas emerging

**Relationships**:
- How JEPA papers build on each other
- Connections between JEPA and EBM approaches
- Links to broader world models literature

**Open Questions**:
- Explicitly stated limitations in papers
- Inconsistent results across studies
- Gaps identified by researchers

## Output Format

```
Synthesis Complete (YYYY-MM-DD)

📊 Papers Reviewed: 12 recent additions

🔍 Key Themes Identified:
1. Variance regularization: All recent JEPA papers use VICReg-style losses to prevent collapse
2. Shift to latent prediction: Moving from pixel-space to abstract representation prediction
3. Scaling laws: Larger encoders (ViT-H) show better downstream performance
4. Multimodal extension: JEPA being applied to text-image, video-audio pairs

📝 Updated concepts.md:
- JEPA section: Added technical details on VICReg regularization, masking strategies
- EBM section: Added connection to JEPA (both avoid contrastive negatives)
- World Models section: Updated with recent robotics applications

📁 Organized publications.md:
- Moved 12 entries from "Recent Additions" to topic sections
- JEPA: 5 papers
- EBM: 3 papers
- Applications: 4 papers

💡 Insights:
- JEPA and EBM are converging: both use energy-based formulations for stability
- Robotics applications showing 10x sample efficiency improvements
- Open question: Optimal latent dimensionality still unclear across papers
```

## Style Guide Compliance

All synthesis must follow style guide:
- Sober, factual language (cite specific papers)
- Concise summaries
- Pattern-oriented (highlight connections)
- Technical precision (specific methods, not vague descriptions)
- Actionable insights

## When to Synthesize

Recommend running `/synthesize`:
- After adding 10+ papers to "Recent Additions"
- Monthly (per maintenance schedule in PLAN.md)
- Before creating a deliverable (to ensure concepts.md is current)
- When user notices patterns and wants them captured

## Error Handling

- If no recent additions found: "No new content in 'Recent Additions' to synthesize"
- If concepts.md is empty: Create initial structure with placeholders
- If patterns unclear: Note in synthesis summary: "Limited patterns (only N papers)"
