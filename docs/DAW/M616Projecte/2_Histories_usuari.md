# Bloc 2. Històries d'usuari i Product Backlog

Una història d'usuari descriu una capacitat del producte des del punt de vista d'una persona que n'obté valor. Ajuda a conversar sobre una necessitat; no és una especificació tècnica completa ni una tasca de programació.

## La forma habitual

```text
Com a [tipus de persona usuària],
vull [capacitat o objectiu],
per [benefici o motiu].
```

Exemple:

> Com a estudiant, vull veure quines sales estan lliures en una franja horària, per triar-ne una abans de demanar una reserva.

- **Qui:** estudiant.
- **Què vol fer:** veure sales lliures en una franja.
- **Per què:** poder escollir una sala disponible.

El «per què» permet prioritzar amb sentit. Si una funcionalitat no resol una necessitat identificable, hem de revisar per què la volem construir.

## La història inicia una conversa

Una història no resol tots els detalls. Per exemple, cal aclarir què vol dir «lliure»: la sala no té cap reserva que se superposi amb la franja? Els horaris estan limitats? Què es mostra si no hi ha sales?

Aquestes converses generen **criteris d'acceptació**, exemples i preguntes. No cal encabir totes les regles dins de la frase de la història.

## Història, requisit, tasca i criteri: no són el mateix

| Element | Pregunta que respon | Exemple |
|---|---|---|
| Necessitat | Quin problema hi ha? | Evitar que dues persones ocupin la mateixa sala alhora. |
| Història d'usuari | Qui necessita fer què i per què? | Com a estudiant, vull reservar una sala lliure per assegurar-me que la tindré disponible. |
| Criteri d'acceptació | Com comprovem que la història es comporta correctament? | Si la sala té una reserva superposada, el sistema no permet confirmar-ne una altra. |
| Tasca | Quina feina concreta ha de fer l'equip? | Afegir una comprovació de solapament a la creació de reserves. |

La història representa valor per a una persona. Les tasques descriuen feina necessària per lliurar-lo; els criteris d'acceptació indiquen quins resultats observables són acceptables.

## Històries petites i valuoses

Una història és útil quan l'equip la pot entendre, estimar i completar en un període curt, mantenint un resultat que té sentit per a l'usuari. Si és massa gran, es pot dividir per resultats o escenaris d'usuari.

Exemple de funcionalitat gran: «Gestionar reserves».

Possibles històries més petites:

1. Consultar la disponibilitat de sales.
2. Crear una reserva per a una sala disponible.
3. Consultar les meves reserves.
4. Cancel·lar una reserva pròpia.

Intentem evitar divisions purament tècniques com «crear la taula», «fer l'API» i «maquetar la pantalla» com si cadascuna fos una història. Són tasques possibles dins d'una història; per si soles no necessàriament lliuren valor complet a l'usuari.

## Product Backlog

El **Product Backlog** és una llista ordenada i evolutiva de la feina coneguda que pot millorar el producte. Pot contenir històries, errors, recerca o treball tècnic. No és un contracte tancat: es revisa a mesura que aprenem.

Exemple simplificat:

| Ordre inicial | Element | Motiu de prioritat |
|---:|---|---|
| 1 | Consultar sales disponibles | Sense això, l'usuari no sap què pot reservar. |
| 2 | Crear una reserva | És el resultat central del producte. |
| 3 | Consultar les meves reserves | Permet revisar què s'ha confirmat. |
| 4 | Cancel·lar una reserva | Dona control a l'usuari i allibera una sala. |

L'ordre pot canviar si canvien les necessitats, el risc o el que hem après. La persona responsable de maximitzar el valor del producte és el **Product Owner**; l'equip col·labora per entendre les opcions i la feina.

## La connexió amb els altres materials

- Els comentaris de client i usuaris expliquen d'on surt la història.
- El diagrama de casos d'ús ajuda a veure qui interactua amb el sistema i quins objectius cobreix.
- Els criteris d'acceptació concreten exemples de comportament.
- Les tasques descomponen la feina perquè l'equip pugui construir i comprovar la història.
- Scrum dona el marc per ordenar el backlog, seleccionar feina per a un Sprint i revisar un increment.

No cal crear una història nova per cada oval d'un diagrama. El diagrama i les històries són vistes diferents del mateix producte i s'han de relacionar quan hi ha correspondència.
