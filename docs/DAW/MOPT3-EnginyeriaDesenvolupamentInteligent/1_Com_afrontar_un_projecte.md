# Bloc 1: Com afrontar un projecte

## Objectiu del bloc

Donar a l'alumnat una metodologia clara per abordar projectes de desenvolupament amb criteri professional.

> **Idea clau**
> Un projecte ben resolt no comença programant: comença entenent què s'ha de construir i en quin ordre.

---

## 1. Llegir i entendre els requisits

Abans de crear cap fitxer, cal entendre:

- què ha de fer el producte,
- quines limitacions té,
- quin és el criteri d'acceptació.

### Pràctica recomanada

1. Separar requisits funcionals (què fa el sistema).
2. Separar requisits no funcionals (rendiment, usabilitat, seguretat, mantenibilitat).
3. Detectar ambigüitats i formular preguntes concretes.



---

## 2. Dividir el problema

Un projecte complex s'ha de dividir en parts petites i verificables.

### Estratègia

- transformar requisits en tasques: convertir allò que ha de fer el projecte en accions petites, clares i realitzables.
- definir dependències: identificar quines tasques necessiten que una altra estigui acabada abans de poder començar.
- ordenar per valor i risc: decidir què convé fer primer. Es prioritzen les funcionalitats més importants per al projecte i també aquelles que presenten més dificultat o incertesa, per detectar els problemes com més aviat millor.

### Patró útil de descomposició

1. Interfície (HTML/CSS).
2. Lògica del joc (JavaScript).
3. Gestió d'estat.
4. Validació i proves.

---

## 3. Fer primer una versió mínima (MVP)

L'MVP és la versió més simple que ja resol l'objectiu principal.

### Criteri per definir MVP

- una funcionalitat nuclear completada,
- flux bàsic operatiu d'inici a fi,
- sense refinaments avançats.

Exemple en un joc web:

- una pantalla inicial;
- una partida que es pugui jugar de principi a fi;
- un criteri clar que determini quan acaba la partida (guanyar, perdre, arribar a una puntuació, esgotar el temps, etc.).

En aquesta primera versió no calen menús complexos ni animacions. L'objectiu és tenir un producte que funcioni i que es pugui provar.

---

## 4. Afegir funcionalitats per iteracions

Un cop l'MVP funciona, s'afegeixen millores de forma incremental.

### Mètode d'iteració

1. Triar una funcionalitat.
2. Implementar-la.
3. Provar regressions; Provar que no trenca funcionalitats existents.
4. Integrar i documentar canvi.

### Bones pràctiques

- canvis petits i freqüents,
- commits descriptius,
- validació contínua del comportament existent.


---

## 5. Saber quan parar i refactoritzar

Refactoritzar és millorar estructura interna sense canviar comportament extern.

### Senyals clars que cal refactoritzar

- codi duplicat,
- funcions massa llargues,
- noms poc expressius,
- dependències difícils de mantenir,
- augment de bugs en canvis petits.

### Regla docent

Si el cost de seguir afegint funcionalitats és més alt que ordenar el codi, toca refactoritzar.


---

## 6. Checklist ràpid d'aplicació

- He llegit i prioritzat requisits abans de codificar.
- He descompost el problema en tasques petites.
- Tinc una versió mínima funcional.
- Afegeixo millores per iteracions controlades.
- Verifico que no trenqui funcionalitats anteriors.
- Detecto moments de refactorització i els justifico.

---
<!-- 
## 7. Recursos oficials de consulta

- [Atlassian - Agile project management](https://www.atlassian.com/agile/project-management)
- [Scrum Guides - The Scrum Guide](https://scrumguides.org/)
- [MDN Web Docs - Client-side web development](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core)
- [Git - Reference documentation](https://git-scm.com/docs)
- [Conventional Commits - Specification](https://www.conventionalcommits.org/en/v1.0.0/)
- [Refactoring Guru - Refactoring catalog](https://refactoring.guru/refactoring)
- [Google Testing Blog - Test sizes and practical testing](https://testing.googleblog.com/2010/12/test-sizes.html)

---
-->
## 7. Resum del bloc

Aquest bloc defineix una metodologia professional per afrontar projectes: entendre requisits, dividir bé el problema, construir un MVP, iterar amb control i refactoritzar quan toca. Aquesta seqüència redueix errors, millora qualitat i facilita el treball en equip.
