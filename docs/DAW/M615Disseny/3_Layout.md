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

Flexbox és un sistema de CSS que permet **distribuir, alinear i ajustar la mida d'un grup d'elements dins d'un contenidor**. És útil, per exemple, per posar els enllaços d'un menú en fila, separar uns botons o centrar una icona al costat d'un text.

Es diu que treballa en **una dimensió** perquè organitza els elements seguint una direcció principal: una fila o una columna.

### 3.1. El contenidor i els elements flex

Imagina una caixa amb tres botons dins. La caixa és el **contenidor flex** i els botons són els **elements flex** (*flex items*).

```html
<div class="accions">
  <button type="button">Desa</button>
  <button type="button">Previsualitza</button>
  <button type="button">Cancel·la</button>
</div>
```

```css
.accions {
  display: flex;
  gap: 1rem;
}
```

Amb `display: flex`, els **fills directes** de `.accions` es distribueixen amb Flexbox. Per defecte, es col·loquen en fila i intenten mantenir-se en una sola línia. `gap: 1rem` deixa una separació entre els botons.

Si un botó conté una icona i un text, aquests elements interiors no es converteixen automàticament en elements flex: caldria aplicar també `display: flex` al botó per organitzar-ne el contingut amb Flexbox.

### 3.2. Entendre els dos eixos

Flexbox utilitza dos eixos per decidir on col·loca els elements:

* **Eix principal** (*main axis*): direcció en què es distribueixen els elements. Es defineix amb `flex-direction`.
* **Eix transversal** (*cross axis*): direcció perpendicular a l'eix principal.

En una pàgina amb escriptura horitzontal d'esquerra a dreta, com aquests apunts:

| Propietat | Distribució | Eix principal | Eix transversal |
| --- | --- | --- | --- |
| `flex-direction: row` | Elements en fila, d'esquerra a dreta | Horitzontal → | Vertical ↓ |
| `flex-direction: column` | Elements en columna, de dalt a baix | Vertical ↓ | Horitzontal → |

```text
row:       [Desa]  [Previsualitza]  [Cancel·la]

column:    [Desa]
           [Previsualitza]
           [Cancel·la]
```

!!! tip "Pensa en els eixos abans d'alinear"

    `justify-content` distribueix els elements en l'eix principal i `align-items` els alinea en l'eix transversal. Amb `row`, `justify-content` actua horitzontalment; amb `column`, actua verticalment.

### 3.3. Propietats que apliquem al contenidor

| Propietat | Per a què serveix? | Exemple |
| --- | --- | --- |
| `display` | Activa Flexbox per als fills directes. | `display: flex;` |
| `flex-direction` | Tria la direcció principal. | `flex-direction: column;` |
| `justify-content` | Distribueix l'espai lliure en l'eix principal. | `justify-content: space-between;` |
| `align-items` | Alinea els elements en l'eix transversal de la seva línia. | `align-items: center;` |
| `gap` | Estableix la separació entre elements i, si n'hi ha, entre línies. | `gap: 1rem;` |
| `flex-wrap` | Permet passar a una altra línia quan no hi ha prou espai. | `flex-wrap: wrap;` |

Valors habituals de `justify-content`:

* `flex-start`: agrupa els elements al principi de l'eix principal; és el comportament habitual per defecte.
* `center`: agrupa els elements al centre.
* `flex-end`: agrupa els elements al final.
* `space-between`: amb dos o més elements, situa el primer al principi i l'últim al final, i reparteix l'espai lliure entre ells.

Valors habituals de `align-items`:

* `stretch`: és el comportament habitual per defecte; estira els elements per ocupar la mida transversal de la línia si no tenen una mida fixada en aquell eix.
* `center`: centra els elements en l'eix transversal.
* `flex-start` i `flex-end`: els alineen al principi o al final de l'eix transversal.

### 3.4. Exemple: una barra amb el títol i els botons

```html
<header class="barra">
  <h2>El meu projecte</h2>
  <div class="accions">
    <button type="button">Desa</button>
    <button type="button">Cancel·la</button>
  </div>
</header>
```

```css
.barra {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  flex-wrap: wrap;
  padding: 1rem;
}

.barra h2 {
  margin: 0;
}

.accions {
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
}
```

**Què passa en aquest exemple?**

1. `.barra` té dos elements flex: el títol i el grup de botons.
2. Si caben a la mateixa línia i sobra espai, `space-between` separa el títol cap a l'esquerra i el grup cap a la dreta.
3. `align-items: center` els centra verticalment dins de la línia, encara que tinguin alçades diferents.
4. `gap` manté una separació entre ells.
5. Si no caben en una línia, `flex-wrap: wrap` permet que el grup de botons passi a sota.
6. `.accions` és un segon contenidor flex que organitza els botons del seu interior.

### 3.5. Propietats que apliquem als elements fills

El contenidor defineix la distribució general, però cada fill també pot indicar com s'ajusta a l'espai disponible:

| Propietat | Què controla? |
| --- | --- |
| `flex-grow` | El factor amb què l'element participa en el repartiment de l'espai sobrant. Amb `0`, no creix per aquest motiu. |
| `flex-shrink` | El factor de reducció quan falta espai, tenint en compte la mida base i els límits de cada element. Amb `0`, no s'encongeix per aquest motiu. |
| `flex-basis` | La mida base en l'eix principal abans de repartir o reduir espai. |
| `align-self` | Permet donar a un fill una alineació transversal diferent de la indicada per `align-items`. |


!!! tip "Diverses files no converteixen Flexbox en Grid"

    Amb `flex-wrap: wrap`, cada línia reparteix el seu espai de manera independent. Per això, les targetes de l'última fila poden tenir amplades diferents de les de la fila anterior. Si necessites columnes alineades entre totes les files, Grid acostuma a encaixar millor.

### 3.6. Errors habituals i com entendre'ls

* **Posar `display: flex` al fill que vols moure:** aplica'l al pare que ha d'organitzar aquell fill i els seus germans.
* **No veure cap canvi amb `justify-content: center`:** comprova si hi ha espai lliure en l'eix principal. Si els fills ja l'ocupen tot, no queda espai per desplaçar-los.
* **Intentar centrar verticalment una columna sense espai disponible:** amb `flex-direction: column`, el contenidor necessita una alçada amb espai sobrant perquè `justify-content: center` tingui un efecte visible.
* **Esperar un salt de línia automàtic:** el valor inicial és `nowrap`; activa `flex-wrap: wrap` si vols permetre diverses línies.
* **Tenir un text llarg que desborda:** els elements flex tenen límits mínims de mida. Segons el cas, pot caldre `min-width: 0` al fill i una regla com `overflow-wrap: anywhere` per permetre partir una cadena llarga.

### 3.7. Quan usar Flexbox i què practicar

Utilitza'l per a menús, barres d'accions, grups de botons, icones amb text i altres grups organitzats principalment en una fila o columna.

**Pràctica:** copia l'exemple de la barra i prova aquests canvis d'un en un:

1. Canvia `space-between` per `center` i observa on queda l'espai lliure.
2. Canvia `row` per `column` i identifica de nou els dos eixos.
3. Amb `column`, canvia `align-items: center` per `flex-start`.
4. Torna a `row`, estreny la finestra i compara el resultat amb `wrap` i amb `nowrap`.

Veure demo: [Flexbox](demos/3_exemples_layout.html#flexbox)

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

## Recursos oficials de consulta

* **MDN - Normal flow**
	* https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Normal_Flow
* **MDN - Basic concepts of Flexbox**
	* https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_flexible_box_layout/Basic_concepts_of_flexbox
* **MDN - Basic concepts of Grid**
	* https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout/Basic_concepts_of_grid_layout
* **MDN - Responsive design**
	* https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design
* **web.dev - Responsive Web Design Basics**
	* https://web.dev/articles/responsive-web-design-basics

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
