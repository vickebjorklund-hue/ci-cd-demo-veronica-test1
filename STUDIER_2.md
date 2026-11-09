# Dag 3 – Automatiserade tester, kodkvalitet och Quality Gates

## Syfte

Målet med övningen var att förstå hur tester och kodkontroller används för att upptäcka fel innan kod når huvudbranchen samt hur CI-pipelines fungerar tillsammans med Pull Requests.

---

## Vad som gjordes

### 1. Köra tester lokalt

Projektet verifierades med:

```bash
python -m pytest -v
```

samt kodgranskning med:

```bash
ruff check app tests
```

Pytest kontrollerade att funktionerna fungerade korrekt medan Ruff kontrollerade kodkvaliteten.

---

### 2. Skapa ett avsiktligt fel

I testfilen `tests/test_service.py` ändrades:

```python
assert add(2, 3) == 5
```

till:

```python
assert add(2, 3) == 6
```

Syftet var att skapa ett kontrollerat testfel.

Resultatet blev:

```text
1 failed, 4 passed
```

---

### 3. Skapa en röd pipeline

Ändringen committades och pushades till en separat demonstrationsbranch.

När GitHub Actions körde CI-pipelinen misslyckades teststeget eftersom testet förväntade sig värdet `6` medan funktionen faktiskt returnerade `5`.

I loggen kunde felet identifieras genom raden:

```text
assert 5 == 6
```

---

## Vad felet visade

Den röda CI-körningen visade att:

- testerna fungerar som en kvalitetssäkring
- fel upptäcks automatiskt
- kod med felaktiga testresultat stoppas innan merge

En röd pipeline betyder att något måste undersökas, men inte automatiskt att applikationen är trasig.

---

## Hur felet rättades

Testet ändrades tillbaka till:

```python
assert add(2, 3) == 5
```

Därefter verifierades:

```bash
python -m pytest -q
ruff check app tests
```

När alla tester passerade committades och pushades rättningen.

GitHub Actions körde då en ny pipeline som blev grön.

---

## Quality Gates

Övningen demonstrerade hur automatiska kontroller fungerar som en **Quality Gate**.

Exempel på Quality Gates:

- Godkända tester (Pytest)
- Godkänd kodkvalitet (Ruff)
- Pull Request
- Kodgranskning (Code Review)

Dessa kontroller hjälper till att förhindra att felaktig kod hamnar i `main`.

---

## Viktiga lärdomar

- Pytest testar funktionalitet.
- Ruff analyserar kodkvalitet.
- Tester bör köras både lokalt och i CI.
- En röd pipeline ska analyseras genom att läsa loggarna.
- Pull Requests kan kopplas till automatiska kontroller.
- Quality Gates hjälper team att hålla hög kvalitet innan merge.

---

1. Varför räcker det inte att koden går att bygga?

Att koden går att bygga innebär bara att den kan kompileras eller startas utan syntaxfel. Det garanterar inte att funktionerna fungerar korrekt. En applikation kan byggas framgångsrikt men ändå innehålla logiska fel, felaktiga beräkningar eller trasiga funktioner. Därför behövs automatiserade tester som verifierar att programmet beter sig som förväntat.

2. Varför bör vissa tester köras oftare än andra?

Vissa tester är snabba och kritiska för applikationens grundläggande funktionalitet, exempelvis unit tester. Dessa bör köras vid varje commit eller Pull Request för att ge snabb återkoppling.

Mer omfattande tester, till exempel integrationstester och end-to-end-tester, tar längre tid och kan därför köras mer sällan, exempelvis vid nattliga körningar eller inför en release.

3. Vad innebär ett regressionstest?

Ett regressionstest kontrollerar att tidigare fungerande funktionalitet fortfarande fungerar efter att ny kod har lagts till eller ändrats.

Syftet är att upptäcka om en förändring oavsiktligt har förstört något annat i systemet.

Exempel:

Ny funktion implementeras
↓
Regressionstester körs
↓
Kontroll att tidigare funktioner fortfarande fungerar

4. Kan en pipeline vara grön trots att applikationen innehåller fel?

Ja.

En grön pipeline betyder endast att de tester och kontroller som finns definierade har passerat. Om viktiga testfall saknas kan fel fortfarande finnas i applikationen.

Exempel:

Testerna täcker inte alla funktioner.
Ett logiskt fel saknar test.
Ett prestandaproblem kontrolleras inte.
Ett säkerhetsproblem ingår inte i testsviten.

Därför betyder en grön pipeline inte att applikationen är felfri.

5. Vilka risker uppstår om testerna tar mycket lång tid?

Om testerna tar lång tid får utvecklarna långsammare återkoppling. Det kan leda till att:

Fler fel hinner introduceras innan resultaten kommer.
Utvecklare väntar längre på svar från CI-pipelinen.
Produktiviteten minskar.
Vissa tester börjar hoppas över.
Leveranser fördröjs.

En viktig princip inom CI är därför att de vanligaste testerna ska ge snabb återkoppling så att fel upptäcks så tidigt som möjligt.

Kort VG-sammanfattning

Att koden går att bygga innebär inte att den fungerar korrekt. Automatiserade tester används för att verifiera funktionalitet och upptäcka fel tidigt. Unit tester körs ofta eftersom de är snabba, medan tyngre tester kan köras mer sällan. Regressionstester säkerställer att tidigare fungerande funktioner inte har gått sönder. En grön pipeline visar endast att de befintliga testerna passerat, inte att applikationen är helt felfri. För långa testkörningar ger långsammare återkoppling och minskar effektiviteten i utvecklingsprocessen.