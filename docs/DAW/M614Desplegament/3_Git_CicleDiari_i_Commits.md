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
