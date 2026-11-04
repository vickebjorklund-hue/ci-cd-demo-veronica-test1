# Dokumentation av min kurs CI/CD

I denna filen dokumentearr jag alla övningar som görs under kursen. Detta för att jag ska kunna gå tillbaka och repetera allt vi gör.
Repot ligger i `Github` och jag pushar efter varje lektion/övning är slutförd.

Repot i sig `https://github.com/vickebjorklund-hue/ci-cd-demo-veronica-test1` är mitt test repo som jag sparar för övningarnas skull.

Vi har övningsuppgifter under lektionerna som benämns `Övning under lektion` och vi har uppgifter som ska lämnas in som benämns `Inlämningsuppgift - dag x`.
Jag kommer även spara våra fördjupningsövningar och självstudier i sparata Markdown som heter `STUDIER_X.md` i detta repo.

Alla inlämningsuppgifter pushas till `https://github.com/cloudfactoreu/devops25-ci-cd-demo` som är vårt huvudrepo, och mitt lokala repo `https://github.com/vickebjorklund-hue/veronica-ci-cd-demo1` som är en fork på huvudrepot.

## Inlämningsuppgift - dag 1

Jag skapade en branch från main, gjorde en dokumentationsändring i README, commitade ändringen lokalt, pushade branchen till GitHub och skapade en Pull Request mot main. Jag mergeade inte eftersom övningen handlade om Git-flödet och Pull Request-processen.

---

## Övning under lektion - dag 2

introducerar en bug i ett litet projekt, för att kunna följ `git action` och avläsa informationen.

### Hur jag gjorde

Jag skapade ett eget repository (som kommer bli mitt test repo under hela kursen), konfigurerade en GitHub Actions-pipeline som automatiskt kör pytest vid varje push. Därefter introducerade jag medvetet ett fel i applikationen, observerade att teststeget misslyckades och analyserade loggarna för att spåra felet tillbaka till källkoden. Efter korrigering verifierade jag att pipelinen åter gick igenom. Detta visar hur CI automatiskt kvalitetssäkrar kod innan den kan levereras vidare.

![ACTION FAIL](/screenshots/01_fail.png)

![GREEN](/screenshots/02_green.png)

---

## Inlämningsuppgift - dag 2

Beskrivning av vad jag gjorde.
En push till branchen startade inte CI-jobbet. Workflowen var konfigurerad att reagera på en Pull Request mot main. När PR:n skapades triggades workflowen, men GitHub krävde godkännande eftersom ändringen kom från en fork.

![DAY 2](/screenshots/03_day2_test.png)

## Dag 2

### Syfte

Att förstå hur en CI-pipeline fungerar och hur GitHub Actions automatiserar tester och kvalitetskontroller.

---

### Hur CI startas

Workflowen kan triggas av:

```yaml
on:
  push:
  pull_request:
```

I vår övning startades CI när en Pull Request skapades mot `main`.

---

### Läsning av loggar

Vid ett fel:

```text
Actions
↓
Välj körning
↓
Öppna det röda steget
```

Läs alltid den faktiska felloggen, inte bara att pipeline-status är röd.

---

## Ruff och Pytest

### Ruff

- Statisk kodanalys
- Läser koden utan att köra den
- Hittar stilfel och vissa programmeringsfel

### Pytest

- Kör testfall
- Verifierar att programmet fungerar korrekt
- Hittar logiska fel

| Ruff | Pytest |
| -------- | -------- |
| Läser kod | Kör kod |
| Kodkvalitet | Funktionalitet |
| Statisk analys | Testkörning |

---

## GitHub-hosted vs Self-hosted Runner

### GitHub-hosted

- GitHub ansvarar för miljön
- Ingen installation krävs
- Passar de flesta projekt

### Self-hosted

- Organisationen ansvarar för servern
- Kräver underhåll och säkerhetshantering
- Kan användas för interna system eller särskild hårdvara

---

## När används Self-hosted Runners?

Exempel:

- Interna API:er
- Företagsnätverk
- Databaser bakom brandvägg
- GPU eller specialutrustning
- Särskilda säkerhetskrav

---

## Kunskapsmål efter dag 2

Jag ska kunna:

- Beskriva kedjan **Händelse → Workflow → Jobb → Runner → Steg → Resultat**
- Hitta och tolka en fellogg i GitHub Actions
- Förklara skillnaden mellan Ruff och Pytest
- Förstå hur en Pull Request triggar CI
- Resonera kring när GitHub-hosted respektive Self-hosted runners används
- Förklara varför snabb återkoppling är viktig i Continuous Integration

---

## Kort sammanfattning

CI automatiserar tester och kvalitetskontroller varje gång kod integreras i projektet. GitHub Actions använder workflows som körs på runners och består av olika jobb och steg. Genom verktyg som Ruff och Pytest kan fel upptäckas tidigt, vilket ger snabb återkoppling, högre kvalitet och säkrare leveranser.
