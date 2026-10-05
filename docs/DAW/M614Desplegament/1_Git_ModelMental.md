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

## 9. Resum presentació

### Diapositiva 1. Què fa Git?

- Guarda **versions del projecte** i el seu historial.
- Permet recuperar versions anteriors i treballar en equip.
- Funciona **localment**, també sense connexió.

---

### Diapositiva 2. On són els meus canvis?

| Espai | Què hi fem? |
| --- | --- |
| **Directori de treball** | Editem i desem els fitxers. |
| **Staging** | Preparem el contingut del proper commit. |
| **Historial local** | Guardem versions amb commits. |
| **Remot** | Compartim els commits amb l'equip. |

---

### Diapositiva 3. El recorregut d'un canvi

```text
  EDITAR          PREPARAR         GUARDAR VERSIÓ       COMPARTIR
    │                │                  │                  │
    ▼                ▼                  ▼                  ▼
 Treball ───────► Staging ───────► Historial local ───────► Remot
         git add         git commit              git push
```

**Desar ≠ fer un commit ≠ publicar al remot.**

---

### Diapositiva 4. Què és un commit?

- Una **instantània del contingut preparat** del projecte.
- Té identificador, autor, data i un **missatge descriptiu**.
- Ha de representar un canvi coherent: per exemple, «Corregeix el formulari de registre».

**Si editem un fitxer després de `git add`, cal tornar-lo a preparar per incloure la nova edició.**

---

### Diapositiva 5. Branques: línies de treball

- `main` pot ser la branca principal.
- Una altra branca permet desenvolupar una millora per separat.
- Una branca **apunta a un commit**; podem integrar-ne el treball més endavant.

```text
main:       A ── B ── C
                 ╲
millora:          D ── E
```

---

### Diapositiva 6. El repositori remot

- És un repositori compartit, per exemple a **GitHub o GitLab**.
- `origin` és un nom habitual per referir-nos a un remot.
- **`push`** envia commits; **`fetch`** obté informació i commits del remot; **`pull`** els obté i els integra a la branca actual.

**Git és l'eina de control de versions; GitHub és una plataforma on podem allotjar repositoris.**

---

### Diapositiva 7. Exemple i pregunta final

Editem `index.html`:

| Acció | Què passa? |
| --- | --- |
| Desem el fitxer | El canvi és al directori de treball. |
| `git add index.html` | Preparem el contingut actual del fitxer. |
| `git commit -m "Actualitza la portada"` | Creem una versió a l'historial local. |
| `git push` | Enviem els commits al remot configurat. |

**Si només he fet un commit, l'equip ja pot veure el canvi al remot?**

??? success "Resposta"
    **No.** El commit és local. Encara cal enviar-lo amb `git push`.