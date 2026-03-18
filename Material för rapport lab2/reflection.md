# Reflektion

I den här labben lärde jag mig att container-säkerhet handlar om mycket mer än bara att få en app att starta. Val av basimage, beroendeversioner, root eller non-root och hur mycket som installeras i imagen påverkar risknivån direkt. Jag såg tydligt hur en gammal och tung image gav mycket fler allvarliga Trivy-fynd än en mindre och hårdad image. Jag lärde mig också att hardening inte bara handlar om sårbarheter utan också om drift, till exempel health checks och tydligare runtime-beteende.

SBOM är viktigt eftersom det ger insyn i exakt vad som finns i imagen. Det gör det lättare att spåra beroenden, förstå vad som faktiskt deployas och reagera snabbare om en ny sårbarhet upptäcks i ett paket. SBOM fungerar därför som ett underlag för både säkerhetsarbete och dokumentation.

Policy-enforcement med Gatekeeper förändrar också hur man jobbar med Kubernetes. I stället för att bara hoppas att teamet följer best practices kan man automatiskt stoppa eller varna för osäkra resurser redan innan de skapas. Det gör att säkerhet flyttas tidigare i arbetsflödet och blir en naturlig del av deploymentprocessen i stället för en manuell efterkontroll.
