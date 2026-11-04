# Självstudier 1 – Continuous Integration och GitHub Actions

## Syfte

Att förstå hur en CI-pipeline fungerar i praktiken, kunna tolka resultatet och förstå varför automatiserad integration är viktig i ett utvecklingsteam.

---

## Del 1 – Teoretisk fördjupning

### Continuous Integration (CI)

Continuous Integration innebär att kod kontinuerligt integreras i ett gemensamt repository och att automatiska tester körs vid varje förändring.

#### Fördelar

- Snabb återkoppling till utvecklare
- Tidig upptäckt av fel
- Färre integrationsproblem
- Stabilare kodbas
- Högre kvalitet på leveranser

---

### GitHub Actions

GitHub Actions är GitHubs plattform för automatisering.

Används för att:

- Köra tester
- Bygga applikationer
- Granska kodkvalitet
- Deploya applikationer

---

### Events och Triggers

En workflow startas av en händelse.

Exempel:

```yaml
on:
  push:
  pull_request:
```

Vanliga triggers:

- push
- pull_request
- schedule
- workflow_dispatch

---

### Workflow, Job och Step

#### Workflow

Den övergripande processen.

Exempel:

```text
CI
```

#### Job

En grupp aktiviteter.

Exempel:

```yaml
jobs:
  test:
```

#### Step

Enskilda moment i ett jobb.

Exempel:

```yaml
- name: Install dependencies

- name: Run tests
```

#### Samband

```text
Workflow
↓
Job
↓
Step
```

---

### GitHub-hosted Runner

En runner är den maskin som utför arbetet.

Exempel:

```yaml
runs-on: ubuntu-latest
```

GitHub startar då en Linux-maskin som utför jobbet.

---

### Automatisering och Återkoppling

CI ger snabb återkoppling när:

- Tester misslyckas
- Kod bryter mot regler
- Builds misslyckas

Ju snabbare fel upptäcks desto billigare blir de att rätta.

---

## Reflektionsfrågor

### 1. Skillnaden mellan manuell testning och CI

#### Manuell testning

- Utförs av människor
- Tar tid
- Kan missas

#### Continuous Integration

- Körs automatiskt
- Samma tester varje gång
- Snabb återkoppling

#### Slutsats

CI minskar risken för mänskliga misstag och upptäcker problem tidigare.

---

### 2. Problem utan CI

Om flera utvecklare arbetar utan CI kan:

- Buggar upptäckas sent
- Kod konflikta
- Main bli instabil
- Deployment misslyckas

---

### 3. Skillnaden mellan workflow, job och step

#### Workflow -

Hela processen.

#### Job -

En större uppgift i processen.

#### Step -

Enskilt moment inom ett jobb.

---

### 4. Vad gör en runner?

Runnern är maskinen som utför workflowens jobb.

Exempel:

```yaml
runs-on: ubuntu-latest
```

---

### 5. Varför är snabb återkoppling viktigt?

- Fel hittas tidigt
- Felsökning blir enklare
- Kostnader minskar
- Leveranser blir säkrare

---

## Del 2 – Praktisk övning

Här dokumenterar jag den övningen vi gjorde under lektion 2. Alltså detta repo och dess workflow. Väldigt enkelt projekt och inget stort arbete.

### Steg 1 – Undersök pipelinen

Öppna:

```text
.github/workflows/ci.yml
```

Undersök:

#### Vad startar pipelinen?

Exempel:

```yaml
on:
  push:
  pull_request:
```

#### Vilken miljö används?

Exempel:

```yaml
runs-on: ubuntu-latest
```

#### Vilka steg genomförs?

Exempel:

```text
Checkout
Install dependencies
Lint
Test
```

#### Vilka kvalitetskontroller utförs?

```text
Ruff
Pytest
```

---

### Steg 2 – Skapa ett fel

Exempel:

Från:

```python
def add(a, b):
    return a + b
```

Till:

```python
def add(a, b):
    return a - b
```

Commit och push:

```bash
git add .
git commit -m "introduce bug"
git push
```

---

### Steg 3 – Analysera resultatet

Öppna:

```text
Actions
↓
CI
↓
Test
```

Undersök:

#### Vilket steg misslyckades?

Exempel:

```text
Pytest
```

#### Vad säger loggen?

Exempel:

```text
assert -1 == 5
```

#### Konsekvens om felet inte upptäckts?

Programmet hade kunnat levereras med felaktig funktionalitet.

---

### Steg 4 – Åtgärda felet

Rätta:

```python
def add(a, b):
    return a + b
```

Kör:

```bash
git add .
git commit -m "fix test failure"
git push
```

Bekräfta att pipelinen blir grön.

---

## Del 3 – Analys och reflektion

### Scenario

Flera utvecklare arbetar samtidigt med en webbaserad tjänst. Tidigare upptäcktes många fel först inför leverans.

Företaget inför GitHub Actions.

---

### 1. Vilka förbättringar kan företaget förvänta sig?

- Snabbare återkoppling
- Färre buggar
- Stabilare kod
- Högre kvalitet
- Snabbare leveranser

---

### 2. Vilka typer av fel kan fortfarande passera?

- Saknade testfall
- Logiska fel
- Säkerhetsproblem som inte testas
- Prestandaproblem
- Produktionsspecifika problem

CI kan bara hitta problem som faktiskt testas.

---

### 3. Hur påverkas utvecklingsteamet?

Före CI:

```text
Kod
↓
Manuell testning
↓
Sen upptäckt av fel
```

Efter CI:

```text
Kod
↓
Commit
↓
Automatiska tester
↓
Snabb återkoppling
```

---

### 4. Vilken affärsmässig nytta får företaget?

- Lägre kostnader
- Färre fel i produktion
- Ökad kundnöjdhet
- Snabbare leveranser
- Effektivare utvecklingsprocess

---

## Viktiga begrepp för prov och VG

### CI-kedjan

```text
Event
↓
Workflow
↓
Job
↓
Runner
↓
Step
↓
Resultat
```

Exempel:

```text
Pull Request
↓
CI Workflow
↓
Test Job
↓
Ubuntu Runner
↓
Install Dependencies
↓
Ruff
↓
Pytest
↓
5 Passed
```

---

### Skillnaden mellan Ruff och Pytest

#### Ruff

- Statisk kodanalys
- Kör inte programmet
- Kontrollerar kodkvalitet

#### Pytest

- Kör testfall
- Verifierar funktionalitet
- Upptäcker logiska fel

---

### Skillnaden mellan GitHub-hosted och Self-hosted Runner

#### GitHub-hosted

- GitHub sköter miljön
- Ingen egen server behövs
- Enkelt att använda

#### Self-hosted

- Organisationen ansvarar för servern
- Kräver underhåll
- Används för särskilda behov eller interna nätverk
