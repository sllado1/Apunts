# Bloc 1. Entendre el client i definir el problema

Abans de proposar pantalles o començar a programar, cal entendre qui necessita el producte, quin problema té i com sabrem si l'hem ajudat. Una petició inicial és informació per investigar, no necessàriament una especificació completa.

## Petició inicial

Una escola ens diu:

> «Volem una aplicació per reservar les sales d'estudi. Ara ho fem amb una llibreta i sovint dues persones es presenten a la mateixa hora.»

Aquesta frase apunta a un problema: els conflictes de reserva. Encara no determina totes les funcionalitats. Per exemple, no sabem qui pot reservar, amb quina antelació, quant dura una reserva ni qui pot cancel·lar-la.

## Preguntes per descobrir necessitats

En una conversa amb el client i les persones usuàries, investiguem:

- **Persones:** qui farà servir el sistema? Hi ha perfils diferents, com estudiants i administradors?
- **Objectiu:** què vol aconseguir cada perfil?
- **Situació actual:** com es resol avui el problema? On es produeixen errors o esperes?
- **Regles:** quines condicions ha de complir una reserva?
- **Excepcions:** què passa si una sala està ocupada, si l'usuari cancel·la o si no es presenta?
- **Prioritat:** quina és la funcionalitat mínima que ja aportaria valor?
- **Restriccions:** hi ha requisits d'accessibilitat, privacitat, dispositius o terminis?
- **Èxit:** quina evidència mostrarà que la solució funciona?

No cal preguntar-ho tot en una única reunió. Es poden fer entrevistes, observar el procés actual, revisar documents i ensenyar prototips senzills per contrastar hipòtesis.

## Distingir necessitat, solució i restricció

| Tipus d'informació | Exemple | Què ens diu |
|---|---|---|
| Necessitat | «Volem evitar que dues persones reservin la mateixa sala a la mateixa hora.» | Quin problema volem resoldre. |
| Solució proposada | «Posem un calendari amb les hores lliures.» | Una idea de com es podria resoldre. Cal validar-la. |
| Regla de negoci | «Una persona pot tenir una sola reserva activa al dia.» | Una condició que el sistema ha de respectar. |
| Restricció | «S'ha de poder fer servir des del mòbil.» | Un límit o requisit de context. |

No confonguis una solució proposada amb la necessitat. Si el client demana «un botó verd», pregunta quin resultat espera; potser el problema és que les persones no troben com confirmar una reserva.

## Abast i Product Goal

El **Product Goal** expressa un objectiu de producte que orienta el treball. Per a l'exemple:

> «Permetre que l'alumnat consulti la disponibilitat i reservi una sala sense conflictes.»

Per mantenir l'abast manejable, acordem què entra a la primera versió:

**Inclou:** veure les sales i la seva disponibilitat, crear una reserva, consultar les reserves pròpies i cancel·lar-les.

**Deixem per més endavant:** pagaments, notificacions push, reserves recurrents i estadístiques avançades.

La llista «més endavant» no és una promesa automàtica. És material que es pot reconsiderar quan tinguem més informació.

## Resultat d'aquesta fase

Abans de passar a descriure funcionalitats, l'equip hauria de tenir una comprensió compartida de:

1. quin problema intenta resoldre;
2. qui hi està implicat;
3. quines regles i restriccions coneixem;
4. què seria un primer resultat útil;
5. quines preguntes continuen obertes.

Les preguntes obertes s'han de fer visibles. No les convertim en requisits inventats: les anotem i busquem qui les pot respondre.
