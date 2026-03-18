# Kort sammanfattning av SBOM

Datum: 2026-03-18

En SBOM genererades för den härdade imagen `my-app:hardened` i CycloneDX-format med Trivy.

## Resultat i korthet

- Image: `my-app:hardened`
- SBOM-format: `CycloneDX`
- Specifikation: `1.6`
- Verktyg: `trivy 0.69.3`
- Output-fil: `sbom.json`

## Vad SBOM-filen visar

SBOM-filen innehåller en strukturerad förteckning över komponenter i containern och metadata om imagen. Den visar bland annat:

- vilken container som analyserades
- vilka lager och komponentreferenser som ingår
- vilka Python-paket och systempaket som finns i imagen
- vilket verktyg som genererade rapporten

## Kort slutsats

SBOM:en ger spårbarhet och bättre insyn i innehållet i den härdade containern. Den kan användas som underlag för säkerhetsgranskning, dokumentation och senare verifiering i pipeline eller rapport.

## Underlag

- `sbom.json`
