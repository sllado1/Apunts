# Bloc 3: Pla de desenvolupament

Aquest bloc ensenya a documentar i planificar abans de construir. Un bon pla redueix errors, facilita el treball en equip i permet prioritzar bé.

---

## 1. Què és un pla de desenvolupament

És un document breu que explica:

- què construirem,
- en quin ordre,
- com validarem cada pas,
- quan una funcionalitat es considera acabada.

> **Idea clau**
> Planificar no és burocràcia: és una manera de garantir qualitat i control del projecte.

---

## 2. Per què fer-lo en Markdown

Markdown és ideal per a plans tècnics perquè és:

- simple d'escriure,
- llegible en text pla,
- compatible amb Git,
- fàcil de versionar i revisar.

### Sintaxi mínima que ha de dominar l'alumnat

```markdown
# Títol principal
## Secció

- punt 1
- punt 2

1. pas 1
2. pas 2

[Enllaç](https://example.com)
```

Documentació oficial:

- [Markdown Guide - Basic Syntax](https://www.markdownguide.org/basic-syntax/)
- [CommonMark Specification](https://spec.commonmark.org/)

---

## 3. Estructura recomanada del document

Plantilla mínima:

```markdown
# Pla de desenvolupament - Nom del projecte

## 1. Objectiu
## 2. Requisits funcionals
## 3. Requisits no funcionals
## 4. MVP (versió mínima viable)
## 5. Fases i tasques
## 6. Criteris d'acceptació
## 7. Riscos i bloquejos
## 8. Seguiment i estat
```

---

## 4. Exemple complet: reproductor de cançons (projecte bàsic)

### 4.1 Objectiu

Construir un reproductor web simple que permeti:

- mostrar una llista de cançons,
- reproduir/pausar,
- passar a cançó següent i anterior,
- mostrar cançó activa.

### 4.2 Requisits funcionals

1. L'usuari pot veure el nom de les cançons.
2. L'usuari pot reproduir i pausar.
3. L'usuari pot canviar de cançó.
4. El sistema marca visualment la cançó actual.

### 4.3 Requisits no funcionals

- Interfície clara i usable en escriptori i mòbil.
- Codi modular i llegible.
- Temps de càrrega raonable.

### 4.4 MVP

Primera versió mínima:

- botó Play/Pause,
- una sola cançó,
- control funcional de reproducció.

### 4.5 Fases i tasques

#### Fase 1 - Base

- estructura HTML,
- estils CSS bàsics,
- reproducció d'un fitxer d'àudio.

#### Fase 2 - Llista

- array de cançons,
- renderitzat de la llista,
- selecció de cançó.

#### Fase 3 - Controls

- següent/anterior,
- estat visual de cançó activa,
- control de temps bàsic.

#### Fase 4 - Qualitat

- neteja de codi,
- validació de rutes,
- proves manuals de regressió.

### 4.6 Criteris d'acceptació

- Play/Pause funciona sense errors.
- Canvi de cançó actualitza àudio i títol.
- No es trenquen funcionalitats existents en afegir una de nova.
- El codi és comprensible per un altre company.

### 4.7 Riscos típics

- rutes incorrectes d'àudio,
- estat desincronitzat entre botons i reproductor,
- duplicació de codi en gestió d'esdeveniments.

### 4.8 Seguiment

Cada sessió ha de deixar:

- què s'ha implementat,
- què falta,
- quin bloqueig hi ha (si n'hi ha),
- següent pas concret.

---

## 5. Exemple curt de fitxer Markdown real

```markdown
# Pla de desenvolupament - Reproductor de cançons

## Objectiu
Crear un reproductor web bàsic amb controls principals.

## MVP
- Reproduir i pausar una cançó
- Mostrar títol de la cançó activa

## Tasques de la setmana
1. Crear estructura HTML
2. Connectar element <audio>
3. Implementar Play/Pause amb JavaScript

## Criteri d'acceptació
Quan faig clic a Play, s'escolta la cançó i el botó canvia a Pause.
```

---

## 6. Checklist ràpid

- El pla està escrit en Markdown i és llegible.
- Hi ha objectiu clar i abast delimitat.
- L'MVP està definit.
- Les tasques estan dividides per fases.
- Cada fase té criteri d'acceptació.
- Es registren riscos i següents passos.

---

## 7. Recursos oficials de consulta

- [Markdown Guide](https://www.markdownguide.org/)
- [CommonMark Spec](https://spec.commonmark.org/)
- [MDN - Introduction to HTML](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content/Basic_HTML_syntax)
- [MDN - CSS basics](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics)
- [MDN - JavaScript first steps](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting)
- [MDN - HTMLMediaElement API](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement)

---

## 8. Resum del bloc

Un pla de desenvolupament en Markdown converteix idees en execució. Si l'alumnat defineix objectiu, MVP, fases i criteris d'acceptació, el projecte avança amb més velocitat i menys improvisació.
