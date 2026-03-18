# Lab 2 Container Security

Detta repo visar ett före/efter-upplägg för container-hardening. Jag byggde först en medvetet sårbar Flask-container och skannade den för att få ett utgångsläge. Därefter härdade jag containern med en modernare och mindre basimage, non-root user, tydligare runtime-konfiguration och bättre dependency-hantering. Jag genererade också en SBOM för den härdade imagen och verifierade policy enforcement i Kubernetes via Gatekeeper Lab i Mission Control.

## Det jag gjorde

1. Skapade en medvetet sårbar app i `app.py` och `Dockerfile.vulnerable`.
2. Byggde och skannade den sårbara imagen med Trivy.
3. Härdade containern i `Dockerfile.hardened`.
4. Byggde och skannade den härdade imagen och jämförde resultatet före och efter.
5. Genererade en SBOM i CycloneDX-format för den härdade imagen.
6. Testade Gatekeeper-policies i Mission Control med en `Bad Pod` och en `Hardened Pod`.

## Verktyg

- `Docker` för att bygga images
- `Trivy` för image scanning och SBOM-generering
- `Python / Flask` för demoapplikationen
- `Gatekeeper` via `Mission Control` för policy enforcement
- `Git` och `GitHub` för versionshantering och inlämning

## Viktiga filer

- `Dockerfile.vulnerable`
- `Dockerfile.hardened`
- `app.py`
- `requirements.txt`
- `scan-before.txt`
- `scan-after.txt`
- `sbom.json`
- `policies/require-labels-template.yaml`
- `policies/require-team-label.yaml`

## Resultat

- Sårbar image: `my-app:vulnerable`
  - storlek: `1.46GB`
  - Trivy: `1299 HIGH`, `181 CRITICAL`
- Härdad image: `my-app:hardened`
  - storlek: `206MB`
  - Trivy: `2 HIGH`, `2 CRITICAL`

## Screenshots

- Trivy före hardening: [screenshots/trivy-before.png](./screenshots/trivy-before.png)
- Trivy efter hardening: [screenshots/trivy-after.png](./screenshots/trivy-after.png)
- Gatekeeper deny: [screenshots/gatekeeper-deny.png](./screenshots/gatekeeper-deny.png)
- Gatekeeper pass: [screenshots/gatekeeper-pass.png](./screenshots/gatekeeper-pass.png)

## Extra rapportmaterial

Mer underlag finns i `Material för rapport lab2/`, bland annat:

- `reflection.md`
- `lab2-summary.md`
- `scan-before-summary.md`
- `scan-comparison-summary.md`
- `sbom-summary.md`
- extra screenshots från Gatekeeper Lab

## Gatekeeper

Gatekeeper var redan installerat i det delade klustret. Tester genomfördes via Mission Control Gatekeeper Lab, inte via `kubectl apply`, eftersom `ConstraintTemplates` och `Constraints` är kluster-scope-resurser och kräver högre rättigheter.
