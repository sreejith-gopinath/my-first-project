# Git Workflow & Repository Security Architecture

A reference repository demonstrating production-grade Git branching strategies, automated CLI workflows, cryptographic commit verification, and repository security hardening.

## Key Technical Implementations

* **Multi-Environment Branching Strategy:** Architected a structured promotion pipeline separating local development (`feature/*`), integration (`dev`), quality assurance (`test`), and production (`main`) environments.
* **Branch Protection & Rulesets:** Enforced active GitHub Repository Rulesets across `dev`, `test`, and `main` to block direct force-pushes, prevent accidental branch deletion, and mandate Pull Request reviews prior to promotion.
* **Cryptographic Commit Signing (SSH):** Configured Ed25519 SSH key authentication and automated Git commit signing (`gpg.format=ssh`), ensuring every commit carries a cryptographically verified signature.
* **Automated Security & Supply-Chain Hardening:** Enabled Dependabot vulnerability alerts, automated security updates, and strict `.gitignore` secret hygiene to prevent credential exposure.
* **Zero-ClickOps CLI Automation:** Managed repository provisioning, branch promotion, Pull Request creation, and security audits end-to-end via the GitHub CLI (`gh`) and Git.

## Environment Promotion Workflow

```text
feature/* ──(PR)──▶ dev ──(PR)──▶ test ──(PR)──▶ main (prod)
```

| Branch | Environment | Purpose |
| :--- | :--- | :--- |
| `main` | **Production** | Protected release branch containing verified, production-ready code. |
| `test` | **QA / Staging** | Pre-production integration and validation environment. |
| `dev` | **Development** | Active integration branch for completed feature work. |
| `feature/*` | **Local** | Short-lived branches for isolated feature development and bug fixes. |

## Tech Stack & Tooling

* **Version Control & CLI:** Git (`2.56+`), GitHub CLI (`gh`), Zsh
* **Security:** Ed25519 SSH Keys, GitHub Repository Rulesets, Dependabot
* **Runtime & Editor:** Python 3, Visual Studio Code
