# idatasolutions.nl

Bedrijfssite van iData Solutions (Issam El-Abdellaoui, Vlaardingen, KVK 42003397).
Eén statische pagina, `index.html`, met alle CSS inline. Geen build-stap, geen
dependencies, geen framework. Bewust zo: de site moet over vijf jaar nog te openen
en aan te passen zijn zonder eerst een toolchain te installeren.

## Positionering

De site verkoopt **software op maat en koppelingen tussen systemen**, niet onderwijs.
Het onderscheid is dat er met AI-tooling wordt ontworpen, gebouwd en getest, waardoor
opleveren sneller en goedkoper gaat dan bij een traditioneel bureau. MijnLVS en
Al-Hijra staan op de site als voorbeeldprojecten, niet als hoofdproduct.

## Hosting

GitHub Pages, repo `issam85/idatasolutions-website`, branch `main`, root.
Pushen naar `main` publiceert. Het `CNAME`-bestand hoort in de repo te blijven staan.

Domein staat bij TransIP, DNS wijst naar GitHub:

- `@`: 4x A (185.199.108-111.153) en 4x AAAA (2606:50c0:8000-8003::153)
- `www`: CNAME naar `issam85.github.io.`

Mail loopt via een **e-mailpakket van TransIP** (mailbox info@idatasolutions.nl,
aangemaakt 31-07-2026). TransIP beheert de MX-records. Pas die niet met de hand aan,
en laat bij elke wijziging in de zone de vier A-records, vier AAAA-records en de
`www`-CNAME met rust: die houden de site in de lucht.

### Als het HTTPS-certificaat blijft hangen

`https_certificate.state` blijft soms leeg terwijl de DNS allang goed staat: GitHub
begint de aanvraag dan nooit. Los het domein los en koppel het opnieuw, daarna is het
binnen minuten `approved`:

```bash
'{"cname":null}' | gh api -X PUT repos/issam85/idatasolutions-website/pages --input -
gh api -X PUT repos/issam85/idatasolutions-website/pages -f cname=idatasolutions.nl
gh api -X PUT repos/issam85/idatasolutions-website/pages -F https_enforced=true
```

`https_enforced` meesturen voordat het certificaat bestaat geeft een 404. Let op: het
loskoppelen verwijdert het `CNAME`-bestand uit de repo en het opnieuw koppelen zet het
terug, dus je lokale kloon loopt daarna achter. Eerst `git pull --rebase`.

## Schrijfstijl

Geen lange streepjes (em dash). Gebruik een komma, dubbele punt of haakjes.

Geen AI-marketingtaal: geen "naadloos", geen "krachtig", geen "niet alleen X maar ook
Y", geen zinnen als "software die het werk echt lichter maakt". Plat en concreet
schrijven, zoals een ondernemer over zijn eigen werk praat.

Zet geen beloftes op de site die niet nagekomen kunnen worden. Teksten over prijzen,
opleverdata en reactietijden altijd eerst aan Issam voorleggen.

## Commits

Privé-project: commit met `i.abdellaoui@gmail.com`, niet met het werkadres uit de
globale git-config.
