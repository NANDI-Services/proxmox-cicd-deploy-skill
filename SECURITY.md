# Security Policy

This repository publishes the `proxmox-cicd-deploy-skill` guidance package.
It does not host runtime production services, but it can influence deployment workflows and infrastructure operations.

## Supported Versions

Security fixes are applied to:

| Version | Supported |
| --- | --- |
| Latest `main` | Yes |
| Older tags/releases | No |

## Reporting a Vulnerability

If you discover a vulnerability, please do not open a public issue with exploit details.

Use one of the following channels:

- GitHub Security Advisory (preferred): `Security` tab in this repository
- Private email: `security@nandi-services.com`

Please include:

- A clear description of the issue
- Steps to reproduce
- Impact assessment (what can be affected)
- Suggested mitigation (if available)

## Response Targets

- Initial acknowledgement: within 72 hours
- Triage and severity assessment: within 7 days
- Fix or mitigation plan: as soon as validated, depending on severity

## Scope Notes

The following are in scope for responsible disclosure:

- Insecure instructions that could lead to command injection, secret exposure, or destructive operations
- Unsafe workflow examples that can cause unintended production impact
- Dependency or template risks included directly in this repository

The following are out of scope:

- Vulnerabilities in third-party platforms (GitHub, Proxmox, runner images, etc.) unless caused by this repository's guidance
- Hypothetical issues without a reproducible path

## Coordinated Disclosure

Please allow reasonable time for validation and remediation before public disclosure.
We will credit reporters who want attribution once a fix is published.
