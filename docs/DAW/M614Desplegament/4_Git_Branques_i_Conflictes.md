# Bloc 4. Treballar amb branques i integrar canvis

**Pregunta clau:** com faig una millora sense alterar la versió principal mentre hi treballo?

Parteix de `main` amb els canvis anteriors registrats i el directori de treball net:

```bash
git switch main    
git switch -c millora-menu
```

o

```bash
git checkout main    
git checkout -b millora-menu
```

Modifica el menú d'`index.html`, comprova que funciona i registra la millora:

```bash
git add index.html
git commit -m "Millora el menú de navegació"
git switch main
git merge millora-menu
```

`switch` canvia de branca; `switch -c` crea una branca i s'hi situa. `merge` integra la branca indicada **a la branca on ets**. En aquest exemple, integrem `millora-menu` a `main`.

La fusió crea un commit de integració si cal, i la branca original continua existent. Si el projecte té un historial lineal, també es poden fer rebase, però això reescriu la història i s'ha d'usar amb precaució en branques compartides.

Un conflicte apareix quan Git no pot combinar automàticament els canvis, per exemple perquè dues branques han modificat la mateixa línia de manera incompatible. No significa que s'hagi perdut la feina.

1. Executa `git status` per identificar els fitxers en conflicte.
2. Obre'ls i resol el contingut marcat amb `<<<<<<<`, `=======` i `>>>>>>>`.
3. Elimina els marcadors, desa el resultat correcte i comprova que funciona.
4. Executa `git add FITXER_RESOLT` i `git commit` per acabar la integració.

Si necessites cancel·lar una integració en conflicte, utilitza `git merge --abort`. Començar amb el directori net facilita tornar a l'estat anterior.


