# Jämförelse före och efter hardening

Datum: 2026-03-18

## Före hardening

- Image: `my-app:vulnerable`
- Storlek: `1.46GB`
- Trivy-resultat `HIGH,CRITICAL`:
  - `HIGH`: 1299
  - `CRITICAL`: 181

## Efter hardening

- Image: `my-app:hardened`
- Storlek: `206MB`
- Trivy-resultat `HIGH,CRITICAL`:
  - `HIGH`: 2
  - `CRITICAL`: 2

## Kort analys

Hardening gav en mycket tydlig förbättring. Den härdade imagen blev betydligt mindre och antalet allvarliga sårbarheter minskade kraftigt jämfört med den sårbara versionen.

De största förbättringarna kom från:

- Ny basimage: `python:3.12-slim-bookworm`
- Uppgraderad Flask-version
- Installation via `requirements.txt`
- Körning som icke-root användare
- Tydligare containerkonfiguration med `WORKDIR`, `EXPOSE` och `HEALTHCHECK`

## Underlag

- `scan-before.txt`
- `scan-after.txt`
