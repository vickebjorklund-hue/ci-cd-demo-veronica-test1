# ci-cd-demo-veronica-test1

## En enkel lektions övning

introducerar en bug i ett litet projekt, för att kunna följ `git action` och avläsa informationen.

## Hur jag gjorde

Jag skapade ett eget repository, konfigurerade en GitHub Actions-pipeline som automatiskt kör pytest vid varje push. Därefter introducerade jag medvetet ett fel i applikationen, observerade att teststeget misslyckades och analyserade loggarna för att spåra felet tillbaka till källkoden. Efter korrigering verifierade jag att pipelinen åter gick igenom. Detta visar hur CI automatiskt kvalitetssäkrar kod innan den kan levereras vidare.

![ACTION FAIL](/screenshots/01_fail.png)

![GREEN](/screenshots/02_green.png)
