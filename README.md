# 📘 Org-Level Renovate Configuration

This repository contains the shared Renovate configuration for all repositories in the organisation. It is designed to:

- Safely manage dependencies for all repos.
- Group minor/major updates and Docker/GitHub Actions updates.  
- Auto-label security and major updates.  
- Support a **Sandbox PR workflow** that spins up Renovate in a dry-run mode to simulate PRs and dependency updates without actually making changes. That gives you a more realistic test of the configuration.
[![Sandbox Renovate PR Validation](https://github.com/mashakir/renovate-config/actions/workflows/sandbox-renovate-validation-.yml/badge.svg)](https://github.com/mashakir/renovate-config/actions/workflows/sandbox-renovate-validation-.yml)

> The badge shows the latest status of the Renovate sandbox workflow on the `main` branch. Green indicates the last validation passed, red indicates failure.

---

## ⚙️ Features

1. **Safe Automerge**  
   - Patch a linter updates are auto-merged according to CI checks.  
   - Minor updates are grouped into a single PR for review.  
   - Major updates are separated and require manual review.  

2. **Grouped Updates**  
   - **GitHub Actions** → grouped PRs  
   - **Docker base images** → grouped PRs  
   - **Minor dependencies** → grouped PRs  
   - **Major upgrades** → separate PRs  

3. **Private NuGet Support**  
   - Uses the `NUGET_FEED_TOKEN` secret to access private GitHub Packages feeds.  

4. **Scheduling & Limits**  
   - Weekly update schedule.  
   - PR concurrency limits (`prConcurrentLimit`) to avoid CI flooding.  
   - Automerge restricted to work hours: 10am–4pm London time.  

5. **Security & Labels**  
   - Security patches auto-labeled `security`.  
   - Major updates labeled `major`.  
   - All Renovate PRs labeled `renovate` and `dependencies`.  

---

## 🚀 Usage

### 1. Include Org Config in Your Repo

Add a `renovate.json` file in your repository:

```json
{
  "extends": ["github>mashakir/renovate-config"]
}
