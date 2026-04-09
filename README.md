# proxmox-cicd-deploy-skill

Public Codex skill for designing, debugging, and hardening CI/CD deploy pipelines to Proxmox hosts and LXC containers.

## What this skill does

`proxmox-cicd-deploy-guardian` helps you:
- enforce a reliable deploy topology from GitHub Actions runners to Proxmox/LXC
- classify failures by layer (runner/SSH, cluster node, shell-wrapper, in-container runtime)
- use deterministic deploy stages (`SYNC`, `INSTALL`, `RESTART`, `HEALTH`)
- safely execute `pct exec` in single-node and cluster scenarios
- apply hardened health-check and retry patterns

## When to use (triggers)

Use this skill when:
- a workflow deploys through SSH to Proxmox
- deploy steps run `pct exec` inside LXC containers
- GitHub Actions deploys fail with connectivity/auth/node-resolution errors
- `appleboy/ssh-action` (`drone-ssh`) shell behavior causes flaky runs

## Installation

Clone or copy this folder into your Codex skills path.

### Option A: `~/.codex/skills`

```bash
mkdir -p ~/.codex/skills
cp -R proxmox-cicd-deploy-skill ~/.codex/skills/proxmox-cicd-deploy-guardian
```

### Option B: `$CODEX_HOME/skills`

```bash
mkdir -p "$CODEX_HOME/skills"
cp -R proxmox-cicd-deploy-skill "$CODEX_HOME/skills/proxmox-cicd-deploy-guardian"
```

## Example usage

Prompt Codex with:

```text
Use $proxmox-cicd-deploy-guardian to debug this failing GitHub Actions deploy to Proxmox.
```

or:

```text
Use $proxmox-cicd-deploy-guardian to generate a hardened cluster-safe deploy workflow using CT_ID, APP_DIR, EXPECTED_NODE, SERVICE_NAME, and HEALTH_URL.
```

## Included files

- `SKILL.md`
- `agents/openai.yaml`
- `references/proxmox-cicd-playbook.md`

## Validate locally

```bash
python C:/Users/ezesc/.codex/skills/.system/skill-creator/scripts/quick_validate.py .
```