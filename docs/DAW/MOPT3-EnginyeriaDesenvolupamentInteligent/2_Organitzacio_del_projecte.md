# Bloc 2: Organització del projecte

## Objectiu del bloc

Definir una base d'organització clara per a projectes web amb HTML, PHP, CSS i JavaScript que sigui escalable, mantenible i fàcil de treballar en equip.

> **Idea clau**
> Una bona arquitectura de carpetes i noms redueix errors, accelera el desenvolupament i facilita la qualitat del programari.

---

## 1. Estructura de carpetes

Una proposta base per a projectes web acadèmics i professionals:

```text
projecte-web/
  public/
    index.php
    assets/
      css/
      js/
      img/
      fonts/
  .gitignore
  README.md
```

Criteri:

- `public/`: únic punt d'entrada web.
- `assets/`: recursos estàtics (CSS, JS, imatges, tipografies).


---

## 2. Noms de fitxers

Els noms han de ser coherents, predictibles i llegibles.

!!! tip "Ull amb les majúscules i les minúscules"

    Alguns sistemes operatius, com Linux en la configuració habitual, distingeixen les majúscules de les minúscules en els noms de fitxers i carpetes: `Logo.png` i `logo.png` són noms diferents. Escriu les rutes amb les mateixes majúscules i minúscules que el nom real, perquè un enllaç que funciona al teu ordinador podria fallar en desplegar el projecte al servidor.

### Recomanacions pràctiques

- usar minúscules en fitxers públics (`app.js`, `styles.css`, `home.php`),
- usar guions o patró coherent (`user-profile.php` o `user_profile.php`),
- evitar espais, accents i caràcters especials,
- fer noms descriptius del contingut,
- seguir un patró consistent a tot el projecte.
  
### Exemples

- Correcte: `game-engine.js`, `score-service.php`, `main.css`.
- Incorrecte: `Arxiu Final Definitiu 2.php`, `estilsNOU!!.css`.

---

## 3. On posar HTML, PHP, CSS i JS

### HTML/PHP

- Si el projecte és PHP, el punt d'entrada principal (`index.php`) ha d'estar a `public/`.

### CSS

- Fulls d'estil globals a `public/assets/css/`.
- Si cal, separar per responsabilitat: `base.css`, `layout.css`, `components.css`.

### JavaScript

- Scripts de client a `public/assets/js/`.
- Separar per mòduls: `game.js`, `ui.js`, `storage.js`.

### Recursos multimèdia

- Imatges a `public/assets/img/`.
- Àudios a `public/assets/audio/` (si n'hi ha).
- Tipografies a `public/assets/fonts/`. (si n'hi ha)

---
## 3.1. Recursos i dependències

Cal distingir clarament recursos propis de tercers.

### Bones pràctiques

- documentar llibreries externes a `README.md`,
- indicar versió i motiu d'ús,
- evitar dependències innecessàries,
- minimitzar i optimitzar recursos estàtics,
- mantenir rastre de canvis en dependències.

### Checklist ràpid

- Els recursos tenen ubicació clara i estable.
- Les rutes dels assets són coherents en tot el projecte.
- Les dependències externes estan justificades.
- El projecte es pot executar sense fitxers "fantasma". El projecte es pot executar amb els fitxers del repositori i les instruccions de configuració, instal·lació i generació documentades.
- S'han documentat les funcionalitats i dependències del projecte a `README.md`.

---

## 5. Errors habituals d'organització

- desar codi PHP de lògica de negoci en carpetes destinades a CSS, JavaScript o imatges,
- canviar convencions de noms a mig projecte.

---

## 6. Recursos oficials de consulta

- [MDN - Structuring the web with HTML](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content)
- [PHP Standards Recommendations (PSR)](https://www.php-fig.org/psr/)
- [Git - Documentation](https://git-scm.com/docs)

---

## 7. Resum del bloc

Una organització sòlida del projecte és una decisió d'enginyeria, no d'estètica. Quan el codi està ben estructurat, amb noms coherents i recursos ben ubicats, el producte és més mantenible, més robust i més professional.
