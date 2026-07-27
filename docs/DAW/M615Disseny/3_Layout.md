# Bloc 3: Layout web (flux, Flexbox, Grid, responsive)

Aquest bloc ensenya a construir maquetacions modernes i estables. L'objectiu és entendre com es distribueixen els elements en pantalla i prendre decisions de layout amb criteri.

---

## 1. Objectiu del bloc

En acabar aquest bloc, l'alumnat ha de poder:

1. Explicar el **flux normal** del document.
2. Fer layouts d'una dimensió amb **Flexbox**.
3. Fer layouts de dues dimensions amb **Grid**.
4. Adaptar la maquetació amb estratègia **responsive**.

Idea clau: primer entén el flux, després decideix si Flexbox o Grid resol millor cada problema.

---

## 2. Flux normal del document

Per defecte, els elements HTML segueixen el flux natural del navegador:

* Els elements de bloc ocupen tota l'amplada disponible i baixen a una línia nova.
* Els elements en línia ocupen només l'espai del contingut.
* L'ordre del codi marca l'ordre visual i de lectura.

### Per què és important

Abans d'aplicar cap layout avançat, cal comprovar si el flux normal ja resol gran part de l'estructura.

---

## 3. Flexbox: layout d'una dimensió

Flexbox és ideal per distribuir elements en una fila o en una columna.

### Conceptes essencials

* **Contenidor flex**: element pare amb `display: flex;`
* **Main axis**: eix principal (row o column).
* **Cross axis**: eix transversal.
* **Items flex**: fills directes del contenidor.

### Propietats clau

* `display: flex;`
* `flex-direction: row | column;`
* `justify-content: ...`
* `align-items: ...`
* `gap: ...`
* `flex-wrap: wrap;`

### Exemple bàsic

Veure demo: [Flexbox](demos/3_exemples_layout.html#flexbox)

### Quan usar Flexbox

* menús
* barres d'accions
* grups de botons
* alineació ràpida d'elements en una sola direcció

---

## 4. Grid: layout de dues dimensions

Grid és ideal quan necessites controlar files i columnes al mateix temps.

### Conceptes essencials

* **Contenidor grid**: element pare amb `display: grid;`
* **Columnes**: `grid-template-columns`
* **Files**: `grid-template-rows`
* **Separació**: `gap`

### Exemple bàsic

Veure demo: [Grid](demos/3_exemples_layout.html#grid)

### Quan usar Grid

* galeries de targetes
* maquetació de pàgines
* dashboards
* estructures amb múltiples zones

---

## 5. Flexbox vs Grid: decisió ràpida

Regla pràctica:

* Si el problema és **una dimensió** (fila o columna), comença amb **Flexbox**.
* Si el problema és **dues dimensions** (files i columnes), usa **Grid**.

No són rivals: es combinen sovint en el mateix projecte.

---

## 6. Responsive: adaptar el layout

Una maquetació moderna ha de funcionar en mòbil, tauleta i escriptori.

### Principis bàsics

* **Mobile first**: defineix primer la versió petita.
* **Escalat progressiu**: afegeix canvis quan l'espai creix.
* **Lectura i interacció**: text llegible i botons usables.

### Meta viewport

Veure demo: [Responsive amb viewport](demos/3_exemples_layout.html#responsive-grid)

### Exemple responsive amb Grid

Veure demo: [Grid responsive](demos/3_exemples_layout.html#responsive-grid)

---

## 7. Errors habituals de layout

* Forçar distribucions complexes amb només marges manuals.
* No definir `gap` i acabar amb espais inconsistents.
* Usar Grid per coses que Flexbox resol de forma més simple.
* No provar la maquetació en pantalles menudes.
* Centrar-ho tot per defecte sense criteri d'estructura.

---

## 8. Checklist de revisió

Abans de tancar una pantalla:

* El flux normal està respectat i té sentit.
* S'ha triat Flexbox o Grid amb un criteri clar.
* Hi ha separació coherent entre elements (`gap`, marges).
* El layout es manté usable en mòbil.
* No hi ha scroll horitzontal innecessari.

---

## 9. El 20% que han de recordar sempre

1. El flux normal és la base de tota maquetació.
2. Flexbox resol una dimensió; Grid resol dues dimensions.
3. `gap` és millor que espais improvisats amb marges a tot arreu.
4. Mobile first simplifica decisions responsive.
5. El millor layout no és el més complex, és el més clar i mantenible.

---

## Resum del bloc

Quan l'alumnat domina flux, Flexbox, Grid i responsive, pot construir layouts moderns amb criteri professional. Aquesta base permet passar després a Bootstrap o Tailwind sense dependre de receptes memoritzades.