# Changelog

All notable changes to this project are documented in this file.

## [0.1.0] - 2026-04-09

### Added

- Initial public release of `proxmox-cicd-deploy-skill`.
- Core skill instructions in `SKILL.md` for Proxmox CI/CD deploy troubleshooting and hardening.
- UI metadata in `agents/openai.yaml`.
- Reusable troubleshooting reference in `references/proxmox-cicd-playbook.md`.
- Project docs: `README.md`, `LICENSE` (MIT), and `CONTRIBUTING.md`.
- Example workflow `examples/github-actions-proxmox-deploy.yml`.

### Changed

- Sanitized sensitive/hardcoded operational values in examples using placeholders (`CT_ID`, `APP_DIR`, `EXPECTED_NODE`, `SERVICE_NAME`, `HEALTH_URL`).
- Aligned docs and metadata naming to `proxmox-cicd-deploy-skill`.
- Added compatibility matrix and portable validation commands (Bash + PowerShell).