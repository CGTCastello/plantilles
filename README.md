# Generador de plantilles · CGT Castelló

Editor web de plantilles gràfiques de CGT Castelló. Qualsevol persona del sindicat pot fer, des del mòbil o l'ordinador, una peça amb el sistema de disseny del sindicat: nota de premsa, convocatòria, cita, dada, comunicat, carrusel, imatge web o miniatura per a enllaços.

Tot passa al navegador: les fotos no es pugen enlloc.

## Què fa

- **9 plantilles**: Nota de premsa, Convocatòria, Cita o lema, La dada, Comunicat sense foto, Portada de carrusel, Balanç (files), Imatge web (1024×492) i Miniatura d'enllaç (1200×630).
- **Formats**: post (1080×1350), story (1080×1920), cartell A4 (300 ppp) i A3 (~250 ppp).
- **Arxius**: PNG, JPG o PDF. Els carrusels es baixen en ZIP o en un PDF de diverses pàgines.
- **Carrusel** de fins a 10 diapositives, amb comptador «2/5» i «Llisca →».
- **Bilingüe**: valencià, castellano o les dues (una peça per idioma).
- **Difuminar cares**: es toca cada cara a la previsualització.
- **Versió per a fotocopiar** (blanc i negre, logo en trama).
- **Logos temàtics**: normal, morat, verd, orgull, trans.
- **Requadre de text** opcional per a aclariments i avisos.
- **Enllaços a una plantilla**: `index.html#conv-a4` obri la convocatòria en A4. Amb `?t=…&dia=…&hora=…&lloc=…` es poden precarregar textos.

## Publicar-ho a GitHub Pages

1. Puja aquesta carpeta a un repositori de GitHub (pot ser de l'organització del sindicat).
2. A **Settings → Pages**, tria *Deploy from a branch*, branca `main`, carpeta `/ (root)`.
3. En un parell de minuts estarà a `https://<usuari-o-organització>.github.io/<repositori>/`.
4. Opcional: un subdomini propi (per exemple `cartells.cgtcastello.org`) amb un arxiu `CNAME` i un registre DNS CNAME cap a `<usuari-o-organització>.github.io`.

No cal compilar res: és HTML, CSS i JavaScript sense dependències externes. Les fonts (Anton i Open Sans) i les llibreries (jsPDF i JSZip) són dins del repositori.

## Provar-ho en local

```bash
python3 -m http.server 8000
# obri http://localhost:8000
```

## Estructura

```
index.html        L'editor sencer (HTML + CSS + JS)
fonts/            Anton i Open Sans (SIL OFL 1.1) + fonts.css
vendor/           jsPDF 2.5.1 i JSZip 3.10.1 (MIT)
.nojekyll         Perquè GitHub Pages servisca els arxius tal qual
CLAUDE.md         Context per a treballar el codi amb Claude Code
```

## Sistema de disseny

Tot segueix el sistema de disseny de CGT Castelló: quatre tintes (roig #E42127, negre #111111, groc #E9E84C, blanc), Anton per a titulars i Open Sans per a la resta, sense cantonades arredonides, logo apaisat i `cgtcastello.org` al peu.

## Llicències

- Codi: a decidir pel sindicat.
- Fonts: SIL Open Font License 1.1 (`fonts/OFL-*.txt`).
- jsPDF i JSZip: MIT (`vendor/LICENSE-*`).
- Logos i il·lustracions de CGT Castelló: ús exclusiu del sindicat.
