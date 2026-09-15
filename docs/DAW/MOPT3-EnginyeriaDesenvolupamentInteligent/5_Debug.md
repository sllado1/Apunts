# Bloc 5: Debug

Aquest és el gran oblidat. I, alhora, una de les competències més útils per a qualsevol desenvolupador.

> **Quan alguna cosa no funciona...**
>
> 1. Reprodueix.
> 2. Llegeix l'error.
> 3. Localitza'l.
> 4. Formula una hipòtesi.
> 5. Comprova-la.

Això els servirà més que moltes hores de teoria.

---

## 1. Reprodueix

Si no pots reproduir el problema, no el pots resoldre de manera fiable.

Què cal fer:

- definir passos exactes,
- identificar entorn (navegador, dispositiu, versió),
- confirmar si falla sempre o de forma intermitent.

Evidència mínima:

- seqüència de passos clara i repetible.

---

## 2. Llegeix l'error

No improvisis canvis abans d'entendre el missatge.

Què cal mirar:

- tipus d'error,
- fitxer i línia,
- context (stack trace, consola, logs).

Regla d'or:

- l'error és una pista, no una sentència definitiva.

---

## 3. Localitza'l

Cal trobar el punt exacte on es trenca el comportament.

Eines i pràctiques:

- `console.log` amb criteri,
- punts de ruptura (breakpoints),
- inspecció de xarxa i resposta HTTP,
- validació d'inputs i estat intern.

Objectiu:

- passar de "no funciona" a "falla aquí, en aquesta condició".

---

## 4. Formula una hipòtesi

Una hipòtesi és una explicació concreta i comprovable.

Exemples:

- "El problema és que la resposta de l'API arriba buida".
- "El selector CSS no apunta a l'element correcte".
- "S'està executant codi abans que el DOM estigui carregat".

Mala pràctica:

- provar canvis aleatoris sense criteri.

---

## 5. Comprova-la

Per validar una hipòtesi, fes un canvi mínim i mesura el resultat.

Procés:

1. canvia una sola variable,
2. executa de nou,
3. observa si l'error desapareix,
4. confirma que no has trencat altres funcionalitats.

Si no funciona:

- descarta la hipòtesi i torna al pas 2 o 3.

---

## 6. Debug en l'era de la IA

Avui no cal passar hores mirant una línia, però sí cal pensar millor.

La IA és un accelerador, no un substitut del criteri tècnic.

Ús intel·ligent de la IA:

- aportar context complet (error, fitxer, pas de reproducció),
- demanar causes probables ordenades per prioritat,
- demanar comprovacions concretes, no "solucions màgiques",
- validar sempre la proposta en el teu codi real.

Ús deficient de la IA:

- copiar tall de codi sense entendre el que fa,
- aplicar molts canvis alhora,
- no verificar regressions, no comprovar l'impacte dels canvis fets.

> **Idea clau**
> Amb IA, el valor professional no és trobar una resposta; és validar-la i decidir bé.

---

## 7. Habilitats necessàries avui en dia

A més de saber programar, cal dominar:

1. **Pensament crític**: separar símptoma i causa arrel.
2. **Lectura tècnica**: entendre errors, logs i documentació.
3. **Observabilitat bàsica**: saber mirar consola, xarxa i estat.
4. **Capacitat d'experimentació**: provar hipòtesis de manera controlada.
5. **Comunicació tècnica**: explicar què falla, per què i com s'ha resolt.
6. **Validació de resultats d'IA**: filtrar propostes i comprovar impacte real.
7. **Disciplina de qualitat**: evitar arreglar un error amb un pedaç que resol el problema immediat però dificulta mantenir el codi més endavant.

---

## 9. Checklist ràpid

- El problema és reproduïble.
- L'error està llegit i documentat.
- Hi ha localització tècnica concreta.
- Hi ha una hipòtesi explícita.
- La hipòtesi s'ha comprovat amb un canvi mínim.
- La solució no trenca altres parts.
- S'ha validat qualsevol proposta de la IA amb proves reals.

---

## 10. Recursos oficials de consulta

- [MDN - Debugging HTML](https://developer.mozilla.org/en-US/docs/Learn_web_development/Howto/Tools_and_setup/What_are_browser_developer_tools)
- [MDN - JavaScript debugging reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors)
- [Chrome DevTools - Debug JavaScript](https://developer.chrome.com/docs/devtools/javascript/)
- [VS Code - Debugging](https://code.visualstudio.com/docs/editor/debugging)

---

## 11. Resum del bloc

Debug no és una habilitat secundària: és una metodologia de resolució de problemes. En l'era de la IA, guanya qui sap reproduir, interpretar, validar i comunicar solucions amb criteri.
