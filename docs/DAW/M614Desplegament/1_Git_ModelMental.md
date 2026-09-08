# Bloc 1. El model mental de Git

**Pregunta clau:** què guarda Git i on són els meus canvis?

Per entendre Git, és útil imaginar que el projecte té diferents “estats” o “espais de treball”. Els fitxers no es guarden directament a la història del projecte fins que decidim explícitament què volem registrar.

## 1. El repositori: la base de dades del projecte

- **Repositori** és el conjunt de fitxers del projecte més el seu historial de versions.
- Git no guarda només el contingut actual, sinó també totes les versions anteriors que hem validat.
- El repositori és el lloc on Git “recorda” el projecte i on hi ha els commits.
- En un repositori local, aquesta informació es guarda normalment a la carpeta `.git`.

És com un “arxiu de versions” del projecte: cada vegada que fem un canvi important, podem guardar una instantània de l’estat actual.

## 2. El directori de treball: on editem els fitxers

- Els fitxers que veiem a l’ordinador i modifiquem a l’editor es troben al **directori de treball**.
- Aquí els canvis encara no són oficials per a Git; poden estar modificats, no seguits o simplement no guardats en el historial.
- Si desem un fitxer, aquest canvi continua a l’espai de treball, però no significa que ja hagi passat a la història de Git.

## 3. L’àrea d’index o staging: el “preparar la foto”

- L’**àrea d’index** o **staging** és una zona intermèdia on decidim quins canvis formaran part del proper commit.
- Quan fem `git add`, estem dient a Git: “d’aquests canvis, vull guardar-ne una instantània en el següent commit”.
- Aquí encara no està creat el commit, però ja hem marcat quins fitxers volem incloure.

És com preparar la llista de coses que aniran a la propera fotografia del projecte.

## 4. El commit: una instantània de la versió

- **Commit** és una instantània del contingut que hem preparat, amb informació com l’autor, el moment i un missatge descriptiu.
- Cada commit té un identificador únic i representa un canvi coherent i revisable.
- Un commit no és “el fitxer que s’ha modificat”, sinó “l’estat complet del projecte en un moment determinat”.

Si un canvi és important o coherent, el guardem amb un commit. El commit passa a formar part de l’historial local del repositori.

## 5. La branca: una línia de treball

- **Branca** és una línia de desenvolupament que apunta a un commit concret.
- Permet treballar en paral·lel sense afectar directament la branca principal o “base” del projecte.
- Per exemple, podem tenir una branca `main` i crear una branca de funcionalitat per provar alguna millora.

Una branca és com una “ruta de treball” diferent sobre el mateix projecte.

## 6. El remot: el repositori compartit

- **Remot** és un repositori de referència extern, normalment a GitHub, GitLab o un servidor propi.
- El nom més habitual és `origin`, que indica el repositori principal del projecte, però pot ser qualsevol nom, el decidim nosaltres en el moment de crear la referència.
- Fer `git push` envia els commits locals al remot; fer `git pull` o `git fetch` obté canvis del remot.

El remot no és el lloc on Git guarda els canvis “de manera automàtica”; el flux normal és: fer canvis localment, validar-los amb commits i després sincronitzar-los amb el remot.

## 7. El recorregut habitual dels canvis

```text
Fitxers de treball → Preparació (staging) → Historial local → Repositori remot
                  git add              git commit       git push
```

Aquest flux explica el model mental bàsic:

1. Modifiquem fitxers al directori de treball.
2. Fem `git add` per decidir què entra al proper commit.
3. Fem `git commit` per guardar una instantània al historial local.
4. Fem `git push` per publicar els commits al repositori remot.

> Desar un fitxer no crea un commit. Fer un commit no publica res al remot. Git funciona localment i pot registrar versions sense connexió.

## 8. Resum mental

La idea clau és aquesta:

- **Directori de treball:** on escric i modifico fitxers.
- **Staging:** on preparo el que entrarà al proper snapshot.
- **Commit:** on git guarda una versió coherent del projecte.
- **Branca:** línia de treball on avanço els canvis.
- **Remot:** còpia compartida del repositori.

Un bon model mental és pensar que Git és un sistema que guarda “instantànies del projecte” en lloc de registrar només canvis puntuals sense context.

**Pràctica:** explica on es troba un canvi després de desar-lo, després de fer `git add` i després de fer `git commit`.
