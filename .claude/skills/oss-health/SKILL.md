---
name: oss-health
description: Evaluate community health, openness, and governance of an open-source project
user-invocable: true
argument-hint: "<github-url>"
---

# OSS Health & Openness Evaluator

Evaluate the community health, openness, governance, and lock-in risk of an open-source project.

## Usage

```text
/oss-health <github-url>
```

## Examples

```text
/oss-health https://github.com/ros2/rclcpp
/oss-health https://github.com/nvidia-cosmos/cosmos-predict2.5
```

## Instructions

When this command is invoked:

1. **Fetch project information** using WebFetch on the GitHub URL and GitHub API (via WebSearch for contributor stats, release history)

2. **Evaluate each dimension**:

   **License**:

   - Identify the license (check LICENSE file, SPDX identifier)
   - Rate: `Permissive` (MIT, Apache 2.0, BSD) | `Copyleft` (GPL, LGPL, MPL) | `Source-available` (BSL, SSPL, custom restrictive) | `Proprietary`
   - Note any patent grants or unusual terms

   **Governance**:

   - Check for GOVERNANCE.md, CHARTER, or foundation affiliation
   - Rate: `Foundation` (Linux Foundation, Apache, Eclipse, OSRA) | `Multi-vendor` (multiple companies on steering committee) | `Single-vendor` (one company controls roadmap) | `BDFL` (individual maintainer)
   - Note the governing entity

   **Contributor Diversity**:

   - Check contributor count, top contributor percentage, number of contributing organizations
   - Rate: `High` (5+ orgs, no single org >50% of commits) | `Medium` (2-4 orgs, or one org 50-80%) | `Low` (single org >80%)
   - Note key contributing organizations

   **Community Health**:

   - Check commit cadence (last 3 months), issue response time, PR merge time, release frequency
   - Rate: `Active` (weekly commits, responsive issues) | `Maintained` (monthly commits, issues addressed) | `Declining` (sporadic commits, growing issue backlog) | `Archived` (no recent activity)

   **Corporate Control Risk**:

   - Check for CLA requirements, single-vendor commit dominance, roadmap control
   - Rate: `Low` (no CLA, diverse contributors) | `Medium` (CLA exists but community has voice) | `High` (CLA + single vendor controls >80% + closed roadmap)

   **Ecosystem**:

   - Check downstream dependents, plugins/extensions, integration breadth
   - Note major users and integrators

   **Release Discipline**:

   - Check semver compliance, release cadence, backwards compatibility
   - Note LTS or stability guarantees

3. **Produce output** in two parts:

   - Structured table (using controlled vocabulary ratings) ready for `projects.md` entry
   - 2-3 sentence narrative assessment summarizing the key findings and risks

4. **If invoked by `/add`**: Return the structured table for inclusion in the project entry

## Evaluation Frameworks

When available, cross-reference with:

- **OpenSSF Scorecard** (<https://scorecard.dev/>) — check if a score exists for the repo
- **CHAOSS metrics** (<https://chaoss.community/>) — use as rubric for community health dimensions

## Output Format

```text
Openness assessment for [project-name]:

| Dimension              | Rating        | Detail                                   |
| ---------------------- | ------------- | ---------------------------------------- |
| License                | Permissive    | Apache 2.0                               |
| Governance             | Single-vendor | NVIDIA controls roadmap                  |
| Contributor diversity  | Low           | 95% NVIDIA employees, 14 contributors   |
| Community health       | Active        | Weekly commits, issues addressed         |
| Corporate control risk | High          | CLA required, single-vendor dominant     |

Assessment: [2-3 sentences summarizing key findings: overall openness,
key risks, comparison to alternatives in same building block]
```
