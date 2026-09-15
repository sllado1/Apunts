# Bloc 3: Pla de desenvolupament

## Objectiu del bloc

Aprendre a redactar un document que expliqui què volem construir, com ho desenvolupem i què necessita una altra persona per instal·lar, executar i desplegar el projecte.

El pla és un **document viu**: es comença abans de programar i s'actualitza a mesura que avança el treball. Al principi hi haurà funcionalitats previstes i decisions pendents; després hi afegirem les tasques acabades, les comprovacions fetes i les incidències trobades.

El podem escriure en Markdown al `README.md` del projecte. Si creix massa, podem deixar un resum al `README.md` i enllaçar la informació detallada des de `docs/`.

> **Idea clau**
> Una altra persona ha de poder entendre el projecte i posar-lo en marxa seguint la documentació.

Els exemples dels apartats següents corresponen a un projecte fictici: un reproductor web de cançons amb HTML, CSS i JavaScript.

---

## 1. Nom i descripció del projecte

### Què cal explicar?

Indica el nom del projecte i descriu, en poques frases, què és, a qui s'adreça i quina necessitat resol. El nom identifica el projecte; la descripció permet entendre'n la finalitat sense haver d'obrir el codi.

### Per què és important?

Situa ràpidament la persona que llegeix el document i ajuda l'equip a compartir una mateixa idea de l'aplicació que està construint.

### Exemple

**Nom:** AulaMusic.

**Descripció:** reproductor web perquè l'alumnat pugui escoltar una selecció de cançons de pràctica des del navegador. Permet consultar la llista i controlar la reproducció sense crear un compte.

---

## 2. Objectius i funcionalitats principals

### Què cal explicar?

Diferencia entre l'**objectiu**, que expressa què vols aconseguir, i les **funcionalitats**, que són les accions concretes que permetrà fer l'aplicació.

Prioritza les funcionalitats i defineix l'**MVP**, la primera versió mínima que ja resol la necessitat principal. Indica també què queda fora de l'abast i les condicions de qualitat que cal complir, com ara poder utilitzar els controls amb el teclat.

### Per què és important?

Permet decidir què s'ha de construir primer i evita afegir millores sense acabar les parts essencials. També dona una base per comprovar si el resultat compleix el que s'havia acordat.

### Exemple

**Objectiu:** facilitar l'escolta de cançons amb una interfície senzilla.

| Prioritat | Funcionalitat prevista | Com comprovarem que funciona? |
| --- | --- | --- |
| MVP | Reproduir i pausar una cançó | El botó inicia i pausa l'àudio i reflecteix l'estat actual. |
| MVP | Mostrar el títol de la cançó | El títol visible correspon a l'àudio carregat. |
| Segona fase | Seleccionar una cançó de la llista | La selecció actualitza l'àudio i el títol. |
| Segona fase | Passar a la cançó següent i anterior | Els controls canvien de cançó segons l'ordre definit. |

En aquesta versió queden fora de l'abast els comptes d'usuari i la pujada de cançons. La interfície ha de ser usable en mòbil i els botons han de tenir etiquetes comprensibles.

---

## 3. Tasques implementades

### Què cal explicar?

Registra les accions concretes que s'han completat: crear un fitxer, programar un control, corregir un error o verificar un comportament. Per a cada tasca, indica el resultat i com s'ha comprovat. Pots afegir-hi la data, la persona responsable i una referència al commit o a la petició d'integració de canvis (*pull request*).

Abans de començar, escriu que encara no hi ha tasques implementades. Mantén les tasques pendents identificades amb el seu ordre de treball i les dependències: per exemple, cal carregar un àudio abans de provar el botó de reproducció.

### Per què és important?

Fa visible el treball realitzat i permet reprendre'l sense haver de recordar cada canvi. També ajuda a repartir la feina i a revisar què s'ha validat.

### Exemple

| Tasca implementada | Resultat | Comprovació feta |
| --- | --- | --- |
| Crear `public/index.html` | Pàgina amb títol i controls | La pàgina es carrega des del servidor local. |
| Connectar el botó de reproducció amb l'element `<audio>` | Reproducció i pausa d'una cançó | S'ha provat iniciar, pausar i reprendre l'àudio. |
| Afegir estils adaptables | Controls visibles en una pantalla estreta | S'ha revisat que no aparegui desplaçament horitzontal. |

**Tasques següents:** definir la llista de cançons, mostrar-la a la pàgina i implementar-ne la selecció, en aquest ordre.

!!! tip "Una tasca acabada ha de tenir un resultat comprovable"

    «Treballar en el reproductor» és massa imprecís. «Implementar el botó de pausa i comprovar que atura l'àudio» explica què s'ha fet i com sabem que funciona.

---

## 4. Tecnologies i eines utilitzades

### Què cal explicar?

Enumera les tecnologies i les eines que utilitzes, la funció que tenen dins del projecte i les versions quan siguin necessàries per reproduir l'entorn. Distingeix les eines necessàries per executar l'aplicació de les que només utilitzes durant el desenvolupament.

### Per què és important?

Ajuda una altra persona a preparar l'entorn adequat i a entendre de què depèn el projecte. També permet detectar diferències entre ordinadors quan alguna cosa no funciona.

### Exemple

| Tecnologia o eina | Ús en el projecte |
| --- | --- |
| HTML | Estructura de la pàgina i element d'àudio. |
| CSS | Presentació visual i adaptació a diferents pantalles. |
| JavaScript | Controls de reproducció i selecció de cançons. |
| Git | Registre de canvis i treball amb branques. |
| VS Code | Editor utilitzat per desenvolupar; no és necessari per executar el web. |
| PHP | Llenguatge de programació utilitzat per a la part del servidor. |
| Navegadors | Versió |
| --- | --- |
| Chrome | 98.0.4758.102 |
| Firefox | 97.0 |
| Safari | 14.0.3 |

En el document real, anota els navegadors amb què has fet les proves. Si utilitzes biblioteques externes, indica'n també la versió i el motiu d'ús.

---

## 5. Estructura general del projecte

### Què cal explicar?

Mostra un arbre simplificat de carpetes i fitxers i explica la responsabilitat de cada part. No cal enumerar tots els fitxers: cal que el lector sàpiga on trobar el codi, els recursos, les proves i la documentació.

### Per què és important?

Facilita que qualsevol membre de l'equip localitzi el que necessita i afegeixi els fitxers nous al lloc adequat.

### Exemple

```text
aulamusic/
  public/
    index.php
    assets/
      css/
      js/
      audio/
  docs/
    proves.md
  .gitignore
  README.md
```

- `public/`: contingut que es publicarà al servidor web.
- `index.php`: pàgina principal del reproductor.
- `assets/css/`: fulls d'estil.
- `assets/js/`: lògica del reproductor.
- `assets/audio/`: àudios de demostració amb permís de distribució.
- `docs/`: documentació complementària, com el registre de proves.
- `README.md`: presentació del projecte i instruccions per posar-lo en marxa.

---

## 6. Requisits previs i instruccions d'instal·lació

### Què cal explicar?

Els **requisits previs** són els programes, accessos o serveis que cal tenir abans de començar. La **instal·lació** són els passos per obtenir el projecte i preparar-lo per executar-lo.

Escriu els passos en ordre i indica des de quina carpeta s'executen les ordres. Si calen dependències, variables d'entorn o una base de dades, explica com preparar-les. Si no en calen, fes-ho constar.

### Per què és important?

Evita que el projecte només funcioni a l'ordinador de qui l'ha creat. Un company ha de poder preparar-lo sense endevinar passos ni demanar fitxers que falten.

### Exemple

**Requisits previs:** Git, PHP 8 i un navegador amb suport per a l'àudio utilitzat.

**Instal·lació:**

1. Clona el repositori substituint `URL_DEL_REPOSITORI` per l'adreça real:

    ```bash
    git clone URL_DEL_REPOSITORI aulamusic
    cd aulamusic
    ```

2. Comprova que existeix `public/assets/audio/demo.mp3`, inclòs al repositori d'aquest exemple.
3. Aquest projecte no requereix instal·lar biblioteques ni configurar una base de dades.

Si el teu projecte necessita un fitxer `.env`, proporciona un `.env.example` amb valors ficticis i explica com completar-lo. Les credencials reals no s'han d'incloure al repositori.

---

## 7. Instruccions per executar el projecte

### Què cal explicar?

Indica com iniciar el projecte després d'instal·lar-lo, quina adreça cal obrir i com comprovar que funciona. Explica també com aturar-lo.

### Per què és important?

Tenir els fitxers i les dependències preparats no implica que l'aplicació estigui en marxa. Aquest apartat permet iniciar-la en cada sessió de treball i fer una primera comprovació.

### Exemple

Des de la carpeta arrel `aulamusic/`, inicia el servidor local de proves integrat de PHP:

```bash
php -S localhost:8000 -t public
```

L'opció `-S localhost:8000` inicia el servidor a l'adreça local i al port indicats. L'opció `-t public` estableix `public/` com a arrel web: el servidor serveix els fitxers d'aquesta carpeta i executa els fitxers PHP. Cal tenir PHP instal·lat i l'ordre `php` disponible al terminal; ho pots comprovar amb `php -v`.

1. Obre `http://localhost:8000` al navegador.
2. Comprova que apareixen el títol i els controls.
3. Prem el botó de reproducció i comprova que se sent l'àudio.
4. Prem el botó de pausa i comprova que s'atura.
5. Per aturar el servidor, prem `Ctrl+C` al terminal.

Aquest servidor s'utilitza per a proves locals. La publicació del projecte s'explica a l'apartat de desplegament.

---

## 8. Estratègia de branques i convencions de desenvolupament

### Què cal explicar?

Defineix com s'organitza el treball amb Git: quina branca conté la versió estable, com es creen les branques de treball i què s'ha de revisar abans d'integrar els canvis.

Acorda també les convencions de noms, format del codi i missatges de commit. Han de ser regles senzilles que l'equip pugui aplicar de manera consistent.

### Per què és important?

Redueix els conflictes, facilita la revisió i ajuda a mantenir una versió que es pugui executar mentre es desenvolupen millores.

### Exemple

- `main`: versió estable, amb els canvis revisats i provats.
- `feature/llista-cancons`: branca per desenvolupar la llista de cançons.
- `fix/ruta-audio`: branca per corregir una ruta incorrecta.
- Abans d'integrar una branca, revisar els canvis i comprovar que la reproducció i la pausa continuen funcionant. 
- Escriure noms de fitxers públics en minúscules i amb guions, com `audio-player.js`.
- Utilitzar `camelCase` per a variables i funcions JavaScript, com `currentSong`.
- Fer commits petits amb missatges concrets, com `Afegeix el control de pausa`.

---

## 9. Estat actual del projecte i funcionalitats implementades

### Què cal explicar?

Resumeix què pot fer l'aplicació ara mateix, què està en desenvolupament, què falta i quins errors o bloquejos es coneixen. Afegeix la data d'actualització i, si és possible, la versió o el commit de referència.

### Per què és important?

Permet saber què es pot demostrar, provar o lliurar. Evita confondre les funcionalitats que es volen construir amb les que ja estan disponibles.

### Exemple

**Estat a la data del lliurament:** MVP disponible, pendent d'ampliar amb la llista de cançons. En el document real, substitueix aquesta referència per una data concreta.

| Funcionalitat | Estat | Observacions |
| --- | --- | --- |
| Reproducció i pausa | Implementada i provada | Funciona amb la cançó de demostració. |
| Títol de la cançó | Implementada i provada | Mostra el títol de l'única cançó disponible. |
| Selecció des d'una llista | Pendent | Cal definir la llista i connectar-la amb el reproductor. |
| Cançó següent i anterior | Pendent | Depèn de disposar de la llista de cançons. |

**Limitació coneguda:** encara no es mostra un missatge propi quan no es pot carregar l'àudio.

**Següent pas:** implementar la llista i comprovar que seleccionar una cançó actualitza l'àudio i el títol.

!!! tip "Tasques implementades i estat actual expliquen coses diferents"

    Les tasques descriuen el treball fet, com «connectar el botó amb l'element d'àudio». L'estat actual explica què pot fer l'usuari amb el resultat, com «reproduir i pausar una cançó». El primer apartat permet seguir el treball; el segon resumeix el producte disponible.

---

## 10. Procés de desplegament

### Què cal explicar?

Descriu com es publica una versió del projecte perquè es pugui utilitzar des del servidor de destinació. Indica on es publica, quins fitxers es necessiten, si cal compilar o configurar res i com es comprova el resultat.


### Per què és important?

Un projecte pot funcionar en local i fallar al servidor per rutes, fitxers absents o diferències de configuració. Un procediment escrit permet repetir la publicació i detectar aquests problemes.

### Exemple

**Destinació prevista:** servidor de l'aula que serveix fitxers estàtics. Procediment pendent de validar en aquest exemple.

1. Seleccionar un commit de `main` revisat i provat, i anotar-ne l'identificador.
2. Comprovar que les rutes dels àudios i els altres recursos coincideixen amb els noms reals, incloses les majúscules i minúscules.
3. Conservar una còpia de la versió publicada anteriorment.
4. Copiar el contingut de `public/` al directori web assignat, mitjançant el sistema de transferència autoritzat a l'aula. Aquest projecte no necessita compilació.
5. Obrir l'adreça pública i comprovar que es carreguen els estils, el JavaScript i l'àudio, i que els controls funcionen.
6. Registrar la data, el commit publicat i el resultat de les comprovacions.
7. Si la versió falla, restaurar la còpia anterior i tornar a comprovar el servei.

En el projecte real, concreta l'adreça pública, el directori de destinació i les ordres o els passos de transferència, sense incloure contrasenyes.

---

## 11. Decisions tècniques rellevants i incidències destacades

### Què cal explicar?

Registra les decisions que condicionen el projecte: quin problema resolen, quines alternatives s'han valorat, per què s'ha triat una opció i quines conseqüències té.

Per a les incidències, descriu el símptoma, la causa identificada, la solució i la comprovació posterior. Si encara no coneixes la causa o no has resolt el problema, indica-ho explícitament.

### Per què és important?

Ajuda a entendre el perquè del codi i evita repetir investigacions o errors. També facilita valorar si una decisió continua sent adequada quan canvien els requisits.

### Exemple de decisió tècnica

- **Necessitat:** controlar la reproducció d'àudio al navegador.
- **Opcions valorades:** utilitzar l'element HTML `<audio>` o incorporar una biblioteca externa.
- **Decisió:** utilitzar `<audio>` i controls propis amb JavaScript.
- **Motiu:** cobreix les funcionalitats previstes sense afegir una dependència.
- **Conseqüència:** cal programar i provar la sincronització entre l'àudio i l'estat dels botons.

### Exemple d'incidència resolta

- **Símptoma:** després de publicar, no es carrega la cançó.
- **Causa:** el codi demana `Demo.mp3`, però el fitxer es diu `demo.mp3`; el servidor distingeix majúscules i minúscules.
- **Solució:** corregir la ruta perquè coincideixi amb el nom del fitxer.
- **Comprovació:** publicar la correcció i verificar que l'àudio es carrega i es reprodueix.
- **Prevenció:** mantenir els noms dels àudios en minúscules i revisar les rutes abans de desplegar.

---

## Plantilla per al document del projecte

Copia aquesta estructura al `README.md` o al document del pla i completa-la amb dades del teu projecte:

```markdown
# Nom del projecte

Descripció breu: què és, a qui s'adreça i quina necessitat resol.

## 1. Objectius i funcionalitats principals
Objectiu, funcionalitats prioritzades, MVP i criteris d'acceptació.

## 2. Tasques implementades
Treball completat i comprovacions fetes. Tasques següents ordenades.

## 3. Tecnologies i eines utilitzades
Tecnologies, funció de cadascuna i versions utilitzades.

## 4. Estructura general del projecte
Arbre de carpetes i explicació de les parts principals.

## 5. Requisits previs i instruccions d'instal·lació
Entorn necessari i passos per preparar el projecte.

## 6. Instruccions per executar el projecte
Ordres, carpeta de treball, adreça local i comprovació inicial.

## 7. Estratègia de branques i convencions de desenvolupament
Branques, revisió de canvis, noms, format i missatges de commit.

## 8. Estat actual del projecte i funcionalitats implementades
Data, funcionalitats disponibles, pendents, limitacions i següent pas.

## 9. Procés de desplegament
Destinació, passos de publicació, verificació i retorn a la versió anterior.

## 10. Decisions tècniques rellevants i incidències destacades
Decisions justificades i problemes amb la seva solució o estat pendent.
``
## Checklist de revisió

- El nom i la descripció permeten entendre la finalitat del projecte.
- Els objectius, les prioritats i l'MVP estan definits.
- Les tasques acabades inclouen una comprovació del resultat.
- Les tecnologies i les versions necessàries estan identificades.
- L'estructura explica on es troba cada part del projecte.
- Un company pot instal·lar i executar el projecte seguint les instruccions.
- Les regles de treball amb branques i de format del codi són clares.
- L'estat actual diferencia les funcionalitats disponibles de les pendents.
- El desplegament està documentat i s'indica si s'ha validat.
- Les decisions i les incidències expliquen els motius i les solucions.

## Resum del bloc

El pla de desenvolupament acompanya tot el projecte: orienta les primeres decisions, registra el treball i permet que altres persones el puguin continuar, executar i publicar. La seva utilitat depèn que sigui concret, entenedor i coherent amb l'estat real del codi.
