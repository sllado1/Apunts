# Bloc 1: El model mental del desplegament

Aquesta guia va d'entendre què passa quan una aplicació passa de funcionar a un ordinador local a estar disponible a la xarxa.

Treballarem primer amb una **web estàtica servida per Apache**: HTML, CSS, JavaScript i imatges. Aquest model permet entendre les bases; després distingirem què canvia quan hi ha codi que s'executa al servidor.

En acabar el bloc, hauries de poder:

- Explicar amb les teves paraules què són un client, un servidor i HTTP.
- Separar les parts d'una URL i explicar per a què serveixen.
- Escriure rutes que funcionin des de pàgines situades en carpetes diferents.
- Relacionar una petició del navegador amb un fitxer publicat.
- Investigar per què una pàgina carrega però una imatge o un CSS no.

**Com treballarem?** Llegeix els exemples en ordre i intenta respondre les preguntes abans de consultar-ne la solució. Els dominis acabats en `.test` són exemples: no has de poder obrir-los a Internet.


> **Idea clau**
> Desplegar no és copiar fitxers a cegues. És posar una aplicació en un entorn on un servidor la pugui servir de manera fiable als usuaris.

---

## 1. Què vol dir desplegar una aplicació?

### Pensa abans de continuar

- Si el teu projecte funciona al teu ordinador, per què un company no el veu des del seu navegador?

Desplegar vol dir instal·lar o actualitzar una versió de l'aplicació en un servidor, configurar allò que necessita i comprovar que funciona. Aquest entorn pot ser de desenvolupament, de proves o de producció, en una màquina física, una màquina virtual o contenidors; fins i tot pot estar al teu ordinador, sobretot si es tracta d'un entorn de desenvolupament.

En el nostre exemple, publicarem una web en un servidor accessible per la xarxa, de manera que:

- l'usuari hi pot accedir mitjançant una URL;
- el servei web està actiu i pot llegir i servir els fitxers publicats;
- el navegador rep les respostes esperades i la web funciona.

**Local no vol dir necessàriament privat, ni desplegat vol dir públic a Internet.** Una web pot estar disponible només a la xarxa de l'aula. `localhost` apunta al mateix dispositiu que fa la petició: si un company obre `http://localhost/`, està demanant la web al seu ordinador, no al teu.

Analogia ràpida:

- Local: cuines a casa per a tu.
- Desplegat: obres un restaurant amb horari, adreça i servei per a clients.

---

## 2. HTTP: com es comuniquen el navegador i el servidor?

### Pensa abans de continuar

- Qui parla primer, el navegador o el servidor?

### 2.1. Primer, tres paraules

El **client** és el programa que demana un recurs. En els nostres exemples és el navegador. El **servidor web** és el programa que rep la petició i hi respon, com Apache. Un **recurs** és allò que es demana: una pàgina HTML, una imatge, un CSS o unes dades.

**HTTP** (*Hypertext Transfer Protocol*) és el protocol que utilitzen per comunicar-se. Un protocol és un conjunt de regles compartides: defineix com es fan les peticions i com s'escriuen les respostes.

Pensa en aquesta conversa:

```text
Navegador: «Vull obtenir /aula/index.html.»
Servidor:  «D'acord: estat 200. El contingut és HTML. Aquí el tens.»
```

HTTP transporta el contingut; **HTML** descriu l'estructura de la pàgina. Són conceptes diferents, encara que les sigles s'assemblin.

### 2.2. Com és una petició?

Aquest és un exemple simplificat amb el format textual d'HTTP/1.1. No cal memoritzar-lo; cal entendre què significa cada part.

```http
GET /aula/index.html HTTP/1.1
Host: exemple.test

```

| Part | Què diu al servidor? |
|---|---|
| `GET` | Vull obtenir un recurs. És el **mètode** de la petició. |
| `/aula/index.html` | Aquesta és la ruta del recurs que demano. |
| `HTTP/1.1` | Aquest missatge utilitza aquesta versió del protocol. |
| `Host: exemple.test` | Demano el lloc web amb aquest nom. És una **capçalera**. |

Les capçaleres aporten informació sobre la petició. Algunes peticions també tenen **cos**, on s'envien dades. Per exemple, un formulari pot utilitzar el mètode `POST` per enviar les dades al servidor. Per carregar el nostre HTML, CSS i logo farem servir `GET`.

### 2.3. Com és una resposta?

```http
HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8

<!doctype html>
<html lang="ca">
  <head><title>La nostra aula</title></head>
  <body><h1>Benvinguts a l'aula!</h1></body>
</html>
```

Llegeix-la de dalt a baix:

1. **Estat:** `200 OK` indica que la petició s'ha resolt correctament.
2. **Capçaleres:** `Content-Type` indica que el contingut és HTML amb codificació UTF-8.
3. **Línia en blanc:** separa les capçaleres del cos.
4. **Cos:** és el contingut que rep el navegador; aquí, el document HTML.

Si demanes un CSS, el tipus de contingut esperat és `text/css`. Per a un PNG, és `image/png`. Si demanes una imatge però reps una pàgina HTML, cal investigar-ho encara que l'estat sigui `200`.

### 2.4. HTTPS i TLS: com protegim la conversa?

#### El problema: el missatge passa per una xarxa

Imagina que envies un formulari d'accés al web de l'aula. Les dades viatgen del navegador al servidor a través de diversos equips de xarxa. Amb HTTP sense TLS, algú amb capacitat d'interceptar aquesta comunicació podria llegir-la o modificar-la.

Com a analogia, pensa en una **postal**: qui la manipula pot llegir-ne el text. Volem enviar el missatge dins d'un sobre que n'oculti el contingut, permeti detectar manipulacions i arribi al destinatari correcte. TLS aporta aquestes proteccions amb criptografia.

#### Quina diferència hi ha entre HTTP, HTTPS i TLS?

| Concepte | Quina feina fa? | Com ho pots recordar? |
|---|---|---|
| **HTTP** | Defineix les peticions i les respostes del web. | La conversa: «demano una pàgina», «aquí la tens». |
| **TLS** (*Transport Layer Security*) | Protegeix la comunicació entre els dos extrems. | La protecció amb què viatja la conversa. |
| **HTTPS** | És l'ús d'HTTP amb TLS. | La conversa HTTP protegida. |

```text
HTTPS = HTTP + protecció TLS

Navegador                 Xarxa                   Servidor
contingut llegible  →  dades xifrades  →  contingut llegible
                   ←  dades xifrades  ←
```

**Xifrar** vol dir transformar dades llegibles en dades que no es poden interpretar sense les claus adequades. El navegador i el servidor les poden desxifrar. TLS protegeix tant la petició com la resposta, incloses les capçaleres i el cos. Vegeu la [introducció a TLS de MDN](https://developer.mozilla.org/en-US/docs/Web/Security/Defenses/Transport_Layer_Security).

#### Les tres preguntes que resol TLS

| Pregunta | Protecció | Exemple al web de l'aula |
|---|---|---|
| Algú pot llegir el contingut pel camí? | **Confidencialitat:** les dades viatgen xifrades. | Un observador de la xarxa no pot llegir el formulari interceptant el trànsit protegit. |
| Algú pot canviar el missatge sense que es detecti? | **Integritat:** es comprova si les dades han estat alterades. | Una modificació del contingut en trànsit fa que la verificació falli. |
| Parlo amb el servidor del nom que he escrit? | **Autenticació del servidor:** es comprova la seva identitat per a aquell nom. | El navegador verifica que el servidor pot acreditar-se per a `aula.exemple.test`. |

#### Què passa abans de demanar la pàgina?

En una connexió HTTPS nova habitual, navegador i servidor fan una negociació inicial anomenada **handshake TLS**. Aquest esquema en resumeix la idea, sense entrar en els missatges criptogràfics:

1. El navegador inicia la connexió i proposa opcions de comunicació segura.
2. El servidor presenta el seu certificat i demostra que disposa de la clau privada corresponent.
3. El navegador valida el certificat per al nom demanat.
4. Tots dos obtenen claus de sessió mitjançant un acord criptogràfic, sense enviar aquestes claus en clar.
5. Intercanvien les peticions i respostes HTTP protegides amb les claus de sessió.

Aquestes funcions es descriuen en l'[especificació de TLS 1.3](https://www.rfc-editor.org/rfc/rfc8446). No cal memoritzar els algoritmes per entendre el desplegament.

#### Què és un certificat?

Un **certificat digital** vincula un nom de domini amb una clau pública. Inclou dades com els noms per als quals és vàlid, el període de validesa i la signatura de l'entitat emissora. La **clau privada** corresponent es manté secreta al servei que gestiona TLS; no s'envia al navegador.

Pensa en una acreditació: no n'hi ha prou que algú digui «sóc el servidor de l'aula»; ha de poder demostrar-ho i l'acreditació ha de ser verificable.

El navegador comprova, entre altres coses, que el certificat correspon al nom de la URL, que és vigent i que la cadena de signatures arriba a una autoritat en què confia. Si alguna comprovació falla, pot mostrar un avís de certificat.

Una **autoritat de certificació (CA)** emet certificats. Per exemple, Let's Encrypt comprova el control del domini abans d'emetre'n un i permet automatitzar-ne la renovació. Pots consultar [com funciona l'emissió de certificats a Let's Encrypt](https://letsencrypt.org/how-it-works/).

#### Exemple: HTTPS funciona, però la pàgina no existeix

Escrius `https://aula.exemple.test/apunts.html`. La connexió TLS s'estableix correctament, però el servidor no troba el recurs i retorna `404`.

**És perfectament possible:** HTTPS protegeix la resposta, també quan és una resposta d'error. No crea el fitxer que falta ni corregeix la ruta.

Tampoc certifica que el contingut sigui honest: una web enganyosa pot tenir un certificat vàlid per al seu propi domini. Cal llegir el nom de la URL. I el servidor destinatari pot llegir les dades rebudes; protegir-les després, quan s'emmagatzemen, és una altra responsabilitat.

#### Què implica per al desplegament?

Canviar el text `http://` per `https://` no configura el servidor. El servei ha de tenir HTTPS habilitat, un certificat adequat amb la seva clau privada i un port accessible, habitualment el `443`. El certificat també s'ha de renovar abans que caduqui.

En el nostre model senzill, Apache pot gestionar TLS. En altres desplegaments ho fa un servei situat al davant d'Apache: la protecció de cada tram s'ha de configurar.

> **Comprova que ho entens**
> Si una web utilitza HTTPS, vol dir que no pot retornar un `404`? Pot llegir el servidor les dades que li envies?

??? note "Resposta raonada"

    Pot retornar un `404`: la comunicació està protegida, però el recurs pot no existir. El servidor sí que pot llegir les dades, perquè és un dels extrems de la comunicació TLS. HTTPS les protegeix durant el trajecte entre aquests extrems.

> **Comprova que ho entens**
> En demanar `logo.png`, qui envia el `GET` i qui envia el codi `200`?
>
> **Resposta:** el navegador envia el `GET`; el servidor retorna el codi d'estat amb la resposta.

Pots ampliar-ho a la [introducció a HTTP de MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Overview).

### 2.5. El recorregut complet

Recorregut base d'una petició d'un fitxer estàtic:

Navegador → xarxa → Apache, que consulta els fitxers publicats → resposta HTTP al navegador.

```text
[Navegador] -- petició HTTP per la xarxa --> [Apache al servidor]
                                                    |
                                      consulta configuració i permisos
                                                    |
                                      llegeix el fitxer publicat
                                                    |
[Navegador] <-- resposta HTTP per la xarxa -----------+
```

Què fa cada element:

- Navegador: fa la petició i mostra la resposta.
- Xarxa: transporta la petició i la resposta; pot ser una xarxa local o Internet.
- Servidor (màquina): allotja els fitxers i executa els serveis.
- Apache (programari servidor web): rep peticions HTTP i les resol segons la configuració. És una de les opcions per crear un servidor web.
- DocumentRoot: directori base configurat per servir els fitxers d'un lloc web. És una ubicació del sistema de fitxers, no un servei pel qual passi la petició.
- Fitxers: HTML, CSS, JS, imatges i altres recursos.
- Resposta HTTP: inclou un codi d'estat, capçaleres (com el tipus de contingut) i, habitualment, un cos amb el recurs o un missatge d'error.

### I si l'aplicació és dinàmica?

Apache pot delegar la petició a un entorn d'execució o a un servei d'aplicació. Aquest executa codi, pot consultar una base de dades i genera una resposta, per exemple HTML o JSON. Per tant, **una URL no sempre correspon a un fitxer**.

El JavaScript de la web estàtica s'executa al navegador. El codi del servidor s'executa al servidor: el client en rep el resultat, no el codi font. Desplegar una aplicació dinàmica també pot requerir dependències, variables d'entorn, processos actius i preparació de la base de dades.

> **Idea clau**
> El navegador no "entra" al servidor. Demana, i Apache respon.

---

## 3. Qui és responsable de què?

### Pensa abans de continuar

- Si una pàgina dona error, de qui pot ser el problema?

| Persona o component | Responsabilitat principal | Exemple de problema |
|---|---|---|
| Desenvolupador | Preparar codi i estructura correctes | Ruta mal escrita a una imatge |
| Servidor | Estar disponible i connectat | Màquina apagada o saturada |
| Apache | Servir fitxers i gestionar peticions | Configuració que apunta a una carpeta incorrecta |
| Sistema operatiu | Permisos, usuaris i fitxers | Apache no pot llegir un directori |
| Xarxa i DNS | Permetre la connexió i resoldre el nom del servidor | Domini mal configurat o port bloquejat |
| Navegador | Interpretar la resposta i executar el codi de client | Memòria cau antiga o error de JavaScript |

Les persones responsables del desplegament configuren i supervisen aquests components. La taula ajuda a localitzar la capa on falla el servei, no a atribuir culpes.

> **Idea clau**
> Desplegar bé és coordinar responsabilitats, no només "fer pujada" de fitxers.

---

## 4. On són els fitxers?

### Pensa abans de continuar

- Si edites un fitxer al teu ordinador, canvia automàticament al servidor?

Diferències clau:

- El meu ordinador: conserva la còpia de treball amb què desenvolupo.
- El servidor de destinació: conté la versió desplegada.
- DocumentRoot: directori base de publicació del lloc; Habitualment la carpeta del projecte. És a dir, el servidor no "llegeix" el projecte, sinó la carpeta configurada com a DocumentRoot.

Esquema ASCII:

```text
[Ordinador local]
  /projecte-web
    index.html
    css/
    js/

        (pujada / sincronització)
                 ||
                 \/

[Servidor remot]
  /var/www/
    html/            <-- DocumentRoot (exemple)
      index.html
      css/
      js/
```

> **Idea clau**
> Desar a l'editor modifica la còpia local. La versió desplegada només canvia si hi ha una transferència, una sincronització o un procés de desplegament que l'actualitzi.

Cal publicar només els fitxers destinats al web. Credencials, còpies de seguretat i fitxers com `.env` han de quedar fora de l'àrea pública. En projectes amb compilació, sovint es publica el resultat generat, no tot el codi del projecte.

---

## 5. URL i rutes: com sap el navegador què ha de demanar?

### Pensa abans de continuar

- Quan escrius una URL, qui decideix quin fitxer s'envia?

### 5.1. Una URL és l'adreça d'un recurs

**URL** vol dir *Uniform Resource Locator*. És una adreça que permet localitzar un recurs. Observa aquest exemple i separa'n les peces:

```text
https://exemple.test:8443/aula/index.html?idioma=ca#horari
\___/   \__________/\__/\______________/\_______/\_____/
esquema     host    port      ruta       consulta fragment
```

| Peça | Exemple | Per a què serveix? |
|---|---|---|
| Esquema | `https` | Indica com s'accedeix al recurs (protocol); aquí, amb HTTPS. |
| Host | `exemple.test` | Identifica el servidor pel nom (domini); també pot ser una IP. |
| Port | `8443` | Identifica el punt de connexió del servei dins de la màquina. |
| Ruta | `/aula/index.html` | Identifica el recurs dins la carpeta del projecte. |
| Consulta | `?idioma=ca` | Envia informació addicional; l'aplicació decideix com interpretar-la. |
| Fragment | `#horari` | Pot indicar una secció del document, com un element amb `id="horari"`. |

El port es pot ometre quan és el predeterminat: **80 per a HTTP i 443 per a HTTPS**. Escriure `:8443` només funcionarà si hi ha un servei HTTPS configurat i que escolti aquest port. Si no, el navegador mostrarà un error de connexió.

La consulta comença amb `?`; és habitual separar diversos paràmetres amb `&`, com `?idioma=ca&grup=2`. El fragment comença amb `#` i **no s'envia al servidor en la petició HTTP**. En aquest exemple, el servidor rep la ruta i la consulta; el navegador gestiona el fragment.

Una web estàtica no canvia d'idioma automàticament perquè afegeixis `?idioma=ca`: cal codi que ho interpreti.

> **Prova-ho mentalment**
> A `http://localhost:8080/imatges/logo.png`, quin és el port i quin recurs es demana?
>
> **Resposta:** port `8080`, recurs `/imatges/logo.png`, al mateix dispositiu des del qual fas la petició.

Referència: [les parts d'una URL, a MDN](https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Web_mechanics/What_is_a_URL).

### 5.2. Què passa després d'escriure-la?

Procés simplificat, suposant que cal accedir a la xarxa:

1. L'usuari escriu una URL al navegador.
2. Si la URL conté un nom de domini, es resol a una adreça IP mitjançant DNS, si aquesta informació no està en memòria cau.
3. El navegador estableix o reutilitza una connexió amb el servei. Els ports habituals són el 80 per a HTTP i el 443 per a HTTPS. HTTPS protegeix la comunicació amb TLS.
4. El navegador envia una petició HTTP, per exemple `GET /css/styles.css`.
5. Apache selecciona el lloc web segons la configuració i el nom demanat, i resol la ruta del recurs.
6. Per a un fitxer estàtic, comprova les regles d'accés i els permisos. Si el pot servir, retorna el contingut; si no, retorna la resposta corresponent.
7. El navegador interpreta la resposta segons el tipus de contingut.
8. En processar l'HTML, demana els recursos referenciats, com CSS, JavaScript i imatges, quan cal. Alguns es poden reutilitzar des de la memòria cau.

### 5.3. Dues adreces diferents: la URL i la ruta del disc

Suposem un lloc amb `DocumentRoot /var/www/html`, sense àlies ni reescriptures:

```text
URL:       https://exemple.test/css/styles.css
Domini:    exemple.test
Ruta URL:  /css/styles.css
Fitxer:    /var/www/html/css/styles.css
```

La ruta del disc `/var/www/html` no forma part de la URL. En demanar `/`, Apache pot servir `index.html` si està configurat com a índex mitjançant `DirectoryIndex`. Si no hi ha cap índex disponible, la configuració determina si es mostra un llistat o es denega l'accés. Vegeu la documentació d'[Apache sobre URL i fitxers](https://httpd.apache.org/docs/2.4/urlmapping.html) i [DirectoryIndex](https://httpd.apache.org/docs/2.4/mod/mod_dir.html#directoryindex).

**Obrir un fitxer i visitar una web són accions diferents:**

| Adreça | Què fa el navegador? |
|---|---|
| `file:///C:/projecte/index.html` | Llegeix un fitxer local; no el demana a Apache mitjançant HTTP. |
| `http://localhost/index.html` | Demana el recurs al servidor web del teu dispositiu. Cal que estigui actiu. |
| `https://exemple.test/index.html` | Demana el recurs al servei corresponent a aquest nom. |

Una ruta com `C:\projecte\logo.png` descriu un fitxer del teu ordinador. No serveix per indicar als visitants on has publicat la imatge. En les rutes web escrivim barres `/`.

### 5.4. Tres maneres d'indicar un recurs

Imagina que tenim aquests fitxers publicats:

```text
/var/www/html/                 ← DocumentRoot
└── aula/
    ├── index.html
    ├── css/
    │   └── styles.css
    ├── imatges/
    │   └── logo.png
    └── pagines/
        └── contacte.html
```

Estàs visitant `https://exemple.test/aula/index.html`. Per carregar el logo pots escriure:

| Tipus de referència | Exemple a l'HTML | Punt de partida |
|---|---|---|
| URL absoluta, completa | `src="https://exemple.test/aula/imatges/logo.png"` | Inclou l'esquema, el host i tota la ruta. |
| Ruta des de l'arrel del lloc | `src="/aula/imatges/logo.png"` | Comença a `/` del mateix origen (esquema, host i port). |
| Ruta relativa al document | `src="imatges/logo.png"` | Parteix de la carpeta de la URL del document. |

Les tres referències porten al mateix logo en aquest exemple. La segona també s'anomena sovint «ruta absoluta», però **no és una URL completa ni una ruta absoluta del disc**. Aquí direm «ruta des de l'arrel (DocumentRoot)» per distingir-les.


### 5.5. Rutes relatives: on soc i on vull anar?

Per escriure una ruta relativa, fes aquests tres passos:

1. Mira la URL de la pàgina actual i identifica'n la carpeta.
2. Localitza la carpeta del recurs que vols demanar.
3. Escriu el camí: entra en carpetes amb `nom/` i puja un nivell amb `../`.

`./` significa «des d'aquesta mateixa carpeta». Així, `./imatges/logo.png` i `imatges/logo.png` tenen el mateix resultat.

**Exemple resolt: carregar el logo des de la pàgina de contacte.**

La pàgina és `https://exemple.test/aula/pagines/contacte.html`. El logo és a `/aula/imatges/logo.png`.

```text
/var/www/html/                 ← DocumentRoot
└── aula/
    ├── index.html
    ├── css/
    │   └── styles.css
    ├── imatges/
    │   └── logo.png
    └── pagines/
        └── contacte.html
```

```text
Començo a:       /aula/pagines/
Pujo amb ../:    /aula/
Entro a imatges: /aula/imatges/
Demano el logo:  /aula/imatges/logo.png

Ruta que escric: ../imatges/logo.png
```

Per tant, a `contacte.html` escric:

```html
<img src="../imatges/logo.png" alt="Logotip de l'aula">
```

Compara què passa si canviem la ruta **des d'aquesta mateixa pàgina**:

| Valor de `src` | Ruta que demana el navegador | Resultat amb l'arbre anterior |
|---|---|---|
| `imatges/logo.png` | `/aula/pagines/imatges/logo.png` | `404`: aquesta ubicació no existeix. |
| `../imatges/logo.png` | `/aula/imatges/logo.png` | Ubicació correcta. |
| `/imatges/logo.png` | `/imatges/logo.png` | `404`: hem sortit de `/aula/`. |
| `/aula/imatges/logo.png` | `/aula/imatges/logo.png` | Ubicació correcta. |

Una ubicació correcta encara requereix que el servidor permeti servir el fitxer, funcioni el servidor web i que el fitxer estigui accessible.

> **Idea clau**
> Una barra inicial `/` vol dir «comença a l'arrel del lloc», no «comença a la carpeta del meu projecte». Això és especialment important si publiques el projecte dins d'una subcarpeta.

#### Per què importa la barra final d'una URL?

Quan el navegador troba una ruta relativa com `logo.png`, l'ha de combinar amb la URL de la pàgina actual. Per fer-ho, es fixa en la **forma de la URL**, perquè no coneix l'organització real de les carpetes del servidor.

Compara aquests dos casos:

| URL actual | Com la interpreta el navegador | Resultat de `logo.png` |
|---|---|---|
| `https://exemple.test/aula/` | `aula/` representa una carpeta. | `https://exemple.test/aula/logo.png` |
| `https://exemple.test/aula` | `aula` representa l'últim recurs de la ruta, com si fos el nom d'un fitxer. El navegador el substitueix. | `https://exemple.test/logo.png` |

En el segon cas, el navegador no pot endevinar que `aula` és realment un directori del servidor. Aplica les regles de resolució d'URL i elimina l'últim segment abans d'afegir `logo.png`:

```text
Base amb barra:    /aula/ + logo.png  → /aula/logo.png
Base sense barra:  /aula  + logo.png  → /logo.png
                            └─ substitueix «aula»
```

Si `/aula` correspon a un directori, Apache acostuma a respondre amb una redirecció cap a `/aula/`. El navegador rep aquesta nova adreça i torna a fer la petició. Així, la URL acaba amb `/` abans que el navegador resolgui les rutes relatives del document.

```text
1. Navegador demana:  GET /aula
2. Apache respon:     redirecció cap a /aula/
3. Navegador demana:  GET /aula/
4. Apache respon:     index.html
5. El navegador resol logo.png com /aula/logo.png
```

> **Idea clau**
> En una URL, la barra final comunica que l'últim segment és un directori. Sense la barra, una ruta relativa substitueix l'últim segment.

Referència: [resolució de referències relatives, a MDN](https://developer.mozilla.org/en-US/docs/Web/API/URL_API/Resolving_relative_references).

### 5.6. I les rutes que escrivim dins del CSS?

En un **fitxer CSS extern**, les referències `url(...)` es resolen respecte de la URL del CSS, no de la pàgina HTML.

El nostre CSS és a `/aula/css/styles.css`. Per arribar a `/aula/imatges/logo.png`, ha de pujar un nivell:

```css
.capcalera {
  background-image: url("../imatges/logo.png");
}
```

Així, el mateix CSS pot carregar la imatge tant si l'utilitza `index.html` com si l'utilitza `pagines/contacte.html`.

### 5.7. Una pàgina, diverses peticions

Si `/aula/index.html` conté:

```html
<link rel="stylesheet" href="css/styles.css">
<img src="imatges/logo.png" alt="Logotip de l'aula">
<a href="pagines/contacte.html">Contacte</a>
```

El navegador primer obté l'HTML i, en processar-lo, demana el CSS i la imatge si els necessita. L'enllaç de contacte permet navegar a una altra pàgina quan el cliques; no és un recurs que calgui carregar per mostrar aquest HTML.

```text
GET /aula/index.html         → 200, HTML
GET /aula/css/styles.css     → 200, CSS
GET /aula/imatges/logo.png   → 200, imatge
```

Cada petició té el seu propi resultat: l'HTML pot retornar `200` i el logo `404`.

En els sistemes de fitxers Linux habituals, `Logo.png` i `logo.png` són noms diferents. Una diferència de majúscules pot passar desapercebuda en local i fallar al servidor.

> **Idea clau**
> Carregar una pàgina acostuma a implicar diverses peticions. Que arribi l'HTML no garanteix que arribin tots els recursos.

---

## 6. Errors habituals

### Pensa abans de continuar

- Quina diferència hi ha entre "no existeix" i "existeix però no hi puc entrar"?

Interpretació intuïtiva:

- 403 (Forbidden): "He entès la petició, però en denego l'accés". No confirma que el fitxer existeixi.
- 404 (Not Found): "No trobo el recurs que m'has demanat".
- 500 (Internal Server Error): "Ha fallat alguna cosa al servidor en processar la petició".

Relació ràpida amb el projecte:

- 403: regles d'accés, permisos insuficients o directori sense índex amb el llistat desactivat (Usuari Apache no té accés sobre el recurs).
- 404: rutes mal escrites o fitxers no pujats.
- 500: error intern d'aplicació o configuració.

El significat de [403 Forbidden](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/403) descriu la resposta, però no identifica per si sol la causa concreta.

**No tots els errors són respostes HTTP.** Si falla el DNS, es rebutja la connexió o hi ha un problema de certificat TLS, pot ser que no s'arribi a obtenir cap codi HTTP. I un `200 OK` indica que la petició s'ha resolt correctament a nivell HTTP, però no garanteix que el contingut rebut sigui l'esperat ni que el JavaScript funcioni.

### Mètode inicial de diagnòstic

1. Obre les eines de desenvolupament del navegador (`F12` o el menú del navegador), entra a **Xarxa / Network** i recarrega la pàgina.
2. Selecciona la petició que falla i anota la URL exacta, el codi d'estat (si n'hi ha), el tipus de contingut i la resposta rebuda.
3. Compara la ruta demanada amb la ubicació i el nom del fitxer al servidor, incloses les majúscules.
4. Consulta la **Consola / Console** per detectar errors d'execució o recursos bloquejats. Si tens accés al servidor, contrasta-ho amb els registres d'accés i d'errors.
5. Formula una hipòtesi, fes una comprovació concreta i torna a provar després de corregir-la.

> **Idea clau**
> El codi d'error no és l'enemic: és la pista principal de diagnosi.

---

## 7. Preguntes per construir el coneixement

### Abans de continuar: practica les rutes

Utilitza el següent arbre de fitxers.

```text
/var/www/html/                 ← DocumentRoot
└── aula/
    ├── index.html
    ├── css/
    │   └── styles.css
    ├── imatges/
    │   └── logo.png
    └── pagines/
        └── contacte.html
```

 Escriu les respostes abans d'obrir la solució.

1. Des de `/aula/index.html`, quina ruta relativa utilitzaries per enllaçar `pagines/contacte.html`?
2. Des de `/aula/pagines/contacte.html`, quina ruta relativa utilitzaries per carregar `css/styles.css`?
3. Des de la mateixa pàgina de contacte, on portaria `href="/index.html"`?
4. A `https://exemple.test/aula/index.html?grup=2#horari`, què s'envia com a ruta i consulta? S'hi envia `#horari`?
5. Si el logo retorna `404` però l'HTML retorna `200`, ha fallat necessàriament tota la web?

??? note "Solucions raonades"

    1. `pagines/contacte.html`: des de `/aula/`, entres a `pagines/`.
    2. `../css/styles.css`: puges de `/aula/pagines/` a `/aula/` i entres a `css/`.
    3. A `https://exemple.test/index.html`, perquè la barra inicial parteix de l'arrel. Per tornar a l'índex de l'aula pots escriure `../index.html`.
    4. `/aula/index.html?grup=2`. El fragment `#horari` no s'envia en la petició HTTP.
    5. No. Cada recurs té una petició independent. Cal investigar la URL del logo i la seva ubicació.



---

## 8. Resum final (1 pàgina visual)

```text
MODEL MENTAL DEL DESPLEGAMENT (M614 - Bloc 1)

1) DESPLEGAR = instal·lar o actualitzar, configurar i verificar en un entorn
2) RECORREGUT = Navegador -> xarxa -> servei web -> resposta al navegador
3) CLAU = el navegador demana; Apache respon
4) RECURS = pot ser un fitxer publicat o una resposta generada per l'aplicació
5) URL = no és una ruta del disc; una pàgina sol requerir diverses peticions
6) ERRORS:
   - 403: accés denegat
   - 404: no trobat
   - 500: error intern del servidor
   - DNS, connexió o TLS: pot no haver-hi resposta HTTP
7) MÈTODE = observar peticions, formular hipòtesis, comprovar i tornar a provar
```

| Si veus… | Recorda… |
|---|---|
| HTTP | Regles de petició i resposta entre client i servidor. |
| HTTPS | HTTP amb la comunicació protegida amb TLS. |
| `https://exemple.test/aula/` | URL completa: indica com accedir-hi i on. |
| `/aula/imatges/logo.png` | Ruta des de l'arrel del lloc. |
| `imatges/logo.png` | Ruta relativa a la carpeta actual. |
| `../imatges/logo.png` | Puja un nivell abans d'entrar a `imatges/`. |
| `/var/www/html/aula/imatges/logo.png` | Ruta del disc del servidor; no és la URL pública. |
| `?grup=2` | Consulta que s'envia al servidor. |
| `#horari` | Fragment que gestiona el client. |

> **Idea clau**
> Abans d'aprendre Apache, SSH o rsync, cal entendre el mapa mental del desplegament.
