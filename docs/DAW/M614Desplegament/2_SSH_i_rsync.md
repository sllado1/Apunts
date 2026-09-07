# Bloc 2: SSH i rsync - connectar-se i desplegar una aplicació

Aquesta guia està pensada per entendre el perquè de les eines, no per memoritzar comandes.

> **Idea clau**
> En desplegament, primer entens el mapa mental i després tries l'eina adequada.

---

## 1. Per què necessitem connectar-nos al servidor?

Pregunta inicial:

- Si els fitxers són en un altre ordinador, com podem entrar-hi?

Quan treballes en local, el projecte viu al teu ordinador.
Quan el desplegues, viu al servidor.

Això implica que, per:

- revisar fitxers remots,
- comprovar rutes,
- executar accions al servidor,

necessites una connexió remota segura.

Analogia simple:

- Treballar en local és com provar la distribució d'un aparador al taller, on pots fer canvis abans que el vegi el públic.
- Desplegar és traslladar aquest muntatge a l'aparador de la botiga, on ja el poden veure els clients.

> **Idea clau**
> El servidor és un altre ordinador, i habitualment geogràficament lluny.

---

## 2. Què és SSH?

SSH és una manera segura de connectar-te a un ordinador remot des de terminal.

Els punts essencials:

- És una connexió remota segura.
- Et permet executar ordres en un altre ordinador.
- És com obrir una terminal al servidor.

Esquema conceptual:

```text
El meu ordinador
       |
   Connexió SSH
       |
Servidor Linux
```

Situació real de projecte:

- "Necessito mirar si el fitxer index.html està realment al directori publicat".

Amb SSH no estàs copiant fitxers encara. Estàs entrant a l'entorn remot per inspeccionar o actuar.

> **Idea clau**
> SSH resol el problema de connectar-se i operar remotament.

---

## 3. Què és rsync?

Pregunta inicial:

- Cada vegada que modifico un fitxer, haig de copiar tota la carpeta?

Rsync resol el problema de sincronitzar contingut entre origen i destí de manera eficient.

Els punts essencials:

- Sincronitza fitxers.
- Copia només els canvis.
- És més ràpid que copiar-ho tot cada vegada.

Esquema conceptual:

```text
[Projecte local]
   fitxer A (canviat)
   fitxer B (igual)
   fitxer C (igual)
        |
      rsync
        |
[Servidor]
   només s'actualitza A
```

Situació real de projecte:

- Has tocat CSS i una vista. No cal tornar a pujar assets enormes que no han canviat.

> **Idea clau**
> Rsync resol el problema de transferir canvis de manera eficient.

### 3.1. Què és SCP i com es compara amb rsync?

SCP (Secure Copy) permet copiar fitxers entre el teu ordinador i un servidor de manera segura, utilitzant SSH.

La diferència principal és què passa quan repeteixes una transferència:

- Amb `scp`, copies els fitxers que indiques, encara que ja existeixin iguals al destí.
- Amb `rsync`, es comprova quins fitxers necessiten actualitzar-se i s'ometen els que es consideren iguals. Per defecte, aquesta comprovació es basa en la mida i la data de modificació.
- En transferències remotes, rsync també pot aprofitar parts d'un fitxer que ja existeixen al destí per reduir les dades enviades.

Situació real de projecte:

- Vols enviar un únic fitxer puntualment: SCP és una opció senzilla.
- Vols desplegar sovint un projecte amb molts fitxers: rsync evita tornar a transferir els que no han canviat.

| Aspecte | SCP | rsync sobre SSH |
|---|---|---|
| Objectiu | Copiar els fitxers indicats | Sincronitzar contingut entre origen i destí |
| Si repeteixes l'enviament | Torna a copiar els fitxers indicats | Omet els fitxers que considera iguals |
| Connexió segura | Utilitza SSH | Utilitza SSH en els exemples d'aquesta guia |
| Fitxers sobrants al destí | No els elimina | Pot eliminar-los amb `--delete`, però no ho fa per defecte |
| Ús habitual | Còpies puntuals | Desplegaments repetits i còpies incrementals |

> **Idea clau**
> SCP copia; rsync sincronitza. Tots dos poden transferir fitxers de manera segura a través de SSH.

### 3.2. I FTP?

FTP (File Transfer Protocol) és un protocol per transferir fitxers entre un client i un servidor. És habitual trobar-lo en allotjaments web, on un client gràfic permet pujar i baixar fitxers arrossegant-los entre carpetes.

Els punts essencials:

- Necessita un servei FTP al servidor.
- Permet pujar, baixar i gestionar fitxers remots, però no obre una terminal per executar ordres com SSH.
- FTP sense xifrat transmet les credencials i les dades en clar.
- FTP no incorpora el mecanisme de transferència de diferències de rsync. Alguns clients poden comparar carpetes i evitar pujar fitxers que no han canviat.

Cal distingir tres noms que sovint es confonen:

| Protocol | Com protegeix la connexió | Relació amb SSH |
|---|---|---|
| FTP | No xifra la connexió | És independent de SSH |
| FTPS | Protegeix FTP amb TLS | És independent de SSH |
| SFTP | Transfereix fitxers a través de SSH | Utilitza SSH; és un protocol diferent de FTP |

Situació real de projecte:

- Si l'allotjament ofereix SFTP, pots pujar fitxers amb un client gràfic i una connexió xifrada.
- Si tens accés SSH i rsync està instal·lat als dos equips, pots fer servir rsync sobre SSH per desplegar els canvis.

> **Idea clau**
> FTP, FTPS i SFTP no són el mateix. Per transferir fitxers de manera segura, utilitza una opció amb xifrat.

---

## 4. SSH i rsync treballen junts

Pensa-ho com dues peces complementàries:

- SSH estableix el canal segur.
- rsync aprofita aquest canal per sincronitzar fitxers.

No són la mateixa eina:

- SSH = connexió/terminal remota
- rsync = sincronització de fitxers

Esquema del procés:

```mermaid
flowchart LR
  A[Ordinador local] -->|Canal segur SSH| B[Servidor]
  A -->|rsync usa el canal SSH| B
  B --> C[Directori publicat]
  C --> D[Apache serveix fitxers]
```

> **Idea clau**
> SSH i rsync no competeixen: es complementen.

---

## 5. Flux típic de desplegament

Abans de cap comanda, el flux mental és aquest:

1. Desenvolupo al meu ordinador.
2. Comprovo que funciona en local.
3. Envio canvis al servidor amb rsync.
4. Apache serveix els fitxers actualitzats.

Esquema curt:

```text
Local -> Validació local -> rsync -> Servidor -> Apache -> Navegador
```

Situació real de projecte:

- Si no valides en local, pots desplegar errors evitables.

> **Idea clau**
> El desplegament bo és un flux disciplinat, no una única comanda.

---

## 6. Les comandes mínimes

Objectiu: entendre la sintaxi bàsica, no memoritzar totes les opcions.

### Comanda 1: SSH

```bash
ssh usuari@servidor
```

Què significa cada part:

- ssh: eina de connexió remota segura.
- usuari: compte amb el qual entres al servidor.
- servidor: màquina remota (host).

Què fa:

- Obre una sessió de terminal al servidor.

### Comanda 2: rsync

```bash
rsync -av ./projecte/ usuari@servidor:/ruta/desti/
```

Què significa cada part:

- rsync: eina de sincronització.
- -a: mode arxiu (manté estructura i metadades bàsiques).
- -v: sortida més explícita (veure què passa).
- ./projecte/: origen local.
- usuari@servidor:/ruta/desti/: destí remot.

Què fa:

- Sincronitza el directori local amb el directori del servidor, enviant principalment canvis.

> **Idea clau**
> SSH i rsync cobreixen la connexió remota i la sincronització del desplegament bàsic.

### Comanda 3: SCP per a una còpia puntual

```bash
scp ./projecte/index.html usuari@servidor:/ruta/desti/
```

Què fa:

- Copia el fitxer local `index.html` al directori indicat del servidor a través de SSH.
- Si ja hi ha un fitxer amb el mateix nom, el sobreescriu si tens permisos.
- Si repeteixes la comanda, torna a copiar el fitxer encara que no l'hagis modificat.

Per copiar una carpeta sencera amb SCP pots utilitzar `-r`. Per actualitzar repetidament un projecte, rsync acostuma a ser més eficient.

---

## 7. Errors habituals

No memoritzis missatges: interpreta'ls.

| Error | Què significa | Causes habituals | Què comprovar primer |
|---|---|---|---|
| Permission denied | No et deixen entrar o escriure | Usuari incorrecte, clau/permisos incorrectes, carpeta sense permisos | Usuari, permisos i ruta de destí |
| Connection refused | El servidor rebutja la connexió | Servei SSH no disponible, host/port incorrectes, màquina no accessible | Que el servidor estigui operatiu i que la dada de connexió sigui correcta |
| No such file or directory | La ruta no existeix | Error de path local o remot, nom mal escrit | Revisar rutes exactes d'origen i destí |

Situació real de projecte:

- El 80% dels errors inicials són d'usuari, ruta o permisos.

> **Idea clau**
> Primer verifica la base: usuari, ruta, permisos i disponibilitat del servidor.

---

## 8. Bones pràctiques

Hàbits que et faran desplegar millor des del primer dia:

- Provar l'aplicació en local abans de desplegar.
- Desplegar només els fitxers necessaris.
- Evitar modificar fitxers directament al servidor si no és una urgència controlada.
- Mantenir una estructura de projecte clara i consistent.
- Deixar un registre curt del que s'ha desplegat i quan.

> **Idea clau**
> Les bones pràctiques redueixen errors repetits i temps perdut.

---

## 9. Resum final

### Resum visual del procés

```text
[1] Desenvolupes en local
[2] Valides que funciona
[3] rsync sincronitza canvis al servidor (via SSH)
[4] Apache serveix els fitxers actualitzats
[5] El navegador mostra el resultat
```

```mermaid
flowchart LR
  A[Local: codi i proves] --> B[Connexió SSH segura]
  B --> C[rsync envia canvis]
  C --> D[Servidor: fitxers actualitzats]
  D --> E[Apache]
  E --> F[Navegador usuari]
```

### Taula comparativa: SSH, SCP, rsync i FTP

| Eina | Per a què serveix | Què no fa | Quan la fas servir |
|---|---|---|---|
| SSH | Connectar-te de forma segura al servidor i executar ordres remotes | No sincronitza per si sola tot el projecte | Quan necessites entrar al servidor o fer comprovacions remotes |
| SCP | Copiar fitxers de manera segura a través de SSH | No evita tornar a copiar fitxers iguals | Quan vols fer una còpia puntual |
| rsync | Sincronitzar fitxers entre local i servidor de forma eficient | No substitueix la lògica d'una sessió remota completa | Quan vols desplegar canvis de fitxers |
| FTP | Transferir i gestionar fitxers en un servidor FTP | No xifra les dades ni ofereix una terminal remota | Quan treballes amb un allotjament que ofereix FTP; cal una alternativa amb xifrat per protegir la transferència |
| SFTP | Transferir i gestionar fitxers de manera segura sobre SSH | No ofereix per si sol la sincronització incremental de rsync | Quan vols pujar o baixar fitxers amb un client compatible, sovint gràfic |

### Idees clau que has de recordar

1. Desplegar no és pujar per pujar: és seguir un flux.
2. SSH connecta; SCP copia; rsync sincronitza.
3. Rsync és eficient perquè envia principalment canvis.
4. El servidor és un altre entorn, amb usuaris i permisos propis.
5. Apache entra en joc després de la sincronització.
6. Si no valides en local, desplegues incertesa.
7. Usuari, ruta i permisos expliquen molts errors inicials.
8. L'objectiu no és memoritzar opcions: és saber deduir decisions.
9. FTP no xifra la connexió; FTPS i SFTP sí, però són protocols diferents.
