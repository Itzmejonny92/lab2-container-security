# Lab 2 Sammanfattning

Datum: 2026-03-18

I den här labben arbetade jag med container-säkerhet genom att först skapa en medvetet sårbar Flask-applikation och sedan stegvis härda den. Jag började med en enkel `app.py` och en sårbar Dockerfile baserad på `python:3.8`, där Flask `1.0.0` installerades direkt i imagen. Den versionen byggdes som `my-app:vulnerable` och skannades med Trivy för att ge ett tydligt utgångsläge.

Den första skanningen visade en mycket hög risknivå. Den sårbara imagen var stor, cirka `1.46GB`, och rapporten innehöll `1299 HIGH` samt `181 CRITICAL` sårbarheter. Jag sparade både full rapport och en kort sammanfattning som underlag för jämförelse senare i labben.

Efter det härdade jag container-konfigurationen genom att byta till `python:3.12-slim-bookworm`, lägga beroenden i `requirements.txt`, köra applikationen som en icke-root-användare, använda `--no-cache-dir` vid installation samt lägga till `WORKDIR`, `EXPOSE` och `HEALTHCHECK`. Den här versionen byggdes som `my-app:hardened`.

När den härdade imagen skannades med Trivy förbättrades resultatet tydligt. Storleken minskade till `206MB`, och mängden allvarliga sårbarheter sjönk till `2 HIGH` och `2 CRITICAL`. Det visade konkret hur stor skillnad modernare basimage, mindre attackyta och bättre containerkonfiguration kan göra.

Jag genererade också en SBOM i CycloneDX-format för den härdade imagen. SBOM-filen visar vilka komponenter och paket som faktiskt finns i containern och ger bättre spårbarhet, dokumentation och möjlighet att följa upp framtida sårbarheter.

I Gatekeeper-delen använde jag Mission Control i stället för `kubectl apply`, eftersom policyresurserna är kluster-scope och kräver högre rättigheter. Jag verifierade vilka constraints som redan var aktiva i namespace `m4k-gang`, granskade policy violations och testade sedan en `Bad Pod` mot en `Hardened Pod`. Resultatet blev att den dåliga poden blockerades av flera policies, medan den hårdade poden tilläts med endast en varning om default service account.

Som avslutning verifierade jag också att inga uppenbara hemligheter eller känsliga filer låg öppna för commit i repot. De stora exporterade image-filerna ignoreras korrekt via `.gitignore`, och inga tydliga secret-liknande filer hittades i projektet.

Repot förbereddes därefter för inlämning så att det så långt som möjligt följer lärarens önskade struktur. Därför finns nyckelfiler som `sbom.json`, `scan-before.txt`, `scan-after.txt` och en separat `screenshots/`-mapp i repo-roten, samtidigt som allt extra rapportmaterial ligger kvar i `Material för rapport lab2/`.

Min slutsats från labben är att container-säkerhet blir betydligt starkare när scanning, hardening, SBOM och policy enforcement används tillsammans. Varje del fångar olika typer av risker, och tillsammans ger de ett mycket bättre skydd än om man bara fokuserar på att få containern att fungera tekniskt.
