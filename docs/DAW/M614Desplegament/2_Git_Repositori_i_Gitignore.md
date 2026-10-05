# Bloc 2. Crear un repositori i decidir què versionem

**Pregunta clau:** com començo i quins fitxers han d'entrar a l'historial?

Configura la identitat que apareixerà als commits una vegada per ordinador. Aquesta configuració no inicia sessió a cap plataforma:

```bash
git config --global user.name "Nom Cognom"
git config --global user.email "alumne@example.com"
```

També pots configurar, una única vegada per ordinador, que la branca principal es digui sempre `main`:

```bash
git config --global init.defaultBranch main
```

Segons la versió de Git instal·lada, un `git init` sense cap opció pot crear per defecte una branca `master` en lloc de `main`. No és cap error, però GitHub, GitLab i la majoria de serveis actuals esperen `main`. Amb aquesta configuració global t'assegures que **tots els repositoris nous** que creïs a partir d'ara utilitzin `main` sense haver-ho d'indicar cada vegada amb `-b main`.

Per començar un projecte nou, executa dins de la seva carpeta:

```bash
git init 
git status
```

Si el projecte ja existeix en un remot, utilitza `git clone URL_DEL_REPOSITORI` i entra a la carpeta creada. **Tria `init` o `clone` segons el cas**; no cal inicialitzar un repositori que acabes de clonar.

Abans del primer commit, crea un fitxer `.gitignore`. Exemple per a un projecte web, que cal adaptar a la tecnologia utilitzada:

```gitignore
.env
node_modules/
vendor/
*.log
```

Versionem el codi, la documentació, els fitxers de dependències i els fitxers de bloqueig de versions. Excloem secrets, dependències instal·lades i fitxers temporals. Podem compartir un `.env.example` amb valors ficticis.

`.gitignore` és un fitxer normal de text: cal afegir-lo i comitejar-lo (`git add .gitignore` o `git add .`) perquè les regles s'apliquin també a la resta de col·laboradors i a altres clonatges del repositori, no només al teu ordinador.

**Atenció:** `.gitignore` només afecta fitxers que encara **no estan seguits** per Git. Si un fitxer ja estava versionat abans de crear la regla, Git el continuarà seguint i el fitxer seguirà apareixent com a modificat, encara que coincideixi amb un patró del `.gitignore`. A més, `.gitignore` no esborra secrets de l'historial: si publiques una credencial, cal revocar-la o substituir-la; eliminar el fitxer no és suficient.

### Deixar de seguir un fitxer ja versionat

Si un fitxer ja estava seguit i vols que a partir d'ara l'ignori, cal deixar-lo de seguir explícitament:

```bash
git rm --cached <fitxer>
```

- `--cached` l'elimina de l'índex de Git (deixa de ser seguit), però **el manté al disc**, sense esborrar-lo.
- A partir d'aquest moment, com que ja no és un fitxer seguit, la regla del `.gitignore` sí que s'hi aplica i Git l'ignorarà en els següents `git status` o `git add`.
- Cal fer `commit` d'aquest canvi (l'eliminació del fitxer de l'historial de seguiment) perquè es propagui a la resta de col·laboradors.

Per exemple, si vas versionar `.env` per error abans de crear el `.gitignore`:

```bash
echo ".env" >> .gitignore
git rm --cached .env
git commit -m "Deixa de seguir .env"
```

**Pràctica:** crea un repositori amb `index.html` i `.gitignore`. Comprova amb `git status` que un fitxer `.env` nou queda exclòs.

## Resum presentació

### Diapositiva 1. Configura la identitat

```bash
git config --global user.name "Nom Cognom"
git config --global user.email "alumne@example.com"
git config --global init.defaultBranch main
```

- Ho configurem **una vegada per ordinador**.
- Nom i correu identifiquen l'autor dels commits; **no inicien sessió** a GitHub o GitLab.
- La tercera ordre defineix `main` com a branca inicial dels repositoris nous.

---

### Diapositiva 2. Com comencem?

| Situació | Ordre |
| --- | --- |
| Projecte local que encara no té Git | `git init` dins la carpeta del projecte. |
| Repositori que ja existeix en un remot | `git clone URL_DEL_REPOSITORI` i entrar a la carpeta creada. |

**Després de clonar, ja tenim un repositori: no cal fer `git init`.**

```bash
git status
```

Ens mostra l'estat dels fitxers i els canvis preparats.

---

### Diapositiva 3. Què versionem?

| Incloem a Git | Excloem de Git |
| --- | --- |
| Codi i documentació | Secrets i credencials: `.env` |
| Fitxers que declaren dependències | Dependències instal·lades: `node_modules/`, `vendor/` |
| Fitxers de bloqueig de versions: `package-lock.json` (npm), `composer.lock` (Composer) | Fitxers temporals i registres: `*.log` |
| `.gitignore` i `.env.example` amb valors ficticis | Configuració privada de cada ordinador |

**L'equip ha de poder reconstruir el projecte sense compartir secrets.**
**Exemple de bloqueig de versions:** `package.json` pot permetre diverses versions d'una dependència; **`package-lock.json` registra les versions exactes resoltes**, també les de les dependències indirectes. El versionem perquè l'equip pugui instal·lar les mateixes versions. En projectes PHP amb Composer, el fitxer equivalent és **`composer.lock`**.

---

### Diapositiva 4. El fitxer .gitignore

Creem un fitxer de text anomenat **`.gitignore`** a l'arrel del repositori:

```gitignore
.env
node_modules/
vendor/
*.log
```

- Cada línia és una regla: nom de fitxer, carpeta o patró.
- Adaptem les regles al projecte.
- **Versionem `.gitignore`** perquè l'equip comparteixi les regles.

---

### Diapositiva 5. Ignorar no és deixar de seguir

```text
Fitxer nou + regla a .gitignore → Git l'ignora.
Fitxer ja seguit + regla nova   → Git el continua seguint.
```

Per deixar de seguir un `.env` ja versionat:

```bash
git rm --cached .env
git add .gitignore
git commit -m "Deixa de seguir .env"
```

**`--cached` conserva el fitxer al disc de qui executa l'ordre i en prepara la retirada del repositori.** El commit registra aquesta retirada; les versions anteriors encara el contenen.

---

### Diapositiva 6. Un secret publicat continua sent un secret exposat

- `.gitignore` **no elimina fitxers dels commits anteriors**.
- Esborrar el fitxer de la versió actual tampoc no esborra l'historial.
- Si hem publicat una contrasenya o un token, cal **revocar-lo o substituir-lo**.
- Compartim un **`.env.example` amb valors ficticis** per indicar quina configuració necessita el projecte.

---

### Diapositiva 7. Exemple i pregunta final

1. Creem una carpeta de projecte i executem `git init`.
2. Creem `index.html`, `.env` i `.gitignore`.
3. Escrivim `.env` dins de `.gitignore`.
4. Executem `git status`: `index.html` i `.gitignore` apareixen com a nous; `.env` queda ignorat.
5. Preparem i guardem la primera versió:

```bash
git add index.html .gitignore
git commit -m "Crea la pàgina inicial i les regles de Git"
```

**Si `.env` ja estava versionat, n'hi ha prou d'afegir-lo a `.gitignore`?**

??? success "Resposta"
    **No.** També cal executar `git rm --cached .env` i fer un commit. Si contenia una credencial publicada, cal revocar-la o substituir-la.