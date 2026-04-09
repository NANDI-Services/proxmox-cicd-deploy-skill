# Proxmox CI/CD Playbook

## 1. Preflight checklist

- Confirm workflow uses `appleboy/ssh-action` against public Proxmox host.
- Confirm secrets exist and are mapped:
  - `PROXMOX_HOST`
  - `PROXMOX_USER`
  - `PROXMOX_SSH_KEY`
- Confirm container metadata:
  - `CT_ID`
  - `APP_DIR`
  - `SERVICE_NAME`
  - `HEALTH_URL`
- Confirm internal node SSH trust for fallback path:
  - `ssh -o BatchMode=yes <ct-node> hostname`

## 2. Deploy command stages inside CT

Recommended sequence:
1. `git config --global --add safe.directory <APP_DIR>`
2. `cd <APP_DIR> && git fetch origin main && git reset --hard origin/main`
3. `cd <APP_DIR> && source .venv/bin/activate && pip install -r requirements.txt`
4. `systemctl restart <SERVICE_NAME>`
5. health check with retry

## 3. Error signatures and actions

### Signature
`Cannot reach <host>:<port> from GitHub runner`

Action
- Do not target private LXC IP from hosted runner.
- Route through public Proxmox host and `pct exec`.

### Signature
`Permission denied (publickey,password)`

Action
- Validate key/user pair.
- Verify public key is present in target host `authorized_keys`.

### Signature
`.../lxc/<id>.conf does not exist`

Action
- You are on wrong cluster node.
- Detect real node from `/etc/pve/nodes/*/lxc/<id>.conf`.
- Route commands to detected node.

### Signature
`fatal: detected dubious ownership in repository`

Action
- Add safe directory before fetch/reset:
  - `git config --global --add safe.directory <APP_DIR>`

### Signature
health endpoint fails after restart

Action
- Inspect service inside CT:
  - `systemctl status <SERVICE_NAME> --no-pager`
  - `journalctl -u <SERVICE_NAME> -n 200 --no-pager`
- Verify app bind/port and endpoint path.

## 4. drone-ssh safety notes

- Keep `set -euxo pipefail`.
- Prefer explicit `if` blocks and explicit state variables.
- Avoid dense control-flow chains where non-zero statuses can leak unpredictably.
- Keep retries bounded and logged.

## 5. Minimal debug bundle for logs

Always print:
- `hostname -f || hostname`
- `id`
- `CURRENT_NODE`, `CT_NODE`, `CT_ID`
- stage markers: `SYNC`, `INSTALL`, `RESTART`, `HEALTH`
- method marker: `pct_exec method=local|ssh_fallback`
