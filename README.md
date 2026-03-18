# Lab 2 Container Security

Detta repo visar ett fore/efter-upplagg for container-hardening. Jag byggde forst en medvetet sarbar Flask-image och skannade den med Trivy. Darefter hardades imagen med nyare basimage, non-root user, mindre attackyta och tydligare runtime-konfiguration.

## Filer i projektet

- `app.py`: enkel Flask-app
- `Dockerfile.vulnerable`: medvetet sarbar containerdefinition
- `Dockerfile.hardened`: hardad containerdefinition
- `requirements.txt`: Python-beroenden
- `policies/`: Gatekeeper-policyfiler som visar YAML-strukturen

## Rapportunderlag

Rapportfiler och screenshots ligger i `Material för rapport lab2/`.

Viktiga underlag:

- `scan-before.txt`
- `scan-after.txt`
- `sbom.json`
- `scan-before-summary.md`
- `scan-comparison-summary.md`
- `sbom-summary.md`
- `active constraints.png`
- `bad pod resultat.png`
- `hardened pod test.png`

## Viktiga resultat

- Sårbar image: `my-app:vulnerable`
  - storlek: `1.46GB`
  - Trivy: `1299 HIGH`, `181 CRITICAL`
- Hardad image: `my-app:hardened`
  - storlek: `206MB`
  - Trivy: `2 HIGH`, `2 CRITICAL`

## Gatekeeper

Gatekeeper var redan installerat i det delade klustret. Policies och dry-run-test genomfordes via Mission Control Gatekeeper Lab, inte via `kubectl apply`, eftersom ConstraintTemplates och Constraints ar kluster-scope-resurser.

## Slutsats

Labben visar hur mycket en mindre, modernare och mer restriktiv containerkonfiguration kan minska risknivan. Den visar ocksa hur SBOM och policy enforcement kompletterar traditionell image scanning.
