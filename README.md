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
