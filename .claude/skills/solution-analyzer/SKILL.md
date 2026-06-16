---
name: solution-analyzer
description: Extract solution details from vendor pages for ecosystem entries
user-invocable: true
argument-hint: "<url>"
---

# Vendor Solution Analyzer

Extract solution details from a vendor page, product doc, or announcement — features, architecture, competitive positioning, and battle card claims.

## Usage

```text
/solution-analyzer <url>
```

## Examples

```text
/solution-analyzer https://developer.nvidia.com/isaac-ros
/solution-analyzer https://www.physicalintelligence.company/blog/pi0
```

## Instructions

When this command is invoked:

1. **Fetch the page** using WebFetch

2. **Extract solution details**:

   - **Functional features**: What it does — capabilities, supported tasks, modalities
   - **Non-functional claims**: Performance metrics, latency targets, throughput, hardware support, supported platforms, scale targets, certifications — what they highlight in comparisons
   - **Competitive positioning**: Who they compare against (explicitly or implicitly), on which dimensions, what they claim to be better at
   - **Architecture / integration points**: APIs, data formats, protocols, dependencies, deployment model
   - **Openness and lock-in signals**: License, hardware requirements (CUDA-only?), proprietary APIs, data format lock-in
   - **Pricing model signals**: Free/paid/enterprise tiers, compute requirements

3. **Identify building blocks**: Which building blocks from `building-blocks.md` does this solution cover?

4. **Identify competitive relationships**:

   - **Competes with**: Other solutions in same building block(s) — on which dimensions
   - **Complements**: Solutions it integrates with or depends on

5. **Produce output** using the `solution-entry.md` template, ready for inclusion in `ecosystem.md`

6. **Archive source**: Download a screenshot or PDF of the source page to `research/library/screenshots/` if feasible

## Style Guide

- Use factual feature comparisons, not marketing language
- Quote specific metrics when vendors provide them
- Note claims that seem inflated or unverified
- Distinguish between announced and shipping features
