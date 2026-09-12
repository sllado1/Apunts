# Bloc 5. Compartir codi i col·laborar amb un remot

**Pregunta clau:** com envio la meva feina i incorporo la dels companys?

Si has començat amb `git init`, crea un repositori buit a la plataforma escollida, sense README ni altres fitxers, i connecta'l després del primer commit:

```bash
git remote add origin URL_DEL_REPOSITORI
git push -u origin main
```

>ULL: `origin` és el nom habitual del remot principal, però pots triar-ne un altre si ho decides. El nom no afecta la funcionalitat, només la referència local que usem per parlar amb el repositori.

Si has fet `git clone`, el remot `origin` ja està configurat. Pots consultar-lo amb `git remote -v`. Per enviar canvis necessitaràs permisos i l'autenticació que requereixi la plataforma.

Per treballar en equip, parteix d'un directori net i actualitza `main` abans de crear la branca:

```bash
git switch main
git pull --ff-only
git switch -c afegeix-contacte
```

Fes la millora i els commits corresponents. Després publica la branca:

```bash
git push -u origin afegeix-contacte
```

Obre una **pull request** o **merge request** a la plataforma: és una proposta per revisar i integrar els canvis a `main`. Explica què has canviat i com ho has comprovat. Un company revisa el codi abans de la integració. Després d'integrar-la, torna a `main` i executa `git pull --ff-only`.

## Rebase i col·laboració: quan convé i quan no

El `rebase` és útil perquè permet deixar el teu historial “lineal” i actualitzat. Però també té una conseqüència important: reescriu el historial de commits.

### Visió visual

Sense rebase, el flux és com una fusió de línies de temps:

```text
A --- B --- C   main
     \ 
      D --- E   branca de treball
```

El `merge` conserva totes dues línies i crea un punt de fusió:

```text
A --- B --- C -------- M
     \             /
      D --- E -----
```

Amb `rebase`, Git intenta “reaplicar” els teus commits sobre la nova base:

```text
A --- B --- C --- D' --- E'
```

Això fa que els commits `D` i `E` siguin diferents, ja que se'ls ha recreat. Per tant, el seu identificador (`sha`) canvia.

### Per què no es recomana gaire quan col·labores amb altres persones?

Perquè el rebase reescriu la història compartida. Si altres companys ja han treballat amb els teus commits i els han basat en ells, canviar-los pot provocar que:

- la línia de temps no coincideixi amb la dels altres,
- els commits apareguin duplicats o conflictius,
- la feina dels companys quedin “desalineada” amb el teu historial.

En resum: el rebase és útil en branques privades o no compartides, però quan el teu historial ja és compartit, cal usar-lo amb prudència.

### Regla pràctica

- `git rebase` és recomanable quan la branca és personal o encara no s’ha publicat.
- Evita rebase sobre commits que ja han estat enviats a un remot i que altres persones poden haver utilitzat.
- Si els commits ja són compartits, és més segur fer `git pull` (o `git pull --rebase` si saps el que estàs fent i l’equip ho accepta).

En projectes col·laboratius, una bona norma és:

> No reescriguis la història d’una branca que ja s’ha compartit amb el grup sense avisar i coordinar-ho.

- `git fetch` descarrega informació i commits del remot sense integrar-los a la branca actual.
- `git pull --ff-only` descarrega i actualitza la branca només si pot avançar sense crear un commit de fusió. Si les històries han divergit, s'atura: revisa la situació abans de continuar.
- `git pull` (sense `--ff-only`) pot fer un merge i crear un commit de fusió si la branca local i el remot no estan alineats.
- `git push` envia commits locals al remot. Si el remot té canvis que falten localment, l'enviament pot ser rebutjat; cal incorporar-los i resoldre els conflictes abans de tornar-ho a provar.


