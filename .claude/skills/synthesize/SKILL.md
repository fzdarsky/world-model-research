---
name: synthesize
description: Review recent additions, identify patterns, update building-block assessments, organize entries
user-invocable: true
---

# Synthesize Insights

Review recent additions, identify patterns, update building-block assessments, and organize entries.

## Usage

```text
/synthesize
```

## Instructions

When this command is invoked:

1. **Review recent additions**:
   - Read `research/publications.md` "Recent Additions" section
   - Identify papers added in last 30 days (check dates)
   - Scan `research/ecosystem.md` for recently added players/solutions
   - Scan `research/projects.md` for recently added projects

2. **Identify patterns and themes**:
   - Common methods across papers
   - Emerging trends (new architectures, convergent approaches)
   - Technical innovations
   - Connections between concepts
   - Open problems or debates
   - Surprising results or contradictions

3. **Update building-block assessments** (`research/building-blocks.md`):
   - New solutions identified → add to Solution landscape tables
   - Maturity changes → update maturity ratings (e.g., project moved from Early OSS to Production-ready)
   - New ecosystem players → add to Key ecosystem players
   - Use-case demand shifts → update demand ratings if evidence supports
   - Platform fit reassessment → flag if new evidence suggests reclassification

4. **Surface competitive shifts** in ecosystem:
   - New entrants to a building block space
   - Positioning changes (player pivoted, acquired, launched new product)
   - Lock-in vector changes (license change, new hardware requirement)
   - Partnership/acquisition signals

5. **Flag stale assessments**:
   - Openness assessments older than 6 months → flag for `/oss-health` re-evaluation
   - Ecosystem entries with no solution updates in 3+ months → flag for review
   - Building block solution landscapes not updated in 3+ months → flag

6. **Update concepts.md**:
   - Read current state of `research/concepts.md`
   - Add new technical details learned from recent papers
   - Update "Current State" sections with latest developments
   - Add connections in "Related Concepts"
   - Preserve existing content (don't delete, only add/update)

7. **Move entries from "Recent Additions"**:
   - Move entries from "Recent Additions" in publications.md to appropriate topic sections
   - Update "Recent Additions" to note: "Last synthesized: YYYY-MM-DD"

8. **Generate synthesis summary**

## Synthesis Focus Areas

**Technical Patterns**:

- Common architectural components across papers
- Shared training techniques
- Convergent vs. divergent approaches

**Platform Intelligence**:

- Which building blocks have increasing demand
- Where OSS alternatives are gaining on proprietary solutions
- New Build/Partner/Integrate opportunities
- Vendor lock-in changes

**Ecosystem Dynamics**:

- Startup funding and growth signals
- Big Tech strategic moves (acquisitions, open-sourcing, product launches)
- OSS community health trends
- Partnership announcements

**Open Questions**:

- Explicitly stated limitations in papers
- Gaps between research and production deployment
- Unmet building-block needs

## Output Format

```text
Synthesis Complete (YYYY-MM-DD)

Papers Reviewed: 12 recent additions

Key Themes Identified:
1. Robot foundation models converging on VLA architecture
2. Sim-to-real transfer improving via video generation (Cosmos-Transfer)
3. ROS2 ecosystem maturing — OSRA governance strengthening

Building Block Updates:
- Robot Foundation Models: Added OpenPI 0.7 to solution landscape, maturity → Early OSS
- Simulation Engines: Genesis World now Production-ready (v0.8 release)
- Model Serving: vLLM-Omni added DiT serving support

Competitive Shifts:
- Physical Intelligence open-sourced pi0.7 — challenges NVIDIA GR00T on openness
- Foxglove acquired by [company] — fleet management consolidating

Stale Assessments Flagged:
- 3 projects need /oss-health re-evaluation (last assessed >6 months ago)
- Sensor Data Ingestion block still unpopulated — needs research

Updated concepts.md:
- Added VLA vs. WAM comparison
- Updated JEPA section with V-JEPA 2.1 temporal coherence improvements

Organized publications.md:
- Moved 12 entries from "Recent Additions" to topic sections
```

## Style Guide Compliance

All synthesis must follow style guide:

- Sober, factual language (cite specific papers)
- Concise summaries
- Pattern-oriented (highlight connections)
- Technical precision
- Use controlled vocabulary for any updated structured fields

## When to Synthesize

Recommend running `/synthesize`:

- After adding 10+ new items across any document
- Bi-weekly (per maintenance schedule in PLAN.md)
- Before creating a deliverable (to ensure all files are current)
- When competitive landscape shifts are suspected

## Error Handling

- If no recent additions found: "No new content to synthesize"
- If concepts.md is empty: Create initial structure with placeholders
- If patterns unclear: Note in summary: "Limited patterns (only N items reviewed)"
