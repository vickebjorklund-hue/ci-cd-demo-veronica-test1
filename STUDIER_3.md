# Självstudier 3 – Från Continuous Integration till Continuous Delivery

## Syfte

Syftet med självstudien var att förstå vad som händer efter att koden har testats och godkänts i CI-processen samt hur applikationer förbereds för leverans och driftsättning.

---

## Viktiga begrepp

### Continuous Integration (CI)

Automatiserade tester och kvalitetskontroller körs när ny kod integreras i projektet.

### Continuous Delivery (CD)

Applikationen hålls i ett leveransklart skick och kan distribueras när organisationen väljer.

### Continuous Deployment

Godkända ändringar distribueras automatiskt till produktion utan manuella steg.

### Build Artifact

Resultatet från en byggprocess, exempelvis en containerimage eller ett kompilerat program.

### Container Image

En paketerad version av applikationen inklusive nödvändiga beroenden.

### Deployment

Processen att installera och starta applikationen i en miljö.

### Rollback

Möjligheten att återgå till en tidigare fungerande version om något går fel.

---

## Dockerfile

I Dockerfile kan man identifiera:

- Vilken basimage som används
- Hur beroenden installeras
- Hur applikationskoden kopieras in
- Vilket kommando som startar applikationen

Dockerfile används för att skapa en reproducerbar containerimage som kan köras i olika miljöer.

---

## Bygga en containerimage

Build-processen skapar en image:

```bash
docker build -t devops-course:1.0 .
```

Kontroll:

```bash
docker images
```

Den skapade imagen kan därefter användas för att starta applikationen.

---

## Varför containerimages används

Fördelar:

- Samma miljö överallt
- Färre "det fungerar på min dator"-problem
- Enklare distribution
- Snabbare leveranser
- Konsekvent drift mellan utveckling, test och produktion

---

## Från CI till CD

Efter att testerna har passerat krävs vanligtvis:

1. Bygg av artifact/containerimage
2. Versionshantering
3. Publicering till registry
4. Deployment till testmiljö
5. Verifiering
6. Deployment till produktion

---

## Om en deployment misslyckas

Om driftsättningen misslyckas bör:

- Felet upptäckas automatiskt
- Deployment stoppas
- Loggar analyseras
- En rollback genomföras vid behov

Det minskar risken för driftstörningar.

---

## Kontroller efter deployment

Exempel på verifieringar:

- Applikationen startar korrekt
- API:er svarar
- Hälsokontroller (health checks) fungerar
- Databasanslutningar fungerar
- Inga kritiska fel visas i loggarna

---

## Viktiga lärdomar

- CI verifierar kvalitet genom tester.
- CD förbereder och levererar godkänd kod.
- Containerimages gör leveranser mer förutsägbara.
- Deployment måste kunna verifieras.
- Rollback är en viktig säkerhetsmekanism.
- Målet är att leverera förändringar snabbt och säkert.

---

## Kort sammanfattning

Continuous Integration säkerställer att koden fungerar genom automatiserade tester. Continuous Delivery tar nästa steg genom att paketera applikationen och göra den redo för leverans. Med hjälp av Docker kan samma containerimage köras i olika miljöer, vilket förenklar deployment och minskar risken för miljörelaterade problem. Om något går fel måste organisationen kunna verifiera deploymenten och vid behov genomföra en rollback till en tidigare fungerande version.
