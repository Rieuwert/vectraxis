# vectraxis.app

Statische site voor **vectraxis.app**: de Vectraxis-homepage, de productsectie
van RekenAppie, en de privacyverklaring en gebruiksvoorwaarden die Google Play
vereist.

| Bestand | Wordt | Wat het is |
| --- | --- | --- |
| `index.html` | `/` | Vectraxis: werkwijze, producten, contact |
| `rekenappie/index.html` | `/rekenappie/` | Productpagina RekenAppie |
| `rekenappie/visie.html` | `/rekenappie/visie` | Visie en volledige functiebeschrijving |
| `rekenappie/changelog.html` | `/rekenappie/changelog` | Versiegeschiedenis |
| `privacy.html` | `/privacy` | **Verplicht voor Play.** Niet verplaatsen. |
| `terms.html` | `/terms` | Gebruiksvoorwaarden |
| `style.css` | — | Gedeelde opmaak voor alle pagina's |
| `fonts/` | `/fonts/…` | IBM Plex Sans, Serif en Mono (woff2) |
| `img/` | `/img/…` | App-icoon, logo en schermafbeeldingen |

Geen build, geen framework, geen externe scripts. **Ook de lettertypes staan
hier**, en dat is geen esthetische keuze: een webfont van een CDN stuurt het
IP-adres van elke bezoeker naar die derde partij, en de privacyverklaring
belooft dat er niets naar derden gaat. Die belofte geldt ook voor de site zelf.

## Opzet van het ontwerp

Vectraxis is de neutrale schil — inkt op papier, haarlijnen, cijfers in mono.
**De kleur komt van het product.** Een productpagina zet de klasse
`t-rekenappie` op `<body>` en krijgt daarmee het blauw van de app; een volgend
product krijgt een eigen klasse met een eigen kleur. Zo blijft de schil
herkenbaar terwijl elk product zijn eigen gezicht houdt.

Alle kleuren staan als tokens op `:root` en worden op drie plekken herhaald
voor de donkere variant: `prefers-color-scheme` (met `:not([data-theme="light"])`)
en `[data-theme="dark"]`. Definieer nooit een kleur uitsluitend binnen een
media query — dan valt hij weg in de standaardstand van de bezoeker.

## Publiceren

Cloudflare Pages is aan deze repo gekoppeld. Een push naar `main` deployt
automatisch binnen ongeveer een halve minuut. Build command leeg, output
directory `/`.

De submap `rekenappie/` werkt vanzelf: Cloudflare Pages serveert
`rekenappie/index.html` op `/rekenappie/` en `rekenappie/visie.html` op
`/rekenappie/visie`, net zoals `privacy.html` op `/privacy` komt.

## Lokaal bekijken

Open de bestanden **niet** rechtstreeks met `file://` — alle paden zijn
root-absoluut (`/style.css`), dus je hebt een server nodig die de site vanaf de
hoofdmap serveert:

```powershell
npx --yes http-server . -p 8790 -c-1
```

## Let op bij wijzigen

`privacy.html` is geen vrijblijvende tekst. De inhoud moet blijven kloppen met
(a) wat de app werkelijk doet en (b) het **Data safety**-formulier in Google
Play Console — reviewers leggen die twee naast elkaar. Komt er een SDK,
permissie of datastroom bij in de app, werk dan beide bij, inclusief de datum
bovenaan de pagina.

De app linkt rechtstreeks naar `/privacy` en `/terms` vanuit het scherm "Over
RekenAppie". Die URL's mogen dus niet veranderen; ze staan vast in
`lib/config/app_links.dart` in de app-repo.

De cijfers op de homepage en de productpagina (vraagvormen, SLO-doelen, tests)
komen uit `CURRICULUM_DEKKING.md` en `VRAAGVORMEN.md` in de app-repo. Werk ze
bij zodra die opnieuw gegenereerd zijn, anders staan er verouderde getallen op
een pagina die juist over controleerbaarheid gaat.
