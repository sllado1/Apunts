# Bloc 3. El cicle diari: revisar, preparar i registrar

**Pregunta clau:** com guardo una versió que després pugui entendre?

Després de crear o modificar `index.html`:

```bash
git status
git diff
git add index.html .gitignore
git diff --staged
git commit -m "Afegeix la pàgina inicial i les exclusions de Git"
git log --oneline
```

| Ordre | Què ens permet comprovar o fer? |
| --- | --- |
| `git status` | Saber la branca actual i quins fitxers estan pendents o preparats. |
| `git diff` | Revisar els canvis no preparats de fitxers que Git ja segueix. |
| `git add FITXER` | Preparar el contingut actual d'un fitxer per al proper commit. |
| `git diff --staged` | Revisar exactament els canvis que entraran al commit. |
| `git commit -m "Missatge"` | Registrar el contingut preparat a l'historial local. |
| `git log --oneline` | Consultar un resum dels commits. |

Els fitxers nous no seguits apareixen a `status`, però el seu contingut no apareix a `git diff` perquè encara no formen part de l'historial. Un cop preparats amb `git add`, els pots revisar amb `git diff --staged`.

Si tornes a editar un fitxer després de `git add`, has de preparar-lo de nou per incloure també els últims canvis. Fes commits petits amb missatges concrets, com ara `Update the menu link`, i evita missatges com `canvis` o `final`.

!!! tip "Canviar només les majúscules i minúscules del nom d'un fitxer"

    A Windows i en molts sistemes macOS, canviar `Index.html` per `index.html` des de l'explorador pot passar desapercebut per a Git. Per registrar el canvi d'un fitxer que Git ja segueix, fes servir `git mv` en dos passos, amb un nom temporal que no existeixi:

    ```bash
    git mv Index.html temporal-index.html
    git mv temporal-index.html index.html
    git status
    git diff --staged --summary
    git commit -m "Canvia Index.html a index.html"
    ```

    `git mv` ja deixa el canvi preparat per al commit; no cal fer `git add` per al canvi de nom. Per passar de minúscules a majúscules, segueix el mateix procediment amb el nom final desitjat. Revisa també els enllaços i les referències al fitxer: en un servidor Linux, habitualment `Index.html` i `index.html` són noms diferents. Si actualitzes aquestes referències, prepara els fitxers modificats amb `git add` abans del commit.

**Pràctica:** fes dos commits amb millores diferents. Modifica un fitxer després d'haver-lo preparat amb `git add` i compara la sortida de `git diff` amb la de `git diff --staged`.

## Resum presentació

### Diapositiva 1. El cicle diari

```text
REVISAR → PREPARAR → COMPROVAR → REGISTRAR → CONSULTAR
status    add        diff        commit      log
diff                --staged                 --oneline
```

**Abans de fer un commit, revisem què hi entrarà.**

---

### Diapositiva 2. Què he canviat?

| Ordre | Què mostra? |
| --- | --- |
| `git status` | Branca actual, fitxers nous, modificats i preparats. |
| `git diff` | Canvis dels fitxers seguits que encara no hem preparat. |

**Si creem un fitxer nou, Git encara no el segueix.** `git status` en mostra el nom com a **no seguit** (*untracked*), però `git diff` no en mostra el contingut: aquesta ordre compara el directori de treball amb el contingut preparat, i el fitxer nou encara no és a l'àrea de staging.

Per exemple, després de crear `contacte.html`:

```bash
git status                     # Mostra contacte.html com a no seguit
git diff                       # No mostra el contingut del fitxer nou
git add contacte.html          # Prepara el fitxer
git diff --staged              # Mostra tot el contingut com una incorporació nova
```

**Per revisar un fitxer nou abans del commit: primer `git add`, després `git diff --staged`.**

---

### Diapositiva 3. Què entrarà al commit?

```bash
git add index.html
git diff --staged
```

- `git add` prepara el **contingut actual** del fitxer.
- `git diff --staged` mostra els canvis preparats respecte de l'últim commit.
- Podem seleccionar fitxers concrets per agrupar un canvi coherent.

**Si tornem a editar el fitxer, cal tornar a fer `git add` per incloure la nova edició.**

---

### Diapositiva 4. Dos canvis, dues comparacions

1. Canviem el títol d'`index.html` i fem `git add index.html`.
2. Després canviem també el text del botó, sense tornar a fer `git add`.

| Ordre | Què veurem? |
| --- | --- |
| `git diff --staged` | El canvi de títol que hem preparat. |
| `git diff` | El canvi de text del botó que encara no hem preparat. |

**Si fem el commit ara, hi entra el canvi de títol. El del botó queda pendent.**

---

### Diapositiva 5. Commits que s'entenen

```bash
git commit -m "Corregeix l'enllaç del menú"
git log --oneline
```

- Fem commits **petits i coherents**, amb una finalitat clara.
- El missatge explica **què hem canviat**.
- `git log --oneline` mostra l'identificador abreujat i el missatge de cada commit.

| Missatge poc útil | Missatge concret |
| --- | --- |
| `canvis` | `Afegeix el formulari de contacte` |
| `final` | `Corregeix l'enllaç del menú` |

**El commit guarda una versió local; per compartir-la al remot cal fer `git push`.**

---

### Diapositiva 6. Canviar majúscules i minúscules

A Windows i en molts sistemes macOS, Git pot no detectar un canvi de nom fet des de l'explorador com `Index.html` → `index.html`.

Fem servir un nom temporal que no existeixi:

```bash
git mv Index.html temporal-index.html
git mv temporal-index.html index.html
git diff --staged --summary
git commit -m "Canvia Index.html a index.html"
```

- `git mv` **ja prepara el canvi de nom**.
- Revisem els enllaços: en un servidor Linux, habitualment aquests noms són diferents.
- Si corregim referències en altres fitxers, també les preparem amb `git add`.

---

### Diapositiva 7. Exemple i pregunta final

Després de corregir un enllaç d'un `index.html` ja seguit per Git:

```bash
git status
git diff
git add index.html
git diff --staged
git commit -m "Corregeix l'enllaç de contacte"
git log --oneline
```

**He fet `git add` i després he tornat a editar el fitxer. Entrarà tot al commit?**

??? success "Resposta"
    **No.** Hi entra el contingut preparat amb l'últim `git add`. Per incloure les edicions posteriors, cal tornar a preparar el fitxer i revisar-lo amb `git diff --staged`.