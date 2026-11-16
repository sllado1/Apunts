# Bloc 7: Docker - empaquetar i desplegar aplicacions

Docker permet empaquetar una aplicació i executar-la en un contenidor. Docker Compose ajuda a descriure i iniciar conjuntament els serveis que necessita, com ara una aplicació web i una base de dades.

En aquest bloc farem servir un projecte fictici anomenat `notes-app`. Els noms i els fitxers són exemples: adapta'ls a l'estructura de cada aplicació.

## Què aprendrem

- Entendre la diferència entre una imatge i un contenidor.
- Construir una imatge a partir d'un `Dockerfile` i publicar-la en un registre.
- Descriure serveis amb Docker Compose.
- Entendre com es passen configuracions i contrasenyes als contenidors.
- Distingir volums amb nom i bind mounts, i saber quines dades conserven.
- Inicialitzar una base de dades i actualitzar-ne l'esquema amb migracions.

## 1. Imatge, contenidor i registre

Una **imatge** és el paquet que Docker utilitza per crear contenidors. Conté l'aplicació, les seves dependències i les instruccions per iniciar-la. Un **contenidor** és una instància d'una imatge en execució. Es pot crear, aturar i recrear un contenidor a partir de la mateixa imatge.

Un **registre** és un servei on es publiquen i des d'on es descarreguen imatges. Docker Hub n'és un exemple.

```text
Dockerfile + codi de l'aplicació
              |
              | docker build
              v
          Imatge (plantilla)
              |
              | docker run
              v
      Contenidor (procés actiu)
```

Les imatges són de només lectura mentre s'executen. Les dades que l'aplicació crea durant l'ús, com ara fitxers pujats o dades de base de dades, s'han de desar en volums si han de sobreviure a la recreació del contenidor.

## 2. Organitzar els fitxers

Una aplicació petita amb una web i una base de dades podria tenir aquesta estructura:

```text
notes-app/
├── Dockerfile
├── .dockerignore
├── .env.example
├── .env                  # configuració local; no es puja al repositori
├── compose.yaml
├── app/
│   └── public/
│       └── index.php
└── db/
    ├── init/
    │   └── 01-schema.sql
    └── migrations/
        └── 001-add-category.sql
```

El `Dockerfile` explica com construir la imatge de l'aplicació. `compose.yaml` descriu els serveis i com es connecten. Els scripts de `db/init/` creen l'esquema inicial quan s'inicia una base de dades buida. Les migracions de `db/migrations/` canvien una base ja existent. `.env.example` és una plantilla sense secrets; `.env` conté els valors locals i no s'ha de versionar.

El fitxer `.dockerignore` evita enviar fitxers innecessaris o secrets al context de construcció:

```text
.git
.env
*.log
```

Comprova que `.env` també és a `.gitignore`. `.dockerignore` i `.gitignore` serveixen per a coses diferents: el primer controla què s'envia a `docker build`; el segon controla què Git incorpora al repositori.

## 3. Construir una imatge amb `Dockerfile`

Exemple de `Dockerfile` per a una aplicació PHP servida per Apache:

```dockerfile
FROM php:8.3-apache
RUN docker-php-ext-install pdo_mysql
COPY app/public/ /var/www/html/
```

- `FROM` tria una imatge base amb PHP i Apache ja instal·lats.
- `RUN` executa una ordre mentre es construeix la imatge; aquí instal·la el controlador PDO per connectar-se a MySQL.
- `COPY` incorpora els fitxers de l'aplicació a la imatge.

Construeix la imatge des de la carpeta `notes-app/`:

```bash
docker build -t notes-app:1.0 .
```

En aquesta ordre, `.` és el **context de construcció**: la carpeta que Docker pot consultar per trobar els fitxers referenciats per `COPY`. El `Dockerfile` s'anomena així i és a la carpeta actual, per tant no cal indicar `-f`. `-t` assigna el nom i l'etiqueta a la imatge: `notes-app` és el nom i `1.0` és la versió.

Si el Dockerfile té un altre nom o és en una altra carpeta, s'indica amb `-f`. Per exemple, executant des de la carpeta que conté `notes-app/`:

```bash
docker build -f notes-app/Dockerfile -t notes-app:1.0 notes-app
```

En aquesta variant, `-f notes-app/Dockerfile` indica quin Dockerfile s'ha de llegir; l'últim argument `notes-app` continua sent el context. `-f` i el context són dues coses diferents.

Per veure les imatges locals:

```bash
docker image ls
```

## 4. Publicar una imatge

Perquè un altre ordinador o servidor pugui descarregar la imatge, publica-la en un registre. En Docker Hub, el nom inclou el teu compte:

```text
USUARI/notes-app:1.0
```

Substitueix `USUARI` pel teu nom de Docker Hub. Inicia sessió i posa a la imatge local l'etiqueta del registre:

```bash
docker login
docker tag notes-app:1.0 USUARI/notes-app:1.0
docker push USUARI/notes-app:1.0
```

`docker tag` crea un nom addicional per a la mateixa imatge local; no la torna a construir. `docker push` la publica. Per descarregar-la en un servidor:

```bash
docker pull USUARI/notes-app:1.0
```

Fes servir una etiqueta nova per a cada versió publicada, com `1.1`. L'etiqueta `latest` és només un nom que algú assigna a una imatge; Docker no comprova si és realment la versió més nova. En desplegaments, una etiqueta explícita facilita saber quina versió s'està executant.

No incloguis contrasenyes ni altres secrets a la imatge o al Dockerfile.

## 5. Configuració amb `.env`

Les aplicacions sovint necessiten configuració que varia entre ordinadors i entorns: noms de bases de dades, usuaris, contrasenyes o ports. Per a l'exemple, crea `.env.example`:

```dotenv
APP_IMAGE=notes-app:1.0
MYSQL_DATABASE=notes
MYSQL_USER=notes_user
MYSQL_PASSWORD=canvia_aquesta_contrasenya
MYSQL_ROOT_PASSWORD=canvia_aquesta_altra
```

Copia'l a `.env` i canvia els valors:

```bash
cp .env.example .env
chmod 600 .env
```

El fitxer `.env` és de configuració local i pot contenir secrets. No el publiquis al repositori. Desa-hi valors reals només en els entorns on s'executi el projecte.

Docker Compose pot llegir `.env` per substituir expressions com `${MYSQL_DATABASE}` que apareixen a `compose.yaml`. Això, per si sol, **no** posa totes les variables dins de cada contenidor: el fitxer Compose ha d'indicar quines variables rep cada servei.

## 6. Definir serveis amb Docker Compose

Un servei és un component que Compose pot crear i gestionar: per exemple, `web` o `db`. Exemple simplificat de `compose.yaml`:

```yaml
services:
  web:
    build: .
    image: ${APP_IMAGE:-notes-app:1.0}
    ports:
      - "8080:80"
    environment:
      DB_HOST: db
      DB_NAME: ${MYSQL_DATABASE}
      DB_USER: ${MYSQL_USER}
      DB_PASSWORD: ${MYSQL_PASSWORD}
    volumes:
      - uploads:/var/www/html/uploads
    networks:
      - web_net
      - db_net
    depends_on:
      - db

  db:
    image: mysql:8.4
    environment:
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
    volumes:
      - db_data:/var/lib/mysql
      - ./db/init:/docker-entrypoint-initdb.d:ro
    networks:
      - db_net

volumes:
  db_data:
  uploads:

networks:
  web_net:
    driver: bridge
  db_net:
    driver: bridge
    internal: true
```

La topologia de xarxa és aquesta:

```text
Navegador de fora
       |
       | port publicat 8080:80
       v
      web ───── db_net interna ───── db
       |
    web_net
```

En llegir aquest exemple, segueix aquestes relacions:

- El navegador es connecta al port `8080` de la màquina; Docker el dirigeix al port `80` de `web`. La publicació `8080:80` fa que el servei web sigui accessible a través de les interfícies de xarxa de la màquina. Per limitar-lo a l'ordinador local, es pot escriure `127.0.0.1:8080:80`.
- `web_net` connecta el servei web amb l'exterior mitjançant el port publicat. `db_net` és una xarxa interna (`internal: true`) que connecta l'aplicació amb la base de dades, sense sortida directa cap a altres xarxes.
- `web` és a totes dues xarxes perquè ha de rebre peticions i parlar amb MySQL. `db` és només a `db_net`; cap port de MySQL es publica a la màquina. Així, l'aplicació pot accedir a la base de dades, mentre que els ordinadors externs només arriben al servei web.
- Compose proporciona resolució de noms dins la xarxa: `web` troba la base de dades amb `DB_HOST=db`, perquè `db` és el nom del servei. Des de `web`, `localhost` voldria dir el mateix contenidor web, no el contenidor de MySQL.
- `depends_on` demana a Compose que iniciï `db` abans de `web`, però no garanteix que MySQL ja estigui preparat per acceptar connexions. L'aplicació ha de poder tornar a provar la connexió si la base encara s'està iniciant.
- El servei `db` no publica el port MySQL a l'ordinador. L'aplicació hi accedeix per la xarxa interna de Compose.
- Si no declarem cap xarxa, Compose crea una xarxa per defecte i hi connecta tots els serveis. Aquí n'hem declarades dues per limitar quins serveis poden comunicar-se entre ells.
- `:ro` vol dir que el contenidor pot llegir els scripts SQL, però no modificar-los.

### Entendre els tipus de volum

Un **volum amb nom** és gestionat per Docker. No cal escollir una carpeta concreta del sistema on desar-lo. A l'exemple, `db_data` conserva els fitxers de la base de dades i `uploads` conserva fitxers pujats per l'aplicació.

Un **bind mount** comparteix una carpeta concreta de l'ordinador amb el contenidor. A l'exemple, `./db/init` és la carpeta `db/init` del projecte i apareix dins del contenidor MySQL a `/docker-entrypoint-initdb.d/`. És útil per passar fitxers de configuració o SQL que es mantenen al projecte.

| Muntatge | Exemple de Compose | Les dades les gestiona... | Ús habitual |
|---|---|---|---|
| Volum amb nom | `db_data:/var/lib/mysql` | Docker | Dades persistents de MySQL. |
| Bind mount | `./db/init:/docker-entrypoint-initdb.d:ro` | La carpeta del projecte | Scripts que volem llegir o editar directament. |

En tots dos casos, la part de la dreta és la ruta dins del contenidor. La part de l'esquerra indica què hi muntem:

- **Volum amb nom:** `db_data:/var/lib/mysql`. `db_data` és el volum que gestiona Docker; dins del contenidor, MySQL desa les dades a `/var/lib/mysql`.
- **Bind mount:** `./db/init:/docker-entrypoint-initdb.d:ro`. `./db/init` és la carpeta del projecte a l'ordinador; dins del contenidor es veu a `/docker-entrypoint-initdb.d`. `ro` indica que el contenidor només la pot llegir.

Per tant, els scripts d'inicialització continuen a `./db/init` al projecte. En canvi, les dades que crea MySQL s'escriuen al volum `db_data`, que Docker conserva encara que recreem el contenidor.

Els contenidors es poden recrear sense perdre el contingut dels volums amb nom. `docker compose down` atura i elimina els contenidors i la xarxa del projecte, però conserva aquests volums. `docker compose down -v` també elimina els volums amb nom i, per tant, les dades que contenen. Fes servir `-v` només quan vulguis esborrar aquestes dades expressament.

## 7. Iniciar Compose i entendre les opcions

La forma més fàcil d'aprendre és entrar primer a la carpeta del projecte, on són `compose.yaml` i `.env`:

```bash
cd notes-app
docker compose up -d
```

Compose troba `compose.yaml` a la carpeta actual i llegeix `.env` automàticament. `up` crea o inicia els serveis; `-d` els deixa executant-se en segon pla. Altres ordres útils:

```bash
docker compose ps
docker compose logs web db
docker compose down
```

Si executes Compose des d'una altra carpeta, indica els camins explícitament. Per exemple, situats al directori pare de `notes-app/`:

```bash
docker compose --env-file notes-app/.env -f notes-app/compose.yaml up -d
```

- `-f notes-app/compose.yaml` indica el fitxer de definició dels serveis.
- `--env-file notes-app/.env` indica el fitxer de variables per substituir `${...}` al YAML.
- Els camins s'interpreten respecte a la carpeta actual del terminal. Per evitar confusions amb camins, és més senzill entrar a la carpeta del projecte abans d'executar Compose.

Comprova que els serveis s'han iniciat i consulta els registres si hi ha errors:

```bash
docker compose ps
docker compose logs web db
```

## 8. Inicialitzar una base de dades

La inicialització prepara una base de dades **nova i buida**: crea taules i, si cal, hi insereix dades inicials. Per exemple, `db/init/01-schema.sql` podria contenir:

```sql
CREATE TABLE notes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    body TEXT NOT NULL
);
```

La imatge oficial de MySQL executa scripts SQL que es munten a `/docker-entrypoint-initdb.d/` quan el directori de dades és buit. Els noms numerats ajuden a fer explícit l'ordre, per exemple `01-schema.sql` i `02-sample-data.sql`.

Els scripts d'inicialització no es tornen a executar cada vegada que s'inicia el contenidor. Quan MySQL ja ha escrit les seves dades al volum `db_data`, editar o afegir un fitxer a `db/init/` no canvia la base existent. Per actualitzar una base existent, es fa servir una migració.

## 9. Migrar l'esquema sense reiniciar la base

Una **migració** és un canvi SQL aplicat a una base de dades existent. Per exemple, per afegir una categoria:

```sql
ALTER TABLE notes ADD COLUMN category VARCHAR(100) NOT NULL DEFAULT '';
```

Desa'l com a `db/migrations/001-add-category.sql`. Des de la carpeta del projecte, envia el fitxer al client MySQL que s'executa al contenidor `db`:

```bash
docker compose exec -T db sh -c 'MYSQL_PWD="$MYSQL_PASSWORD" mysql -u "$MYSQL_USER" "$MYSQL_DATABASE"' \
  < db/migrations/001-add-category.sql
```

`exec` executa una ordre en un contenidor actiu; `-T` desactiva el terminal interactiu perquè la redirecció `<` pugui enviar el contingut del fitxer. El fitxer SQL és llegit des del teu ordinador i enviat al contenidor. Aplica cada migració una sola vegada i anota quines s'han executat.

No esborris el volum `db_data` per canviar l'esquema: conté les dades. Tampoc no tornis a executar scripts d'inicialització sobre una base que ja s'utilitza.

## 10. Publicar una versió nova de l'aplicació

Quan el codi canvia, construeix una imatge amb una etiqueta nova i publica-la. Des de la carpeta del projecte:

```bash
docker build -t USUARI/notes-app:1.1 .
docker push USUARI/notes-app:1.1
```

Actualitza `APP_IMAGE` a `.env`:

```dotenv
APP_IMAGE=USUARI/notes-app:1.1
```

Al servidor, des de la carpeta del projecte, descarrega la imatge i recrea el servei web:

```bash
docker compose pull web
docker compose up -d --no-deps web
```

`pull` descarrega la imatge, però no canvia un contenidor que ja està en execució. `up` crea de nou només el servei `web`; `--no-deps` evita recrear els serveis dels quals depèn, com la base de dades. El volum `db_data` es manté.

Si també canvies l'esquema de la base de dades, fes una còpia de seguretat, aplica la migració compatible i després actualitza l'aplicació. No eliminis el volum per desplegar una versió nova.

## Errors habituals

| Símptoma | Què revisar primer |
|---|---|
| L'aplicació no connecta amb MySQL | A `DB_HOST`, utilitza el nom de servei `db`; revisa les variables de `.env` i els registres. |
| El navegador no arriba a la web | Revisa el port publicat, `docker compose ps` i `docker compose logs web`. |
| MySQL no és accessible des de fora | En aquest exemple és intencionat: MySQL no publica cap port a l'amfitrió. |
| Els scripts SQL no s'han tornat a executar | És el comportament esperat si el volum de dades ja s'havia inicialitzat. Aplica una migració. |
| S'han perdut dades en aturar Compose | Revisa si s'ha executat `docker compose down -v` o s'ha eliminat el volum. |
| El servei web continua amb la imatge antiga | Descarrega la imatge amb `docker compose pull web` i recrea el servei amb `docker compose up -d --no-deps web`. |

## Idees clau

1. El Dockerfile construeix una imatge; un contenidor és una instància en execució d'aquesta imatge.
2. Compose descriu serveis, xarxes, ports i volums en un únic fitxer.
3. El context de `docker build` determina quins fitxers pot utilitzar `COPY`.
4. Un volum amb nom és gestionat per Docker; un bind mount apunta a una carpeta concreta de l'ordinador.
5. `.env` aporta valors a Compose, i el YAML decideix quins passen a cada servei.
6. Els scripts d'inicialització preparen una base nova; les migracions actualitzen una base existent.
7. Recrear contenidors no esborra volums amb nom; `down -v` sí que els elimina.
