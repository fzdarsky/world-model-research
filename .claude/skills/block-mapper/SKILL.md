---
name: block-mapper
description: Map content to building blocks and update cross-references
user-invocable: false
---

# Building Block Mapper

Given a new solution, project, or use case, identify which building blocks it involves and update cross-references in building-blocks.md.

## Instructions

When invoked (by `/add` or `/synthesize`):

1. **Read current taxonomy**: Read `research/building-blocks.md` to understand the current block definitions

2. **Map content to blocks**: Identify which building block(s) the new content relates to

   - A solution may cover multiple blocks (e.g., NVIDIA Isaac Sim covers Simulation Engines + Sim-to-Real)
   - A project implements one or more blocks
   - A use case requires multiple blocks

3. **Check for new blocks**: If the content suggests a capability not covered by existing blocks, flag it:

   - Output: "Potential new building block identified: [name] — [rationale]"
   - Do NOT auto-create new blocks; flag for user review

4. **Update cross-references**: In `building-blocks.md`, update the relevant block entries:

   - Add new solutions to the Solution landscape table
   - Add new ecosystem players to the Key ecosystem players list
   - Update use-case demand ratings if new evidence suggests a change
   - Add links to new publications or concepts

5. **Return mapping**: Report which blocks were matched and what was updated
