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
