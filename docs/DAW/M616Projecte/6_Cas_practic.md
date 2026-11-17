# Bloc 6. Cas pràctic: de la petició al Sprint

Aquest bloc recorre tot el fil amb un exemple. La intenció és veure com les peces es relacionen, no omplir documents per complir un tràmit.

## 1. Petició i necessitat

El client diu:

> «L'alumnat no sap quines sales estan lliures i hi ha reserves duplicades.»

Necessitat acordada: l'alumnat ha de poder consultar disponibilitat i reservar una sala sense conflictes.

## 2. Product Goal i abast inicial

**Product Goal:** permetre que l'alumnat consulti i reservi sales d'estudi sense conflictes.

Per a una primera versió, prioritzem consultar sales, crear una reserva i consultar les reserves pròpies. Notificacions i reserves recurrents queden fora de l'abast inicial.

## 3. Actor i cas d'ús

**Actor:** estudiant.  
**Cas d'ús:** reservar una sala.  
**Precondició:** l'estudiant té sessió iniciada.  
**Resultat:** el sistema confirma una reserva o explica per què no s'ha pogut fer.

Escenari principal: selecciona data i hora, veu les sales lliures, tria una sala, confirma i rep una confirmació.

Excepció: si la sala s'ha reservat mentrestant, el sistema no crea una reserva duplicada i mostra el conflicte.

## 4. Història al Product Backlog

> Com a estudiant, vull reservar una sala lliure per assegurar-me que la tindré disponible.

L'element es relaciona amb el cas d'ús «Reservar una sala». El cas d'ús aporta l'escenari i l'excepció; la història resumeix el valor que ordenem al backlog.

## 5. Criteris d'acceptació

- Es pot seleccionar una sala i una franja que apareixen com a disponibles.
- Si la sala continua lliure en confirmar, la reserva queda desada i es mostra sala, data i hora.
- Si la sala ja té una reserva superposada, no es crea la reserva i es comunica el conflicte.

Exemple en Given / When / Then:

```text
Given: la sala A està lliure de 10.00 a 11.00
When: l'estudiant confirma una reserva per a aquella franja
Then: el sistema desa la reserva i mostra la confirmació
```

## 6. Tasques de l'equip

Durant la planificació, els Developers poden descompondre la història en feina com:

- definir com es representen les franges horàries;
- implementar el servei que comprova solapaments;
- desar la reserva vinculada a l'estudiant;
- crear el formulari de selecció;
- mostrar la confirmació i l'error de conflicte;
- provar el camí correcte i el cas de concurrència.

El Product Owner ajuda a aclarir el valor i les regles. Els Developers decideixen com fer la feina i com dividir-la. Scrum Master dona suport perquè la planificació sigui efectiva i elimina impediments quan sigui possible.

## 7. Selecció per al Sprint

L'equip acorda un Sprint Goal:

> «L'estudiant pot completar una reserva vàlida i rebre una confirmació clara.»

El Product Backlog conté les històries ordenades. A la Sprint Planning, els Developers seleccionen els elements que creuen que poden completar i creen el Sprint Backlog: objectiu, elements seleccionats i pla de treball.

Durant el Sprint, l'equip inspecciona el progrés i adapta el pla. A la Sprint Review, el client prova la reserva i dona feedback. A la Retrospective, l'equip acorda una millora en la manera de treballar.

## Mapa de traçabilitat

| Necessitat del client | Cas d'ús | Història | Criteri d'acceptació | Tasques | Scrum |
|---|---|---|---|---|---|
| Evitar reserves duplicades | Reservar una sala | Com a estudiant, vull reservar una sala lliure... | Una franja ocupada no es pot reservar dues vegades. | Comprovar solapament, desar reserva, mostrar conflicte, provar. | Element del Product Backlog seleccionat cap a un Sprint Goal i un increment. |

## Preguntes de revisió

1. Quina diferència hi ha entre la necessitat i la solució proposada?
2. Per què la història no inclou la llista de tasques tècniques?
3. Quin escenari del cas d'ús es converteix en el criteri de conflicte?
4. Qui decideix com es divideix la feina durant el Sprint?
5. Quina informació nova de la Sprint Review podria fer canviar l'ordre del Product Backlog?
