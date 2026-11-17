# Bloc 4. Tasques petites i criteris d'acceptació

Una història pot ser massa gran per completar-la d'una sola vegada. L'equip la pot descompondre en tasques petites, mantenint visible quin valor d'usuari es vol obtenir.

## De la història a les tasques

Història:

> Com a estudiant, vull reservar una sala lliure per assegurar-me que la tindré disponible.

Tasques possibles:

1. Acordar i documentar les regles de franges horàries.
2. Crear el model de dades d'una reserva.
3. Implementar la comprovació que evita reserves superposades.
4. Crear l'acció de confirmar una reserva.
5. Construir el formulari per seleccionar sala i franja.
6. Mostrar confirmació o explicar per què no s'ha pogut reservar.
7. Provar el cas correcte i el conflicte de reserva.

Les tasques poden ser tècniques, de disseny, de recerca o de verificació. L'equip decideix com organitzar-les. Si només completa una tasca de base de dades però l'usuari encara no pot reservar, la història no està acabada.

## Què vol dir «petita»?

Una tasca petita:

- té un resultat concret que es pot revisar;
- és prou acotada perquè l'equip pugui avançar sense grans incògnites;
- es pot provar o inspeccionar;
- no queda bloquejada esperant una fase llunyana de la mateixa funcionalitat.

No hi ha una mida universal en hores. Si una tasca sembla massa gran, concreta el resultat o divideix-la. No fragmentis tant que cada tasca sigui només un gest sense resultat verificable.

## Criteris d'acceptació

Els criteris d'acceptació defineixen comportaments o resultats observables que han de ser certs perquè una història sigui acceptable. Han d'ajudar l'equip i el client a entendre quan la funcionalitat compleix la necessitat.

Exemple per a la història de reserva:

1. Una persona amb sessió iniciada pot seleccionar una sala i una franja disponible.
2. Si la sala continua lliure, el sistema desa la reserva i mostra una confirmació amb sala, data i hora.
3. Si la franja ja està ocupada, el sistema no desa una segona reserva i informa del conflicte.
4. Una persona no pot reservar una sala en nom d'un altre usuari sense autorització.

Els criteris descriuen què ha de passar, no com s'ha de programar. «Crear la taula `reservations`» és una tasca tècnica, no un criteri d'acceptació.

## Format Given / When / Then

Per a casos concrets, podem expressar un criteri en forma d'escenari:

```text
Given (Donat): una sala està lliure entre les 10.00 i les 11.00
When (Quan): l'estudiant confirma una reserva per a aquella franja
Then (Aleshores): la reserva queda desada i es mostra la confirmació
```

Escenari de conflicte:

```text
Given (Donat): la sala ja té una reserva entre les 10.00 i les 11.00
When (Quan): l'estudiant intenta reservar-la en la mateixa franja
Then (Aleshores): el sistema no crea la reserva i informa que la sala ja no està disponible
```

Aquest format ve de pràctiques d'especificació per exemples; és una opció útil, no un requisit obligatori per a totes les històries.

## Criteris d'acceptació i Definition of Done

Són relacionats, però responen preguntes diferents:

| Element | Pregunta | Abast |
|---|---|---|
| Criteris d'acceptació | Aquesta funcionalitat concreta fa el que s'ha acordat? | Una història o element de backlog. |
| Definition of Done | El treball compleix el nivell de qualitat acordat per considerar-lo part de l'increment? | Comú a tot l'increment del producte. |

Una Definition of Done d'exemple podria exigir que el codi estigui integrat, que les proves acordades passin, que no hi hagi errors bloquejants i que la documentació necessària estigui actualitzada. L'equip l'adapta al producte i als seus compromisos de qualitat.

## Una història està preparada per treballar-hi?

Abans de començar a desenvolupar l'equip hauria de poder explicar:

- qui obté valor i quin és l'objectiu;
- quines regles i exemples són coneguts;
- quins criteris permeten comprovar el resultat;
- quines dependències o preguntes pendents hi ha;
- si l'abast és prou petit per intentar completar-lo dins del Sprint.

Això no és una porta d'aprovació rígida ni una checklist universal. És una conversa per fer visibles les incògnites abans que es converteixin en sorpreses.
