# Bloc 6: Components i sistemes de disseny

Aquest bloc transforma els fonaments previs en peces reutilitzables. L'objectiu és crear components consistents (botons, targetes, formularis, navegació) i entendre Bootstrap i Tailwind com a implementacions d'un sistema, no com a substituts del criteri.

---

## 1. Objectiu del bloc

En acabar aquest bloc, l'alumnat ha de poder:

1. Definir components UI reutilitzables.
2. Construir botons, targetes, formularis i navegació coherents.
3. Organitzar variants i estats d'interacció.
4. Entendre què és un sistema de disseny.
5. Aplicar Bootstrap i Tailwind amb criteri professional.

Idea clau: primer sistema, després framework.

---

## 2. Què és un component

Un component és una peça d'interfície amb una funció clara i repetible.

Exemples habituals:

* botó
* targeta
* camp de formulari
* barra de navegació

Un bon component té:

* estructura HTML clara
* estils consistents
* estats definits (`hover`, `focus`, `disabled`, `error`)
* variants controlades (primari, secundari, etc.)

---

## 3. Botons

Els botons guien l'acció principal de la pantalla.

### Bones pràctiques

* Defineix jerarquia (primari, secundari, terciari).
* Manté una mida tàctil adequada.
* Garanteix contrast i llegibilitat.
* Cuida estats d'interacció.

### Exemple base

Veure demo: [Botons](demos/5_exemples_components.html#botons)

---

## 4. Targetes

Les targetes agrupen contingut relacionat en un bloc visual.

### Regles bàsiques

* Padding intern coherent.
* Espais regulars entre títol, text i accions.
* Jerarquia visual clara dins la mateixa targeta.
* Variants mínimes i justificades.

### Estructura típica

* capçalera opcional
* cos (títol + descripció)
* peu amb accions

Veure demo: [Targetes](demos/5_exemples_components.html#targetes)

---

## 5. Formularis

Els formularis són punts crítics d'UX. Han de ser clars i tolerants a error.

!!! success "A tenir en compte"

        * Cada camp amb `label` visible.
        * Missatges d'error concrets i prop del camp.
        * Estats diferenciats: normal, focus, error, desactivat.
        * Agrupació lògica i ordre de lectura.

### Exemple de camp

Veure demo: [Formularis](demos/5_exemples_components.html#formularis)

---

## 6. Navegació

La navegació orienta l'usuari i defineix recorreguts.

### Criteris clau

* Menys opcions però més clares.
* Estat actiu visible a la secció actual.
* Patró consistent a tot el lloc.
* Adaptació responsive (menú col·lapsat en mòbil quan cal).

Veure demo: [Navegació](demos/5_exemples_components.html#navegacio)

---

## 7. Sistema de disseny (base mínima)

Un **sistema de disseny** és el conjunt de normes i elements que serveixen perquè una aplicació o una pàgina web tingui un aspecte coherent i uniforme.

### Elements mínims del sistema

#### Tokens

Els **tokens** són els valors bàsics del disseny que es reutilitzen a tota l'aplicació.

Exemples:

* **Color:** colors principals, secundaris, de fons o d'error.
* **Espai:** marges i separacions (8 px, 16 px, 24 px...).
* **Tipografia:** tipus de lletra, mida i pes.
* **Radi:** arrodoniment de les cantonades (4 px, 8 px...).
* **Ombres:** efectes d'ombra per donar profunditat als elements.

### Components

Els **components** són peces reutilitzables de la interfície.

Exemples:

* Botons
* Targetes (cards)
* Formularis
* Navegació (menús)

#### Variants i estats

Un mateix component pot tenir diferents versions (**variants**) i diferents comportaments (**estats**).

**Exemple d'un botó:**

**Variants:**

* Primari
* Secundari

**Estats:**

* Normal
* Hover (quan el cursor passa per sobre)
* Active (quan es prem)
* Disabled (desactivat)

### Convencions de nom

Les **convencions de nom** serveixen per identificar els elements de manera clara i coherent.

Exemples:

* `color-primary`
* `spacing-md`
* `button-primary`

### Exemple de tokens

A la demo **"Tokens i sistema"** es poden veure els tokens definits i com s'utilitzen per construir els diferents components de la interfície.

Veure demo: [Tokens i sistema](demos/5_exemples_components.html)

---

## 8. Bootstrap i Tailwind: implementacions del sistema

### Bootstrap

* Framework de components predefinits.
* Ràpid per prototips i pantalles estàndard.
* Requereix personalització per evitar resultats genèrics.

### Tailwind

* Framework utilitari basat en classes petites.
* Molt flexible per crear sistemes propis.
* Exigeix un gran criteri  de composició per evitar desordre.

### Criteri docent

No és "Bootstrap o Tailwind"; és:

1. definir sistema i components
2. implementar-los amb l'eina que més convingui

---

## 9. Errors habituals

* Repetir estils a mà en cada pantalla.
* No definir variants ni estats dels components.
* Fer servir components diferents per al mateix ús.
* Dependència total del framework sense criteri propi.
* No documentar decisions bàsiques del sistema.

---

Recursos oficials de consulta:

* [Bootstrap - Documentation](https://getbootstrap.com/docs/)
* [Tailwind CSS - Documentation](https://tailwindcss.com/docs)
* [W3C WAI-ARIA Authoring Practices Guide (APG)](https://www.w3.org/WAI/ARIA/apg/)
* [MDN - HTML forms](https://developer.mozilla.org/en-US/docs/Learn/Forms)
* [MDN - Accessibility (guides)](https://developer.mozilla.org/en-US/docs/Web/Accessibility)

---

## 10. El 20% que han de recordar sempre

1. Un component és una peça funcional reutilitzable.
2. Botons, targetes, formularis i navegació han de parlar el mateix llenguatge visual.
3. Sense estats (`hover`, `focus`, `error`, `disabled`) no hi ha component complet.
4. El sistema de disseny dona consistència i velocitat.
5. Bootstrap i Tailwind són eines; el criteri de disseny el poses tu.

---

## Resum del bloc

Aquest bloc connecta disseny i implementació. Quan l'alumnat domina components i sistema de disseny, pot construir interfícies coherents i escalar projectes amb o sense framework.
