# 🤖 Claude Managed Agent: PR & Commit Digest

Built during the **Claude Founder House Stockholm · Managed Agents Workshop** (October 2026).

A Claude Managed Agent that writes a weekly engineering digest of my GitHub. This repo hosts its architecture page and a sample of what it produces.

---

## 🌐 Live pages
- **[Agent architecture dashboard](https://akkireddy-challa.github.io/claude-managed-agent/)**: the CMA primitives (environment, vault, outcome grading, deployment) and the run log.
- **[Sample digest](https://akkireddy-challa.github.io/claude-managed-agent/digest.html)**: written by agent v2 over a 30-day test window (61 commits across 3 repos), graded `satisfied` on its first attempt.

---

## 🏗️ CMA primitives
| | Primitive | Setting |
|---|---|---|
| 🤖 | Agent | `pr-digest` · `claude-opus-5-5` · version 2 · `agent_01K1DDc9H3gcMQaB85GzNWot` |
| 📦 | Environment | Cloud sandbox · `env_01RYs36XAgXUtX7mUCoD8p75` |
| 🔐 | Vault | Read-only fine-grained GitHub token as an `environment_variable` credential, injected only on requests to `api.github.com`. The agent never sees the value. |
| 🎯 | Outcome | `user.define_outcome`: a 6-point rubric graded on every run · `max_iterations: 3` |
| 🗓️ | Deployment | Every Friday 17:00 Europe/London (`0 17 * * 5`), pinned to agent v2 · `depl_01XR6M18zhZoCR3cR1opf2Pz` |
| 🧪 | Evals | Case 1 = the verified 30-day v2 digest, used as the regression baseline before promoting any new agent version |

## 📊 What the agent does
1. Scans the repos owned by `@akkireddy-challa` through the GitHub API (read-only).
2. **Merged & Shipped**: merged PRs plus direct commits to each default branch, grouped by repo and summarized by theme.
3. **Needs Attention**: open PRs in the window that have waited more than 48h without approval or have changes requested. Older PRs are collapsed into a single "stale" line.
4. **High-Impact**: large diffs (more than 500 lines or 20 files) and breaking changes.
5. **Velocity**: PRs merged and opened, non-bot commits per repo, active contributors. Bot activity is excluded and noted.
6. Writes a self-contained HTML page, graded against the rubric. Every number can be traced to a GitHub API response.

## 🔁 Iteration log
- **v1** was graded `satisfied` but produced an empty digest: no PRs in 30 days, because work here lands as direct commits.
- **v2** added direct commits, collapsed stale PRs and excluded bots. It was graded `satisfied`, and its numbers match an independent hand count (61 commits, 2 contributors).
