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
  src/
    php/
      Controllers/
      Services/
      Repositories/
      Views/
  config/
  tests/
  docs/
  .gitignore
  README.md
```

Criteri:

- `public/`: únic punt d'entrada web.
- `assets/`: recursos estàtics (CSS, JS, imatges, tipografies).
- `src/`: lògica de negoci i codi d'aplicació.
- `config/`: configuracions d'entorn i constants.
- `tests/`: proves automatitzades.
- `docs/`: documentació tècnica i funcional.

---

## 2. Noms de fitxers

Els noms han de ser coherents, predictibles i llegibles.

### Recomanacions pràctiques

- usar minúscules en fitxers públics (`app.js`, `styles.css`, `home.php`),
- usar guions o patró coherent (`user-profile.php` o `user_profile.php`),
- evitar espais, accents i caràcters especials,
- fer noms descriptius del contingut,
- aplicar convencions consistents en classes PHP (`PascalCase`) i mètodes (`camelCase`).

### Exemples

- Correcte: `game-engine.js`, `score-service.php`, `main.css`.
- Incorrecte: `Arxiu Final Definitiu 2.php`, `estilsNOU!!.css`.

---

## 3. On posar HTML, PHP, CSS i JS

### HTML/PHP

- Si el projecte és PHP, el punt d'entrada principal (`index.php`) ha d'estar a `public/`.
- Les vistes o plantilles es poden gestionar dins `src/php/Views/`.

### CSS

- Fulls d'estil globals a `public/assets/css/`.
- Si cal, separar per responsabilitat: `base.css`, `layout.css`, `components.css`.

### JavaScript

- Scripts de client a `public/assets/js/`.
- Separar per mòduls: `game.js`, `ui.js`, `storage.js`.

### Recursos multimèdia

- Imatges a `public/assets/img/`.
- Àudios a `public/assets/audio/` (si n'hi ha).
- Tipografies a `public/assets/fonts/`.

---

## 4. Recursos i dependències

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
- El projecte es pot executar sense fitxers "fantasma".

---

## 5. Errors habituals d'organització

- barrejar lògica PHP amb assets estàtics sense criteri,
- tenir fitxers duplicats amb noms similars,
- deixar recursos dispersos fora de l'estructura principal,
- no separar codi d'aplicació i codi públic,
- canviar convencions de noms a mig projecte.

---

## 6. Activitat guiada (20-30 minuts)

Objectiu:

- reorganitzar un projecte desordenat i justificar les decisions.

Tasca:

1. Reubicar fitxers segons una estructura proposada.
2. Normalitzar noms de fitxers i carpetes.
3. Corregir rutes trencades en HTML/PHP/CSS/JS.
4. Documentar 5 decisions d'organització amb argument tècnic.

Evidència de sortida:

- arbre final de carpetes,
- llista de canvis realitzats,
- justificació breu de qualitat i mantenibilitat.

---

## 7. Recursos oficials de consulta

- [MDN - Structuring the web with HTML](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content)
- [MDN - Client-side web development](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core)
- [PHP Manual - Introduction](https://www.php.net/manual/en/intro-whatis.php)
- [PHP Standards Recommendations (PSR)](https://www.php-fig.org/psr/)
- [Google Developers - JavaScript style guide](https://google.github.io/styleguide/jsguide.html)
- [Git - Documentation](https://git-scm.com/docs)

---

## 8. Resum del bloc

Una organització sòlida del projecte és una decisió d'enginyeria, no d'estètica. Quan el codi està ben estructurat, amb noms coherents i recursos ben ubicats, el producte és més mantenible, més robust i més professional.
