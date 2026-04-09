# Contributing

Gracias por contribuir a `proxmox-cicd-deploy-skill`.

## Scope

Este repositorio publica la skill `proxmox-cicd-deploy-skill` para uso comunitario en Codex.

## Repo Structure

- `SKILL.md`: instrucciones principales de la skill.
- `agents/openai.yaml`: metadata de interfaz para listados/chips.
- `references/`: material de apoyo reutilizable.
- `examples/`: ejemplos de workflows listos para adaptar.
- `README.md`: instalación, triggers y uso.

## Contribution Rules

- No incluir secretos ni datos privados.
- Evitar hardcodes de entornos reales; usar placeholders (`CT_ID`, `APP_DIR`, `EXPECTED_NODE`, `SERVICE_NAME`, `HEALTH_URL`, etc.).
- Mantener ejemplos reproducibles y orientados a buenas prácticas.
- Mantener cambios enfocados y pequeños por PR.

## Local Validation

Ejecuta validación antes de abrir PR.

### Bash

```bash
python "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-creator/scripts/quick_validate.py" .
```

### PowerShell

```powershell
$codexHome = if ($env:CODEX_HOME) { $env:CODEX_HOME } else { Join-Path $HOME '.codex' }
python (Join-Path $codexHome 'skills/.system/skill-creator/scripts/quick_validate.py') .
```

Resultado esperado:

```text
Skill is valid!
```

## Pull Request Checklist

- [ ] `SKILL.md` actualizado y consistente con el objetivo de la skill.
- [ ] `agents/openai.yaml` consistente con la descripción visible.
- [ ] Referencias actualizadas si cambian flujos/error signatures.
- [ ] Ejemplos actualizados si cambian stages o placeholders.
- [ ] `README.md` actualizado si cambian instalación, triggers o uso.
- [ ] Validación local ejecutada y pasando.
- [ ] Sin secretos ni datos de infraestructura privada.

## Versioning

Seguimos SemVer en tags (`vMAJOR.MINOR.PATCH`):

- `PATCH`: fixes o clarificaciones sin cambiar comportamiento esperado.
- `MINOR`: nuevas capacidades backward-compatible.
- `MAJOR`: cambios incompatibles en comportamiento o interfaz de uso.