# tauceti-chf-dashboard

**Live dashboard: <https://why-op109.github.io/tauceti-chf-dashboard/>**

A public, read-only status page for an AI-assisted contribution pipeline that works on the
`CombinatorialHeegaardFloer` roadmap of [Tau Ceti](https://github.com/TauCetiProject/TauCeti), the
open library of AI-written, AI-reviewed formal mathematics in Lean 4. The pipeline is operated by
[@WHY-Op109](https://github.com/WHY-Op109).

The status data is generated automatically and nothing can be operated from here: the page has
no operation buttons, no commands and no way to send anything back. All operations happen on the
operator's local machine.

## What the dashboard shows

- **Pipeline:** each roadmap target moving through select, claim, author, verify, gate, submit,
  CI/review and merge, with the pull requests it produced (linked to GitHub).
- **Review state:** CI result and the verdict of each review rubric per PR, review rounds left.
- **Selector:** which roadmap units are ranked next, the queue, and units on cool-down.
- **Automation:** which automatic stages are switched on, the caps, and whether the Codex and
  Claude agents currently have quota available.
- **Reviews:** how many review rounds other contributors posted on our PRs, and how many we posted
  on theirs.

Timestamps in the data are UTC. For the full story of any PR, use the PR itself on
[TauCetiProject/TauCeti](https://github.com/TauCetiProject/TauCeti/pulls?q=author%3AWHY-Op109).

## How it works

A local control board publishes a snapshot about every 5 minutes; the page reads it every
minute. The page shows the snapshot's age (amber after 15 minutes, red after 60), which usually
means the operator's machine is offline, not that GitHub is out of date.

| Branch | Content |
|---|---|
| `status` | `status.json`, `manifest.json` and this README, as a single commit that is replaced on every publish (schema `chf-dashboard-snapshot/v3`) |
| `gh-pages` | the static viewer served at the link above |

Raw data: <https://raw.githubusercontent.com/WHY-Op109/tauceti-chf-dashboard/status/status.json>

## What is not published

The snapshot is built from an allowlist of structured fields only (ids, states, timestamps, counts,
short commit hashes, links to Tau Ceti PRs). Logs, agent transcripts, PR titles and bodies, review
texts, file paths, branch names, account identifiers and credentials are never included, and every
snapshot is scanned again before it is published.

## Contribution rules the pipeline follows

Work is limited to roadmap targets and to `TauCeti/`; every PR states its AI authorship and its
roadmap attribution; branch pushes are compare-and-swap only; nothing is merged by an admin
override; the pipeline never opens issues or PRs in `TauCetiRoadmap` by itself, and intention
issues are filed only by the operator.

This repository is generated: manual changes to `status` are overwritten by the next publish and
changes to `gh-pages` by the next viewer deploy.
