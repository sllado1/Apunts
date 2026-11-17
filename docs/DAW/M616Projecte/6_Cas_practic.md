# Bloc 6. Cas pràctic: bicicletes i incidències

En aquest projecte farem una aplicació per gestionar el manteniment d'una flota de bicicletes. Les dades de les bicicletes venen de **La Volteta**, una altra aplicació.

En aquest exercici planificarem dues tasques i veurem per què una depèn de l'altra. Després escriurem criteris d'acceptació per saber si les tasques funcionen.

> Ara només planifiquem la feina. No cal programar-la encara.

## Primer: quina feina ha de fer l'aplicació?

Una **funcionalitat** és una cosa que l'aplicació permet fer a una persona.

En aquest exemple n'hi ha dues:

| Funcionalitat | Qui la fa servir? | Què vol aconseguir? |
|---|---|---|
| **F-01. Sincronitzar bicicletes** | Supervisor | Tenir a l'aplicació les dades actualitzades de les bicicletes de La Volteta. |
| **F-02. Registrar una incidència** | Supervisor | Registrar que una bicicleta està espatllada i enviar-la al taller. |

Una funcionalitat pot necessitar diverses tasques. Aquí ens centrarem en una tasca de cada funcionalitat.

## Segon: quines tasques farem?

### Tasca 1 — Importar les bicicletes

**Funcionalitat:** F-01, sincronitzar bicicletes.  
**Què farem:** llegirem les dades de La Volteta i les desarem a la base de dades local.

**Abans de començar, necessitem:** accés a l'API de La Volteta i un lloc on desar les bicicletes.

**La tasca està acabada quan:** les bicicletes noves s'han desat, les dades d'origen s'han actualitzat i no s'han creat duplicats.

**Criteris d'acceptació:**

- Si La Volteta envia una bicicleta que encara no tenim, apareix a la base de dades local.
- Si tornem a importar la mateixa bicicleta, no se'n crea una còpia.
- Si La Volteta ha canviat les dades d'una bicicleta, s'actualitzen les dades d'origen i es conserven les notes pròpies del taller.

### Tasca 2 — Registrar una incidència

**Funcionalitat:** F-02, registrar una incidència.  
**Què farem:** permetrem que el supervisor registri una incidència per a una bicicleta que La Volteta indica com a espatllada.

**Abans de començar, necessitem:** que la bicicleta ja estigui desada localment (Tasca 1) i poder consultar quines bicicletes estan espatllades.

**La tasca està acabada quan:** el supervisor pot registrar la incidència, aquesta queda relacionada amb la bicicleta i no es duplica.

**Criteris d'acceptació:**

- Si el supervisor registra una avaria d'una bicicleta que encara no té cap incidència, es crea una incidència pendent relacionada amb aquella bicicleta.
- Si la mateixa avaria ja s'havia registrat, el sistema no en crea una altra.

> **Una pregunta per resoldre:** com sabem que dues notificacions de La Volteta són la mateixa avaria? Reviseu si l'API dona un identificador. Si no, anoteu les opcions i pregunteu quin criteri s'ha d'utilitzar.

## Per què la Tasca 2 depèn de la Tasca 1?

La incidència ha d'estar relacionada amb una bicicleta. Si encara no hem importat la bicicleta, no tenim el registre local al qual vincular-la.

```text
La Volteta ──→ Tasca 1: importar bicicleta ──→ Tasca 2: registrar incidència
                    desar-la localment              vincular-la a la bicicleta
```

Alguna feina es pot començar abans. Per exemple, podem llegir la documentació de l'API mentre preparem la base de dades. Però no podem completar la Tasca 2 fins que la bicicleta existeixi localment.

## Una tasca més endavant: el tècnic agafa la reparació

Quan la incidència ja existeix, un tècnic pot autoassignar-se la reparació si està pendent i encara no té cap tècnic assignat. Aquesta feina depèn del registre de la incidència i de tenir usuaris i permisos configurats.

```text
Tasca 1: importar bicicleta
              ↓
Tasca 2: registrar incidència
              ↓
Més endavant: el tècnic s'autoassigna la reparació
```

## Què escrivim a GitHub?

Cada tasca es pot crear com una issue al repositori. La descripció ha de permetre entendre la feina sense haver de llegir tota la conversa de l'equip.

Exemple per a la Tasca 2:

```text
Títol: Registrar una incidència per a una bicicleta espatllada

Funcionalitat: F-02. Registrar una incidència.
Descripció: el supervisor pot registrar una avaria i vincular-la a la bicicleta local.
Depèn de: Tasca 1 (la bicicleta ha d'estar desada localment).
Comprovarem que: es crea una incidència pendent i no se'n crea una còpia si ja existeix.
```

Al GitHub Project, enllaceu la Tasca 2 amb la Tasca 1 i actualitzeu-ne l'estat mentre treballeu.

## Criteris d'acceptació i comprovació de la feina

Els criteris d'acceptació expliquen com ha de funcionar una funcionalitat vista des de l'usuari. Per a una tasca tècnica petita, pot ser suficient escriure una comprovació concreta.

Per exemple:

- **Tasca funcional:** «El supervisor pot registrar una avaria». Criteri: «Quan registra una avaria d'una bicicleta importada, es crea una incidència pendent vinculada a aquella bicicleta».
- **Tasca tècnica:** «Llegir l'endpoint de bicicletes». Comprovació: «Hem desat a la issue l'adreça de l'endpoint, els camps que retorna i un exemple de resposta».

No cal escriure criteris llargs per a cada pas tècnic, però totes les tasques han de tenir una manera clara de comprovar que s'han acabat.

## Ara ho feu vosaltres

1. Llegiu l'enunciat i escriviu amb les vostres paraules les funcionalitats F-01 i F-02.
2. Creeu dues issues de GitHub: una per a la Tasca 1 i una per a la Tasca 2.
3. Indiqueu a cada issue què cal tenir abans de començar.
4. Escriviu criteris d'acceptació per a les dues tasques funcionals.
5. Enllaceu les issues perquè es vegi que la Tasca 2 depèn de la Tasca 1.
6. Anoteu els dubtes sobre l'API o les incidències que necessiteu aclarir amb el professorat.

## Com es relaciona això amb Scrum?

Les dues tasques es poden posar al **Product Backlog** i ordenar segons el valor i les dependències. Quan l'equip estigui preparat, pot seleccionar feina per a un Sprint. Un objectiu possible seria:

> «El supervisor pot importar bicicletes de La Volteta i registrar una incidència per a una bicicleta espatllada.»

Si la Tasca 1 encara no està acabada, l'equip ha de tenir-ho en compte abans de comprometre's amb la Tasca 2.
