# Bloc 5: Responsive, mobile first, media queries i frameworks

Aquest bloc explica com fer que una interfície funcioni bé en mòbil, tauleta i escriptori, i com decidir quan té sentit usar un framework.

---

## 1. Objectiu del bloc

En acabar aquest bloc, l'alumnat ha de poder:

1. Dissenyar amb enfocament **mobile first**.
2. Aplicar **media queries** amb criteri.
3. Adaptar un layout a diferents amplades de pantalla.
4. Entendre quan un framework ajuda i quan limita.
5. Mantenir la interfície usable en qualsevol dispositiu.

> **Idea clau**
> Responsive no vol dir només que "s'adapta": vol dir que la interfície està pensada per créixer i reorganitzar-se amb criteri.

---

## 2. Què és responsive

Una interfície responsive canvia la seva disposició, dimensions o comportament segons l'espai disponible i les característiques del dispositiu.

Exemples:

- una columna en mòbil i dues en escriptori,
- un menú horitzontal que es converteix en menú plegable,
- imatges i targetes que s'ajusten a l'amplada del contenidor.

---

## 3. Mobile first

Mobile first significa començar pel disseny més petit i després ampliar-lo.

Per què és útil:

- obliga a prioritzar contingut,
- evita layouts massa carregats,
- simplifica les decisions responsive,
- millora la llegibilitat i la usabilitat.

### Exemple mental

1. Primer defineixo què veu l'usuari en mòbil.
2. Després afegeixo espai i components quan hi ha més amplada.
3. Finalment ajusto escriptori i pantalles grans.

---

## 4. Media queries

Les media queries permeten aplicar estils diferents segons l'amplada de la pantalla o altres característiques.

### Exemple bàsic

```css
.layout {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1rem;
}

@media (min-width: 768px) {
  .layout {
    grid-template-columns: 1fr 1fr;
  }
}
```

### Bona pràctica

- escriu primer l'estil base per a mòbil,
- afegeix canvis progressius a partir de punts de tall,
- evita duplicar massa codi dins de moltes media queries.

---

## 5. Punts de tall

Un punt de tall és l'amplada a partir de la qual canvies el comportament visual.

Exemples orientatius:

- mòbil petit: fins a 480 px,
- tauleta: a partir de 768 px,
- escriptori: a partir de 1024 px.

> No cal memoritzar xifres exactes com si fossin sagrades. Cal entendre el canvi de comportament i adaptar-los al projecte.

---

## 6. Responsive en un projecte bàsic

Exemple d'una pantalla de videojoc o reproductor simple:

- en mòbil, la informació es mostra en columna,
- els botons ocupen tota l'amplada útil,
- la informació secundària queda sota la principal,
- en escriptori, controls i contingut poden anar en dues columnes.

### Criteri d'aula

Abans d'aplicar codi, l'alumnat hauria de poder dibuixar:

- la versió mòbil,
- la versió tauleta,
- la versió escriptori.

---

## 7. Frameworks: quan ajuden i quan no

Un framework pot accelerar el desenvolupament, però no substitueix el criteri de disseny.

### Quan ajuden

- prototips ràpids,
- projectes amb temps limitat,
- components repetitius,
- coherència visual inicial.

### Quan poden limitar

- quan el projecte necessita una identitat visual molt pròpia,
- quan s'acaba depenent massa de classes predefinides,
- quan es fa servir el framework sense entendre el layout base.

### Exemples habituals

- **Bootstrap**: útil per començar ràpid i tenir components estàndard.
- **Tailwind**: útil quan vols construir un sistema molt controlat amb utilitats petites.

> **Idea clau**
> Primer has d'entendre responsive sense framework. Després el framework suma valor.

---

## 8. Criteri professional

El responsive bo no depèn només del CSS.

També necessita:

- estructura HTML neta,
- contingut prioritzat,
- components reutilitzables,
- imatges i recursos fluids,
- proves en dispositius reals o simulats.

---

## 9. Errors habituals

- pensar només en escriptori,
- posar media queries sense una base clara,
- fer layouts rígids amb amplades fixes,
- usar frameworks com a plantilla tancada sense revisar-les,
- no provar el resultat en diferents amplades.

---

## 10. Activitat guiada (20-30 minuts)

Objectiu:

- convertir una interfície simple en responsive de manera controlada.

Tasca:

1. Dibuixar la versió mòbil del projecte.
2. Decidir què canvia en tauleta.
3. Decidir què canvia en escriptori.
4. Aplicar una o dues media queries com a màxim al principi.
5. Verificar que el layout continua sent usable.

### Evidència de sortida

- esquema de les tres versions,
- CSS amb punts de tall justificats,
- explicació breu del perquè de cada canvi.

---

## 11. Checklist ràpid

- La base està pensada per a mòbil.
- Les media queries tenen una funció clara.
- El layout canvia amb criteri, no per caprici.
- Els components continuen sent llegibles i usables.
- El projecte es prova en diferents amplades.
- El framework, si s'utilitza, està justificat.

---

## 12. Recursos oficials de consulta

- [MDN - Responsive design](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Responsive_Design)
- [web.dev - Responsive Web Design Basics](https://web.dev/articles/responsive-web-design-basics)
- [MDN - CSS media queries](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_media_queries/Using_media_queries)
- [Bootstrap Documentation](https://getbootstrap.com/docs/)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)

---

## 13. Resum del bloc

Responsive, mobile first i media queries són la base d'una interfície adaptable. Els frameworks poden ajudar, però només si primer s'entén el comportament del layout i es pren el criteri professional com a punt de partida.
