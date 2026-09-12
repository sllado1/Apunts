# Bloc 1. Informació i dades: què tracta un ordinador?

**Pregunta clau:** com passa un ordinador de treballar amb zeros i uns a mostrar-nos un missatge, una nota o una fotografia?

Quan consultes les notes, escrius un missatge o deses una fotografia, estàs treballant amb dades. Per entendre què fa un sistema operatiu, primer hem d'entendre què són aquestes dades, com les representem i com en mesurem la quantitat.

Aquest bloc introdueix els conceptes inicials de l'apartat **1.2. Codificació de la informació en diferents sistemes de representació** del material de referència. Les conversions entre bases i les representacions numèriques més avançades queden per a un aprofundiment posterior.

## 1. Què aprendràs?

En acabar el bloc, has de poder:

- Distingir una dada de la informació que n'obtenim.
- Reconèixer dades numèriques, alfabètiques i alfanumèriques.
- Explicar per què els ordinadors representen les dades amb bits.
- Diferenciar bits i bytes i fer conversions senzilles.
- Explicar per què cal un codi per interpretar les dades.
- Relacionar aquests conceptes amb els fitxers i el sistema operatiu.

## 2. Dades i informació: quina diferència hi ha?

Una **dada** és la representació d'un fet, una observació o un valor. Pot ser un nombre, una paraula, una mesura o un símbol.

Imagina que trobes aquest valor escrit en un paper:

> 28

Pots llegir-lo, però sense context no saps què representa. Podrien ser 28 alumnes, 28 graus o el número d'una casa.

Ara afegim context:

> A l'aula d'informàtica hi ha 28 °C.

Ja pots interpretar el valor. La **informació** és el significat que obtenim quan posem les dades en context, les relacionem o les processem. Aquesta informació ens pot ajudar a prendre decisions; per exemple, valorar si cal ventilar l'aula.

!!! tip "Idea clau"
    Les dades són la matèria primera. Quan les interpretem amb un context, obtenim informació. No sempre cal fer un càlcul: de vegades, n'hi ha prou de saber què representa una dada.

### Exemple resolt: les notes d'una alumna

| Pas | Exemple | Què fem? |
| --- | --- | --- |
| Dades | `6`, `8` i `7` | Recollim tres valors. |
| Context | Són tres notes de la Laia i totes pesen igual. | Sabem què representen i com les hem de tractar. |
| Processament | `(6 + 8 + 7) / 3 = 7` | Calculem la mitjana. |
| Informació | La mitjana de la Laia és un 7. | Interpretem el resultat. |

Un resultat també pot convertir-se en una dada per a un altre procés: la mitjana de la Laia es pot utilitzar després per calcular la mitjana del grup.

## 3. El cicle de tractament de les dades

Un ordinador pot **rebre, processar, mostrar i emmagatzemar dades**.

```text
ENTRADA DE DADES  →  PROCESSAMENT  →  SORTIDA
Notes: 6, 8 i 7      Calcular mitjana   Mostrar: «Mitjana: 7»
```

Les dades d'entrada i els resultats es poden **desar** per recuperar-los més endavant.

Per exemple, quan utilitzes un full de càlcul:

1. Introdueixes les notes amb el teclat: és l'**entrada**.
2. El programa calcula la mitjana: és el **processament**.
3. Veus el resultat a la pantalla: és la **sortida**.
4. Deses el document en una unitat d'emmagatzematge: és l'**emmagatzematge**.

!!! note "On intervé el sistema operatiu?"
    El full de càlcul fa el càlcul de la mitjana. El sistema operatiu proporciona serveis perquè el programa rebi l'entrada, utilitzi memòria, mostri el resultat i desi el fitxer. A més, gestiona els recursos que necessita per executar-se.

## 4. Tipus de dades i caràcters

Un **caràcter** és un element d'un text, com una lletra, un dígit, un signe de puntuació o un espai.

Per exemple, `Aula 2` té sis caràcters: `A`, `u`, `l`, `a`, un espai i `2`.

Seguint la classificació introductòria del PDF, podem distingir:

| Tipus de dades | Què representen? | Exemples |
| --- | --- | --- |
| **Numèriques** | Quantitats amb les quals té sentit fer càlculs. | 28 alumnes, una nota de 7,5, una temperatura de −2 °C. |
| **Alfabètiques** | Text format per lletres. | `Laia`, `Barcelona`. |
| **Alfanumèriques** | Text que pot incloure lletres, dígits, espais i altres símbols. | `Aula 2`, `Carrer Major, 15`, `grup1@centre.cat`. |

### Un conjunt de dígits no sempre és una quantitat

El codi postal `08001` està escrit amb dígits, però identifica una zona. No té sentit sumar dos codis postals per obtenir-ne un de nou. Per això el tractem com a **text**, i així també conservem el zero inicial.

El mateix passa amb un número de telèfon: la seva funció és identificar, no expressar una quantitat.

!!! question "Pensa-hi"
    `15` pot ser el nombre d'ordinadors d'una aula o el número del carrer d'una adreça. En el primer cas podem calcular quants ordinadors falten; en el segon, el nombre forma part d'una identificació. El significat i l'ús de la dada són importants.

Aquesta classificació ens ajuda a començar, però també treballem amb dades com **imatges, so i vídeo**. L'ordinador també les representa digitalment.

## 5. Com representa les dades un ordinador?

Nosaltres utilitzem lletres, nombres, imatges i sons. Els circuits digitals d'un ordinador treballen amb dos estats lògics, que representem amb els símbols **0** i **1**.

Aquests estats es poden implementar, per exemple, amb dos intervals de tensió elèctrica. Els zeros i uns són la nostra manera d'escriure aquesta representació.

El **sistema binari** utilitza només dos dígits: `0` i `1`. Cada dígit binari és un **bit**.

### Un bit: dues possibilitats

Podem acordar que un bit representi si una opció està activada:

| Bit | Significat acordat |
| --- | --- |
| `0` | Opció desactivada. |
| `1` | Opció activada. |

Amb més bits podem representar més possibilitats:

| Nombre de bits | Combinacions possibles | Quantitat |
| --- | --- | --- |
| 1 | `0`, `1` | 2 |
| 2 | `00`, `01`, `10`, `11` | 4 |
| 3 | `000`, `001`, `010`, `011`, `100`, `101`, `110`, `111` | 8 |
| 8 | Des de `00000000` fins a `11111111` | 256 |

Cada bit afegit duplica el nombre de combinacions. Amb **n bits tenim 2ⁿ combinacions**.

### Una primera lectura d'un nombre binari

En decimal, les posicions valen unitats, desenes, centenes… En binari, de dreta a esquerra, valen **1, 2, 4, 8, 16…** Cada posició val el doble que l'anterior.

Per interpretar `00001101` com un enter sense signe:

| Valor de la posició | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Bit | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 1 |

Sumem només els valors de les posicions que tenen un `1`: **8 + 4 + 1 = 13**.

## 6. Bits i bytes: com mesurem les dades?

Un **byte**, també anomenat **octet**, és un grup de **8 bits**.

> **1 B = 8 bits**

Per exemple, `01000001` ocupa un byte. Amb els seus vuit bits podem formar 256 combinacions diferents. Si les interpretem com a enters sense signe, corresponen als valors del **0 al 255**, inclosos.

!!! warning "No confonguis bit i byte"
    La `b` minúscula s'utilitza per al bit i la `B` majúscula per al byte. **8 Mb equivalen a 1 MB**. Per passar de bytes a bits, multipliquem per 8; per passar de bits a bytes, dividim per 8.

### Múltiples decimals i binaris

Cal distingir dues famílies d'unitats:

| Múltiples decimals: salts de 1.000 | Múltiples binaris: salts de 1.024 |
| --- | --- |
| 1 kB = 1.000 B | 1 KiB = 1.024 B |
| 1 MB = 1.000 × 1.000 B | 1 MiB = 1.024 × 1.024 B |
| 1 GB = 1.000 × 1.000 × 1.000 B | 1 GiB = 1.024 × 1.024 × 1.024 B |

**Exemple resolt:** un fitxer de 2 KiB ocupa `2 × 1.024 = 2.048 bytes`. En bits són `2.048 × 8 = 16.384 bits`.

**Exemple de velocitat:** una transferència de 80 Mb/s equival a `80 / 8 = 10 MB/s`. A aquesta velocitat constant, transferir 100 MB trigaria 10 segons en un càlcul ideal, sense comptar dades de control ni altres limitacions.

!!! note "Precisió respecte del material de referència"
    El PDF utilitza kB, MB i GB també per a múltiples de 1.024. En aquests apunts distingim explícitament kB de KiB, MB de MiB i GB de GiB per evitar confusions.

## 7. Què vol dir codificar les dades?

**Codificar** és representar dades seguint unes regles. Per recuperar-ne el significat, hem de conèixer les regles utilitzades.

Per exemple, `X` pot ser una lletra o representar el nombre deu en numeració romana. El símbol és el mateix, però la interpretació depèn del codi.

Amb els bits passa el mateix. La seqüència `01000001` pot representar:

- El nombre **65**, si la interpretem com un enter binari sense signe.
- La lletra **A**, si la interpretem com a text ASCII.

Per tant, **els bits per si sols no ens indiquen com els hem d'interpretar**. Necessitem saber el tipus de dada i la codificació o el format.

### Com representem el text?

- **ASCII** és un codi de 7 bits amb 128 valors, que inclou lletres llatines sense accent, dígits, signes i caràcters de control. Els seus valors es poden guardar en bytes.

**Unicode: un número per identificar cada caràcter**

Imagina Unicode com un gran catàleg de lletres, signes i altres símbols de molts sistemes d'escriptura. Cada element del catàleg té un número que l'identifica. Aquest número s'anomena **punt de codi**.

Per exemple:

| Caràcter | Número que li assigna Unicode, escrit en decimal |
| --- | --- |
| `A` | 65 |
| `à` | 224 |
| `€` | 8.364 |

El número **65 identifica la lletra `A`** dins d'aquest catàleg. No vol dir que la lletra ocupi 65 bytes: és el seu identificador, com el número de carnet identifica un alumne.

Pots trobar aquests identificadors escrits com `U+0041` per a `A`. El prefix `U+` indica que és un punt de codi Unicode i el número que el segueix està escrit en hexadecimal. De moment, només cal entendre que **és una altra manera d'escriure el seu número identificador**.

**UTF-8: com desem aquests identificadors en bytes**

Quan desem text en un fitxer, necessitem representar aquests identificadors amb bytes. **UTF-8 estableix les regles per fer aquesta conversió**. Segons el punt de codi, utilitza entre 1 i 4 bytes.

| Caràcter | Identificador Unicode en decimal | Representació en UTF-8: cada grup de 8 bits és un byte | Espai |
| --- | --- | --- | --- |
| `A` | 65 | `01000001` | 1 byte |
| `à` | 224 | `11000011 10100000` | 2 bytes |
| `€` | 8.364 | `11100010 10000010 10101100` | 3 bytes |

No cal memoritzar aquestes seqüències. Observa que **Unicode ens diu quin caràcter és i UTF-8 com el representem en bytes**.

Quan tornem a obrir el fitxer, el programa fa el camí invers: interpreta els bytes segons les regles d'UTF-8, recupera els identificadors Unicode i mostra el text.

Per exemple, en UTF-8, `A` ocupa 1 byte i `à` ocupa 2 bytes. Per això **comptar les lletres d'un text no és suficient per saber quants bytes ocupa**.

### I les imatges i el so?

Una imatge digital pot representar-se amb valors de color de píxels. Un so digital es pot representar amb una seqüència de mostres. Els formats dels fitxers estableixen com es guarden aquestes dades i poden aplicar compressió.

Quan obres un fitxer, el programa interpreta les dades segons el format. El sistema operatiu facilita l'accés al fitxer i als recursos necessaris.

## 8. Exemple complet: desar una nota de classe

Imagina que escrius `Hola` en un editor de text i ho deses com a `salutacio.txt` en UTF-8.

1. **Entrada:** escrius els quatre caràcters amb el teclat.
2. **Representació:** el programa codifica el text en UTF-8.
3. **Memòria:** mentre hi treballes, el programa utilitza la RAM.
4. **Emmagatzematge:** en desar, el programa demana al sistema operatiu que escrigui el fitxer a la unitat d'emmagatzematge.
5. **Recuperació:** en obrir-lo, el programa llegeix els bytes i els interpreta com a text.

Les quatre lletres de `Hola` ocupen **4 bytes en UTF-8**, si no afegim cap salt de línia ni cap marca addicional. L'espai assignat al disc pot ser més gran perquè el sistema de fitxers organitza l'emmagatzematge en blocs.

!!! tip "Connexió amb el mòdul"
    Quan estudiem memòria, fitxers i emmagatzematge, continuarem treballant amb aquestes idees: les dades tenen una representació, ocupen espai i els programes necessiten recursos per tractar-les.

## 9. Comprova què has entès

Intenta respondre abans d'obrir les solucions.

1. Trobes la dada `92`. Quin context hi afegiries perquè aportés informació?
2. Un full conté les notes `5`, `7` i `9`, totes amb el mateix pes. Identifica les dades, el processament i la informació que obtenim calculant-ne la mitjana.
3. Classifica el tipus de dades de: `Marta`, una quantitat de `24` ordinadors, `Carrer Nou, 7` i el codi postal `08001`.
4. Quants bits hi ha en 6 bytes? Quants bytes són 32 bits?
5. Quantes combinacions es poden representar amb 4 bits?
6. Quin valor decimal té `00001010` si representa un enter sense signe?
7. Quants bytes són 3 KiB? I 3 kB?
8. Per què és incorrecte afirmar que un caràcter sempre ocupa un byte?
9. Si una aplicació calcula una mitjana i la desa en un fitxer, quina feina fa l'aplicació i com hi participa el sistema operatiu?

??? success "Solucions orientatives"
    1. Per exemple: «La bateria està al 92 %». El context ens indica què representa el valor.
    2. Les dades són les tres notes; el processament és `(5 + 7 + 9) / 3`; la informació és que la mitjana és un 7.
    3. `Marta`: alfabètica; 24 ordinadors: numèrica; `Carrer Nou, 7`: alfanumèrica; `08001`: text que identifica una zona, encara que només contingui dígits.
    4. `6 × 8 = 48 bits`; `32 / 8 = 4 bytes`.
    5. `2⁴ = 16 combinacions`.
    6. `8 + 2 = 10`.
    7. `3 × 1.024 = 3.072 bytes`; `3 × 1.000 = 3.000 bytes`.
    8. Depèn de la codificació i del caràcter. En UTF-8, `A` ocupa 1 byte i `à`, 2 bytes.
    9. L'aplicació calcula la mitjana i demana desar el resultat. El sistema operatiu gestiona recursos com la memòria i proporciona els serveis per escriure el fitxer.


## Material de referència

Adaptació didàctica de *Sistemes operatius monolloc. Introducció als sistemes operatius*, apartat **1.2**, especialment els subapartats **1.2.1–1.2.4 i 1.2.11–1.2.12**, del document facilitat `fp_smx_m02_u1_pdfindex.pdf`.