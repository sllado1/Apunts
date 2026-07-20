# Bloc 1: Fonaments de l'HTML5
## Sintaxi, Estructura i Accessibilitat

---

## 1. Què és l'HTML5?
L'HTML (**HyperText Markup Language**) és la tecnologia que defineix el contingut i l'estructura de qualsevol lloc web [1, 2].
*   **Semàntica:** L'HTML5 introdueix etiquetes que descriuen el significat del contingut de manera que les màquines el puguin entendre, cosa vital per a l'accessibilitat i el SEO [1, 3, 4].
*   **Objectiu:** Millorar la interoperabilitat i oferir funcionalitats estàndard per a multimèdia i aplicacions web [2, 5].

---

## 2. Anatomia d'un Element HTML
La sintaxi es basa en elements que inclouen [6, 7]:
*   **Etiqueta d'obertura:** `<nom_etiqueta>`.
*   **Atributs:** Proporcionen propietats extra (ex: `class`, `id`, `lang`, `href`) [6, 8, 9].
*   **Contingut:** El text o elements niats.
*   **Etiqueta de tancament:** `</nom_etiqueta>`.
*   **Elements buits (void):** No tenen contingut ni tancament (ex: `<img>`, `<br>`) [6, 10].

---

## 3. Estructura Bàsica del Document
Tot document ha de seguir aquesta jerarquia essencial [6, 7, 11]:
1.  **`<!DOCTYPE html>`:** Obligatori per indicar que s'usa l'estàndard HTML5 [2, 6].
2.  **`<html lang="ca">`:** L'element arrel on cal especificar l'idioma per als lectors de pantalla [6, 12, 13].
3.  **`<head>`:** Contenidor de metadades (títol, codificació `charset`, enllaços a CSS) no visibles [6, 7].
4.  **`<body>`:** Conté tot el contingut que l'usuari veurà [6, 7].

---

## 4. Estructura Semàntica Principal
L'HTML5 defineix elements per descriure les zones de la pàgina [14-16]:
*   **`<header>`:** Capçalera amb logos o títols de la secció [16, 17].
*   **`<nav>`:** Bloc de navegació principal [5, 16, 17].
*   **`<main>`:** Contingut principal i únic de la pàgina [16, 18].
*   **`<section>`:** Agrupa contingut relacionat temàticament [16, 19].
*   **`<article>`:** Contingut autònom i independent (notícies, posts) [16, 18, 20].
*   **`<aside>`:** Contingut relacionat de manera indirecta (barres laterals) [16, 18].
*   **`<footer>`:** Peu de pàgina amb info legal o xarxes socials [5, 16, 18].

---

## 5. Els Encapçalaments (`<h1>` - `<h6>`)
S'usen per crear una jerarquia lògica de contingut [14, 21]:
*   **`<h1>`:** Ha de ser únic i representar el tema principal [21, 22].
*   **No saltis nivells:** L'estructura ha de ser seqüencial per no desorientar els usuaris de lectors de pantalla [14, 22].

---

## 6. Accessibilitat Web (Principis WCAG)
L'accessibilitat garanteix que tothom pugui percebre, operar i entendre el web [23, 24]:
1.  **Perceptible:** Info presentada de manera que es pugui detectar pels sentits [24, 25].
2.  **Operable:** La interfície ha de ser navegable, especialment amb teclat [24, 26, 27].
3.  **Comprensible:** El funcionament i la info han de ser clars [24, 28].
4.  **Robust:** Compatible amb diferents navegadors i ajudes tècniques [24, 29].

---

## 7. Bones Pràctiques i Validació
*   **Text alternatiu (`alt`):** Totes les imatges l'han de tenir per descriure el contingut [10, 30].
*   **Etiquetes de formulari (`<label>`):** Associa sempre el text amb el seu `<input>` mitjançant els atributs `for` i `id` [31, 32].
*   **Validació W3C:** Utilitza el validador oficial per corregir errors de sintaxi o anidament [33-35].
