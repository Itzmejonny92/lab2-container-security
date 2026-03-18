# Kort sammanfattning av Trivy-scan

Datum: 2026-03-18

Den sårbara imagen `my-app:vulnerable` byggdes från `Dockerfile.vulnerable` och skannades med Trivy innan några säkerhetsförbättringar gjordes.

## Resultat i korthet

- Image: `my-app:vulnerable`
- Skannad via exporterad tar-fil: `my-app-vulnerable.tar`
- Verktyg: `trivy`
- Hittade sårbarheter med filtrering `HIGH,CRITICAL`:
  - `HIGH`: 1299
  - `CRITICAL`: 181

## Kort slutsats

Scanningen visar att imagen är kraftigt sårbar i sitt nuvarande skick. En stor del av fynden kommer från basimagen och installerade paket, vilket gör den lämplig som utgångsläge för labben innan vi bygger en säkrare version och jämför resultat före och efter.

## Underlag

Full rapport finns i:

`scan-before.txt`
