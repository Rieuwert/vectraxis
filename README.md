# vectraxis.app

Statische site voor **vectraxis.app**: de landingspagina van RekenAppie plus de
privacyverklaring en gebruiksvoorwaarden die Google Play vereist.

| Bestand | Wordt |
| --- | --- |
| `index.html` | https://vectraxis.app/ |
| `privacy.html` | https://vectraxis.app/privacy.html |
| `terms.html` | https://vectraxis.app/terms.html |
| `style.css` | gedeelde opmaak |

Geen build, geen framework, geen externe scripts of fonts — de pagina's laden
niets van servers van derden. Dat is een bewuste keuze: de privacyverklaring
belooft dat er geen trackers zijn, en dan hoort de site zelf er ook geen te
hebben.

## Publiceren

Cloudflare Pages is aan deze repo gekoppeld. Een push naar `main` deployt
automatisch binnen ongeveer een halve minuut. Build command leeg, output
directory `/`.

## Let op bij wijzigen

`privacy.html` is geen vrijblijvende tekst. De inhoud moet blijven kloppen met
(a) wat de app werkelijk doet en (b) het **Data safety**-formulier in Google
Play Console — reviewers leggen die twee naast elkaar. Komt er een SDK,
permissie of datastroom bij in de app, werk dan beide bij, inclusief de datum
bovenaan de pagina.

De app linkt rechtstreeks naar `privacy.html` vanuit het scherm "Over
RekenAppie". Die URL mag dus niet zomaar veranderen; hij staat vast in
`lib/config/app_links.dart` in de app-repo.
