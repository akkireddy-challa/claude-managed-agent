# 🤖 Claude Managed Agent: PR Digest & Engineering Intelligence

Built during the **Claude Founder House Stockholm · Managed Agents Workshop** (October 2026).

This repository hosts the live architecture schematic and the generated output from a production **Claude Managed Agent (CMA)** running on Anthropic's platform.

---

## 🌐 Live Web Demos
- **[Live Agent Architecture Dashboard](https://akkireddy-challa.github.io/claude-managed-agent/)**: Interactive CMA schema showing environment, vault, outcome grading, and session run status.
- **[Generated PR Digest Output](https://akkireddy-challa.github.io/claude-managed-agent/digest.html)**: The deliverable produced autonomously by the Opus 5.5 agent.

---

## 🏗️ Architecture & CMA Primitives
- **Model**: `claude-opus-5-5`
- **Agent ID**: `agent_01K1DDc9H3gcMQaB85GzNWot` (Version 1)
- **Environment**: Anthropic Cloud Sandbox (`env_01RYs36XAgXUtX7mUCoD8p75`)
- **Credential Security**: Fine-grained GitHub read token stored in Anthropic Managed Vault (`vlt_011Cg2AYNaJCc5aZu58f6eaN`)
- **Outcome Grader**: 6-point strict rubric evaluated on every run (`user.define_outcome`)
- **First Run**: `sesn_01MToGXHiKi5MTpMgQDsAg8a` (Status: `satisfied` on 1st attempt)
- **Scheduled Deployment**: Weekly cron on Friday at 5 PM (`0 17 * * 5 Europe/London`)

---

## 📊 What the Agent Does
1. **Scans active repositories** across `@akkireddy-challa` via GitHub API.
2. **Detects blockers**: Identifies open PRs waiting >48h or with change requests.
3. **Synthesizes updates**: Categorizes Merged & Shipped, High-Impact Architectural changes, and Team Velocity.
4. **Self-grades against rubric**: Confirms no hallucinated links or estimated numbers.
5. **Generates standalone visual deliverable**: Writes a self-contained executive HTML report.
