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

#### Practica
Practica el flexbox amb el joc de les granotes: [Exercici Flexbox](https://flexboxfroggy.com/)

---

## 4. Grid: layout de dues dimensions

CSS Grid permet **organitzar els elements en una graella de files i columnes**. Imagina un full quadriculat: pots posar un element en una casella o fer que n'ocupi diverses.

Treballa en **dues dimensions** perquè pots definir les files i les columnes al mateix temps. És útil per crear una galeria amb columnes alineades o una pàgina amb capçalera, menú lateral, contingut i peu.

### 4.1. El contenidor i les caselles

* **Contenidor grid**: element pare al qual apliquem `display: grid`.
* **Elements grid** (*grid items*): fills directes que es distribueixen dins de la graella.
* **Files i columnes**: franges horitzontals i verticals, també anomenades *pistes*.
* **Cel·la**: espai on es creuen una fila i una columna.
* **Línies**: límits que separen les files i les columnes. Serveixen per indicar on comença i acaba un element.
* **Àrea**: rectangle format per una o més cel·les que pot ocupar un element.

```text
             Columna 1    Columna 2    Columna 3
           ┌────────────┬────────────┬────────────┐
Fila 1     │     A      │     B      │     C      │
           ├────────────┼────────────┼────────────┤
Fila 2     │     D      │     E      │     F      │
           └────────────┴────────────┴────────────┘
```

En aquesta graella hi ha tres columnes, dues files i sis cel·les. Les dues files comparteixen les mateixes columnes: per això els elements queden alineats verticalment.

### 4.2. Primer exemple: una galeria de tres columnes

```html
<div class="galeria">
  <article class="targeta">Projecte A</article>
  <article class="targeta">Projecte B</article>
  <article class="targeta">Projecte C</article>
  <article class="targeta">Projecte D</article>
  <article class="targeta">Projecte E</article>
  <article class="targeta">Projecte F</article>
</div>
```

```css
.galeria {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 1rem;
}

.targeta {
  padding: 1rem;
  background: #e8eef8;
  border: 1px solid #9aacc8;
  overflow-wrap: anywhere;
}
```

**Què fa el navegador?**

1. Converteix `.galeria` en un contenidor grid.
2. Crea tres columnes iguals amb `grid-template-columns`.
3. Col·loca els fills per ordre: A, B i C a la primera fila; D, E i F a la segona, en una pàgina amb escriptura d'esquerra a dreta.
4. Crea les files necessàries automàticament, perquè no les hem definit explícitament.
5. Deixa `1rem` de separació entre files i entre columnes.

`display: grid` tot sol no crea tres columnes: cal indicar la distribució que volem. Tampoc converteix els descendents interiors de cada targeta en elements d'aquesta graella; actua sobre els fills directes.

### 4.3. Com es defineixen les mides?

Amb `grid-template-columns` escrivim una mida per a cada columna. Amb `grid-template-rows` podem fer el mateix per a les files.

| Exemple | Què significa? |
| --- | --- |
| `grid-template-columns: 12rem 1fr;` | Una columna de `12rem` i una altra que aprofita l'espai restant. |
| `grid-template-columns: 1fr 2fr;` | Dues columnes flexibles amb proporció 1:2, sempre que els mínims del contingut ho permetin. |
| `grid-template-columns: repeat(3, 1fr);` | Tres columnes flexibles amb el mateix factor de repartiment. |
| `grid-template-rows: auto 1fr auto;` | Primera i última fila dimensionades segons el contingut; la central pot aprofitar l'espai disponible. |
| `gap: 1rem 2rem;` | `1rem` entre files i `2rem` entre columnes. |

La unitat **`fr`** representa una fracció de l'espai que es reparteix entre pistes flexibles. Per exemple, si queden 600 píxels després de descomptar separacions i pistes fixes, `1fr 2fr` reparteix aquest espai en 200 i 400 píxels, si els mínims del contingut no ho impedeixen.

`repeat(3, ...)` evita escriure tres vegades la mateixa definició. `minmax(mínim, màxim)` estableix els límits d'una pista: **`minmax(0, 1fr)`** permet que la columna es redueixi fins a zero i participi en el repartiment de l'espai. Així, un contingut llarg no força per si sol una columna a ser més ampla que les altres; el contingut encara necessita regles adequades perquè no desbordi.

!!! tip "Evita sumar percentatges i separacions sense tenir-los en compte"

    Tres columnes de `33.33%` ja ocupen pràcticament tota l'amplada. Si hi afegeixes `gap`, la graella pot desbordar. Amb `repeat(3, minmax(0, 1fr))`, Grid descompta les separacions abans de repartir l'espai entre les columnes.

### 4.4. Files explícites i files automàtiques

La **graella explícita** és la que defineixes amb `grid-template-columns` i `grid-template-rows`. Quan calen més pistes per col·locar els elements, el navegador crea la **graella implícita**.

En la galeria anterior hem definit tres columnes, però cap fila. Si afegim una setena targeta, apareix una tercera fila automàticament.

Per controlar les files creades automàticament podem afegir:

```css
.galeria {
  grid-auto-rows: minmax(8rem, auto);
}
```

Cada fila automàtica tindrà una alçada mínima de `8rem` i podrà créixer si el contingut ho necessita. Això és útil per evitar files massa baixes sense fixar una alçada que pugui tallar el text.

### 4.5. Fer que un element ocupi diverses cel·les

#### Línies, pistes i cel·les: què numeram?

Les **línies** són les fronteres de la graella, no les columnes ni les files. Una **pista** és l'espai entre dues línies consecutives. Una **cel·la** és la intersecció d'una pista de fila i una de columna.

Les línies de la graella es numeren. **Tres columnes tenen quatre línies verticals**: una a cada extrem i dues interiors.

```text
Línia 1        Línia 2        Línia 3        Línia 4
   │ Columna 1    │ Columna 2    │ Columna 3    │
```

Podem afegir la classe `destacada` a la primera targeta:

```html
<article class="targeta destacada">Projecte A</article>
```

```css
.destacada {
  grid-column: 1 / 3;
}
```

`grid-column: 1 / 3` significa que comença a la línia 1 i acaba a la línia 3: **ocupa dues columnes**, no tres. Els altres elements es col·loquen als espais disponibles seguint el comportament automàtic de Grid.

Altres opcions:

* `grid-column: span 2`: ocupa dues columnes sense fixar-ne la línia inicial.
* `grid-column: 1 / -1`: ocupa totes les columnes de la graella explícita; `-1` identifica la seva última línia.
* `grid-row: span 2`: ocupa dues files.

#### Exemple complet: situar un element amb quatre límits

**Codi HTML:**

```html
<div class="graella-linies">
  <article class="bloc-a">A</article>
  <article class="bloc-b">B</article>
  <article class="bloc-c">C</article>
</div>
```

**Codi CSS:**

```css
.graella-linies {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  grid-template-rows: repeat(2, minmax(6rem, auto));
  gap: 1rem;
}
.graella-linies > article {
  padding: 1rem;
  background: #e8eef8;
  border: 1px solid #9aacc8;
}
.bloc-a {
  grid-column: 1 / 3;
  grid-row: 1 / 3;
}
.bloc-b {
  grid-column: 3 / 4;
  grid-row: 1 / 2;
}
.bloc-c {
  grid-column: 3 / 4;
  grid-row: 2 / 3;
}
```

**Resultat** (esquema sense representar el `gap`):

```text
                    Línies de columna
                1           2           3           4
Línia de fila 1  ┌───────────────────────┬───────────┐
                │                       │     B     │
Línia de fila 2  │           A           ├───────────┤
                │                       │     C     │
Línia de fila 3  └───────────────────────┴───────────┘
```

**Per què passa?**

1. El contenidor defineix tres columnes i dues files: hi ha **quatre línies de columna i tres línies de fila**.
2. `grid-column: 1 / 3` situa A entre les línies verticals 1 i 3: ocupa les columnes 1 i 2.
3. `grid-row: 1 / 3` situa A entre les línies horitzontals 1 i 3: ocupa les dues files. La seva àrea és un rectangle de quatre cel·les.
4. B i C comparteixen els límits de columna `3 / 4`, però tenen límits de fila diferents. Per això queden un damunt de l'altre.
5. `gap` separa pistes, però **no afegeix números de línia**. A s'estén també per l'espai de les separacions interiors de l'àrea que ocupa.

La notació sempre és **inici / final**. Aquestes declaracions són equivalents:

```css
.bloc-a {
  grid-column-start: 1;
  grid-column-end: 3;
  grid-row-start: 1;
  grid-row-end: 3;
}
```

També podem escriure tota la posició amb una sola propietat:

```css
.bloc-a {
  grid-area: 1 / 1 / 3 / 3;
  /* fila inicial / columna inicial / fila final / columna final */
}
```

Aquí `grid-area` utilitza **quatre límits**, no un nom d'àrea. El resultat és el mateix que amb les dues propietats anteriors.

#### Comptar des del final i utilitzar `span`

En aquests apunts, amb escriptura horitzontal d'esquerra a dreta, les línies de columna positives es compten des de l'esquerra i les de fila des de dalt. Els números negatius es compten des del final de la **graella explícita**:

```text
Línies positives:     1       2       3       4
Línies negatives:   -4      -3      -2      -1
                     │       │       │       │
                     columna columna columna
                        1       2       3
```

| Declaració | Resultat en aquesta graella de tres columnes |
| --- | --- |
| `grid-column: 1 / -1` | Ocupa les tres columnes explícites. |
| `grid-column: 2 / -1` | Ocupa les columnes 2 i 3. |
| `grid-column: 1 / span 2` | Comença a la línia 1 i ocupa dues columnes; equival a `1 / 3`. |
| `grid-column: span 2` | Ocupa dues columnes i deixa que la col·locació automàtica decideixi on comença. |

**Per què passa?** Un número identifica una línia; `span 2` indica quantes pistes volem ocupar. No existeix la línia `0`. `-1` no es desplaça fins al final de les pistes implícites que es puguin crear després.

#### Donar noms a les línies

Els números es poden substituir per noms declarats entre claudàtors:

```css
.graella-linies {
  grid-template-columns:
    [inici] minmax(0, 1fr)
    [centre] minmax(0, 1fr)
    [lateral] minmax(0, 1fr) [final];
}
.bloc-a { grid-column: inici / lateral; }
.bloc-b { grid-column: lateral / final; }
.bloc-c { grid-column: lateral / final; }
```

**Resultat:** si substituïm la definició de columnes i les posicions horitzontals de l'exemple anterior per aquestes regles, obtenim la mateixa distribució.

**Per què passa?** `[inici]`, `[centre]`, `[lateral]` i `[final]` anomenen les quatre línies; no creen columnes addicionals. Les mides entre els noms continuen definint les tres pistes. Un **nom de línia** identifica una frontera; un **nom d'àrea** identifica una zona rectangular.

### 4.6. Organitzar una pàgina amb àrees

Quan la pàgina té zones clares, podem donar-los noms amb `grid-template-areas`. Això permet dibuixar-ne la distribució amb text dins del CSS.

```html
<div class="pagina">
  <header class="capcalera">Capçalera</header>
  <nav class="menu" aria-label="Principal">Menú de navegació</nav>
  <main class="contingut">Contingut principal</main>
  <footer class="peu">Peu de pàgina</footer>
</div>
```

```css
.pagina {
  display: grid;
  grid-template-columns: minmax(0, 1fr);
  grid-template-areas:
    "capcalera"
    "menu"
    "contingut"
    "peu";
  gap: 1rem;
}

.capcalera { grid-area: capcalera; }
.menu { grid-area: menu; }
.contingut { grid-area: contingut; }
.peu { grid-area: peu; }

@media (min-width: 48rem) {
  .pagina {
    grid-template-columns: 12rem minmax(0, 1fr);
    grid-template-areas:
      "capcalera capcalera"
      "menu      contingut"
      "peu       peu";
  }
}
```

En una pantalla petita, totes les zones apareixen en una columna. A partir de `48rem`, el menú ocupa la columna lateral i el contingut ocupa la resta. La capçalera i el peu s'estenen per les dues columnes perquè repetim el seu nom a les dues posicions de la fila.

Cada cadena entre cometes representa una fila. Totes han de tenir el mateix nombre de cel·les, i les cel·les d'una mateixa àrea han de formar un rectangle. Un punt (`.`) representa una cel·la sense àrea assignada.

#### Resultat visual i lectura del codi

```text
Pantalla petita              A partir de 48rem
┌─────────────────┐          ┌─────────────┬──────────────────┐
│    capcalera    │          │           capcalera            │
├─────────────────┤          ├─────────────┼──────────────────┤
│      menu       │          │    menu     │    contingut     │
├─────────────────┤          ├─────────────┴──────────────────┤
│    contingut    │          │              peu               │
├─────────────────┤          └────────────────────────────────┘
│       peu       │
└─────────────────┘
```

**Per què passa?**

1. `grid-template-columns` defineix les **amplades**. `grid-template-areas` defineix el **mapa de zones**, no les seves amplades.
2. A la versió ampla, cada cadena té dos noms perquè hi ha dues columnes. Les tres cadenes defineixen tres files.
3. Repetir `capcalera` a dues cel·les contigües crea **una única àrea** que les abasta. No duplica l'element HTML.
4. `.capcalera { grid-area: capcalera; }` assigna aquell element a l'àrea. El nom de classe i el nom d'àrea no es vinculen automàticament: cal aquesta declaració.
5. La consulta de mitjans canvia el mapa i les columnes; les assignacions dels fills continuen sent les mateixes.

En la versió ampla, l'àrea `capcalera` va de la línia de columna **1 a la 3** i de la línia de fila **1 a la 2**. Per tant, línies i àrees descriuen la mateixa graella de dues maneres diferents.

#### Exemple: una àrea de dues files i una cel·la buida

Amb el mateix HTML, podem substituir el mapa de la versió ampla per:

```css
@media (min-width: 48rem) {
  .pagina {
    grid-template-areas:
      "capcalera capcalera"
      "menu      contingut"
      "menu      ."
      "peu       peu";
  }
}
```

**Resultat:** el menú ocupa dues files. El contingut ocupa la cel·la superior de la dreta, i la inferior no té cap àrea assignada. El peu ocupa tota la darrera fila.

**Per què passa?** Les dues aparicions verticals de `menu` formen un rectangle d'una columna i dues files. El punt deixa una cel·la sense nom: no crea un element invisible ni impedeix que la col·locació automàtica hi situï un fill addicional. La fila amb el punt no té una alçada mínima fixada, de manera que l'espai buit visible dependrà del dimensionament de les files i del contingut.

#### Exemple incorrecte: una àrea en forma de L

```css
/* Incorrecte: la zona anomenada menu no forma un rectangle. */
.pagina {
  grid-template-areas:
    "menu menu"
    "menu contingut";
}
```

**Resultat:** el navegador descarta aquesta declaració de `grid-template-areas` perquè és invàlida.

**Per què passa?** Un mateix nom ha d'ocupar un rectangle complet, sense forats ni formes de L. També seria invàlid escriure files amb nombres diferents de cel·les. Si hi ha una altra declaració vàlida aplicable, la cascada determinarà quin mapa s'utilitza.

### 4.7. Una galeria que adapta el nombre de columnes

En lloc de fixar sempre tres columnes, podem deixar que Grid calculi quantes hi caben. Per provar-ho, substitueix la definició de columnes del primer exemple:

```css
.galeria {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 15rem), 1fr));
  gap: 1rem;
}
```

Llegeix l'expressió de dins cap enfora:

1. `min(100%, 15rem)` tria el valor més petit entre l'amplada del contenidor i `15rem`. Així, el mínim de la columna no supera el contenidor en pantalles molt estretes.
2. `minmax(..., 1fr)` defineix aquest mínim i permet que la columna creixi amb l'espai disponible.
3. `repeat(auto-fit, ...)` crea les columnes que hi caben i col·lapsa les que queden buides, perquè les ocupades puguin aprofitar l'espai.

El resultat passa d'una columna a diverses segons l'amplada disponible, sense haver de definir una consulta de mitjans per a cada nombre de columnes.

### 4.8. Alinear el contingut dins de la graella

En una pàgina amb escriptura horitzontal, aquestes propietats del contenidor controlen els elements dins de les seves àrees:

| Propietat | Efecte |
| --- | --- |
| `justify-items: center` | Centra cada element horitzontalment dins de la seva àrea. |
| `align-items: center` | Centra cada element verticalment dins de la seva àrea. |
| `place-items: center` | Combina els dos centraments anteriors. |

Molts elements s'estiren per defecte per omplir la seva àrea. Si els centres, poden deixar d'ocupar-ne tota l'amplada o alçada. Per canviar només un fill, utilitza `justify-self` o `align-self`.

`justify-content` i `align-content` tenen una altra funció: distribueixen **el conjunt de les pistes** dins del contenidor quan hi ha espai lliure. Per exemple, unes columnes d'amplada fixa es poden centrar amb `justify-content: center` si no ocupen tota l'amplada.

### 4.9. Errors habituals

* **Aplicar Grid al fill en lloc del pare:** el contenidor és qui organitza els seus fills directes.
* **Confondre números de columna amb números de línia:** `1 / 3` ocupa dues columnes.
* **Fixar alçades massa petites:** deixa que les files creixin amb el contingut o utilitza un mínim amb `minmax`.
* **Crear columnes fora de les previstes:** col·locar un element més enllà de la graella definida pot generar pistes implícites inesperades.
* **Forçar elements massa amples:** revisa els mínims de les columnes i adapta imatges i textos perquè no desbordin.
* **Canviar l'ordre visual sense revisar l'HTML:** moure un element amb Grid no canvia l'ordre de lectura del document ni, habitualment, el recorregut del teclat. Mantén un ordre HTML coherent.

### 4.10. Quan usar Grid i què practicar

Utilitza Grid per a galeries de targetes, panells d'informació i pàgines amb diverses zones que necessiten compartir files i columnes. Pots utilitzar Flexbox dins d'una targeta per alinear-ne els botons.

**Pràctica guiada:**

1. Copia l'exemple de la galeria i canvia les tres columnes per dues.
2. Afegeix una setena targeta i observa com es crea una fila nova.
3. Fes que la primera targeta ocupi dues columnes amb `grid-column: span 2`.
4. Retira aquesta regla i prova les columnes automàtiques de l'apartat 4.7 mentre canvies l'amplada de la finestra.
5. Copia l'exemple d'àrees i comprova com canvia la posició del menú en una pantalla ampla.
6. Activa la visualització de la graella a les eines de desenvolupador del navegador per identificar les línies, les pistes i les separacions.

Veure demo: [Grid](demos/3_exemples_layout.html#grid)

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
