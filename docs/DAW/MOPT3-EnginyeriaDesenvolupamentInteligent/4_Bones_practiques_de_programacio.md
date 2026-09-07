# Bloc 4: Bones pràctiques de programació

Aquest serà probablement el capítol més consultat. L'objectiu és tenir regles simples que es puguin aplicar cada dia.

---

## 1. Variables amb noms descriptius

❌ Incorrecte

```javascript
let x = 3;
let y = 120;
let z = x * y;
```

✅ Correcte

```javascript
const numberOfTickets = 3;
const ticketPrice = 120;
const totalPrice = numberOfTickets * ticketPrice;
```

---

## 2. Funcions petites

❌ Incorrecte

```javascript
function processGame(game) {
  // valida, calcula puntuacio, desa resultat, envia notificacio i renderitza UI
}
```

✅ Correcte

```javascript
function validateGame(game) {
  return game.players.length > 0;
}

function calculateScore(game) {
  return game.hits * 10;
}

function saveResult(result) {
  // persistencia
}
```

---

## 3. Evitar duplicació

❌ Incorrecte

```javascript
const finalPriceA = priceA - (priceA * 0.1);
const finalPriceB = priceB - (priceB * 0.1);
const finalPriceC = priceC - (priceC * 0.1);
```

✅ Correcte

```javascript
function applyDiscount(price, discount) {
  return price - (price * discount);
}

const finalPriceA = applyDiscount(priceA, 0.1);
const finalPriceB = applyDiscount(priceB, 0.1);
const finalPriceC = applyDiscount(priceC, 0.1);
```

---

## 4. Constants

❌ Incorrecte

```javascript
if (playerScore >= 1000) {
  level = 2;
}
```

✅ Correcte

```javascript
const LEVEL_UP_SCORE = 1000;

if (playerScore >= LEVEL_UP_SCORE) {
  level = 2;
}
```

---

## 5. Indentació

❌ Incorrecte

```javascript
function renderCard(card){
if(card.active){
console.log(card.title);
}
}
```

✅ Correcte

```javascript
function renderCard(card) {
  if (card.active) {
    console.log(card.title);
  }
}
```

---

## 6. Codi mort

❌ Incorrecte

```javascript
function calculateBonus(points) {
  return points * 2;
  console.log('Aquesta linia mai s executa');
}
```

✅ Correcte

```javascript
function calculateBonus(points) {
  return points * 2;
}
```

---

## 7. Comentaris útils

❌ Incorrecte

```javascript
// sumem dos numeros
const total = subtotal + taxes;
```

✅ Correcte

```javascript
// Apliquem impostos abans de mostrar el preu final a la pantalla de pagament
const total = subtotal + taxes;
```

---

## Checklist ràpid

- Les variables expliquen què representen.
- Les funcions fan una sola responsabilitat.
- No hi ha blocs duplicats evitables.
- Els valors clau estan declarats com a constants.
- El codi manté indentació consistent.
- No queda codi mort.
- Els comentaris aporten context real.

---

## Resum del bloc

Aquest bloc no busca escriure codi "bonic", sinó codi mantenible. Si l'alumnat aplica aquestes set regles, el projecte serà més clar, més robust i més fàcil d'evolucionar.
