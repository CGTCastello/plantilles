# CLAUDE.md — Editor de plantilles de CGT Castelló

Context per a qualsevol sessió de Claude Code que treballe en aquest repositori.

## Què és

Una web estàtica (GitHub Pages) perquè la gent de CGT Castelló faça cartells i imatges per a xarxes amb el sistema de disseny del sindicat, sense saber disseny. Tot es dibuixa en un `<canvas>` al navegador; no hi ha servidor ni pas de compilació.

- Interfície en **valencià**. Les peces poden eixir en valencià, en castellano o en totes dues (primer valencià).
- Públic: afiliades sense coneixements tècnics, majoritàriament des del **mòbil** (iPhone i Android).

## Estructura del codi (`index.html`)

Tot el JS és dins d'una IIFE al final d'`index.html`. Les parts principals són aquestes:

- `LOGO_BODY`, `TRI`, `logoSVG(v)`: el logo apaisat en SVG. Només canvia el triangle: `color`, `negre` (transparent), `trama`, `morat`, `verd`, `orgull`, `trans`. «CGT» porta vora negra en `trama` i `trans`.
- `TPL`: definició de cada plantilla, amb els camps visibles i els textos per defecte en `va` i `es`. `TPL_ORDER` en fixa l'ordre a la interfície.
- `FMT`: formats. L'amplada lògica és sempre `W` (1080, o 1024/1200 en web/og). `px` és l'amplada real a l'exportar i `T` és el marge de seguretat del story (250 px dalt i baix).
- `RENDER.<plantilla>(tx, warn)`: dibuixa cada plantilla. Fan servir `R` (context de la peça: diapositiva, idioma, mides, paleta `P`) i helpers com `fit()` (ajusta la mida del titular), `drawLines()`, `drawBoxed()`, `etiqueta()`, `kicker()`, `peu()`, `peuBand()`, `noteAt()` (requadre de text) i `drawPhoto()` (enquadrament + difuminat de cares).
- `palette(bn)`: paleta normal o de fotocòpia (blanc i negre).
- `paint(target, scale, idx, lang, preview)`: pinta una diapositiva en qualsevol canvas a qualsevol escala. La previsualització és escala 1; l'exportació, `FMT.px / W`.
- `buildFile()`: PNG/JPG, ZIP (JSZip) o PDF (jsPDF), segons el nombre de diapositives i d'idiomes.
- Baixades: dins de Claude (artifact) s'usa `window.claude.use('downloads')`; fora (GitHub Pages) s'usa un `<a download>` normal. Cal mantenir els dos camins.
- Enllaços: `#plantilla-format` (p. ex. `#conv-a4`) i, només fora de Claude, paràmetres `?t=&e=&k=&x=&c=&dia=&hora=&lloc=&f=&n=` (sufix `_es` per al castellano), més `lang=es|both`, `logo=` i `bn=1`.

## Regles del sistema de disseny (no les trenques)

Font de veritat: «CGT Castelló · Sistema de disseny» (artifact `claude.ai/artifact/PZJLDkCv3ANyjQrGEm9PLA`, començant per `project/README.md`).

- **Quatre tintes**: roig `#E42127`, negre `#111111`, groc `#E9E84C`, blanc. Grisos de suport: `#BDBDBD` (meta sobre negre) i `#333333` (filets sobre negre). Cap altre color, llevat del triangle dels logos temàtics.
- **Dues famílies**: Anton (titulars, etiquetes, xifres i peu, sempre en majúscules) i Open Sans 400/700/800. Sense cursives.
- Marge de 60 px sobre 1080. El peu va a 48 px de la vora: filet de 4 px, `cgtcastello.org` i el logo apaisat de 92–118 px d'alt (ara, 96).
- Sense cantonades arredonides, sense ombres i sense degradats (excepte el de la foto cap al roig a la convocatòria).
- El groc és només per a etiquetes: una o dues per peça, mai com a fons.
- Logo: color sobre fons clar; negre (triangle transparent) sobre roig; sobre negre o foto, banda blanca al peu; trama en B/N.
- Titulars de quatre línies com a màxim. Les dades sempre amb font.
- Fotos reals i **cares difuminades** sempre.

## Treballar-hi

- Provar en local: `python3 -m http.server 8000` i obrir `http://localhost:8000`.
- No afegeixis dependències de CDN: tot ha de funcionar des del repositori (fonts en `fonts/`, llibreries en `vendor/`).
- Límit dels iPhone: canvas de 16,7 Mpx com a màxim. Per això l'A3 s'exporta a 2900 px d'ample.
- Abans de pujar un canvi, revisa cada plantilla en post, story i A4, en valencià i en castellano, amb foto i sense, i en B/N.

## Idees pendents

- Detecció automàtica de cares al navegador (mantenint el toc manual com a reserva).
- Marques de tall i sagnat al PDF per a impremta.
- Logo «orgull intersex-inclusiu» (té un chevron i un triangle groc amb cercle morat: cal agafar l'SVG del sistema de disseny).
- Textures «fotocòpia» i «trama + gra» del llenç «estil 11N».
