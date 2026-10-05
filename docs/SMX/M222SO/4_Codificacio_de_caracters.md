# Bloc 4. Codificació de caràcters: ASCII i Unicode

**Pregunta clau:** com representa un ordinador les lletres i els símbols?

## 1. ASCII: cada caràcter té un número

**ASCII (American Standard Code for Information Interchange)** és un sistema de codificació que assigna un **valor numèric a cada caràcter**. Aquest valor es pot representar en binari.

**Caràcter → codi numèric → representació binària**

| Caràcter | Decimal | Binari (mostrat amb 8 bits) |
| --- | --- | --- |
| A | 65 | `01000001` |
| B | 66 | `01000010` |
| C | 67 | `01000011` |
| 7 | 55 | `00110111` |
| Espai | 32 | `00100000` |

!!! note "ASCII estàndard té 7 bits"
    Permet **128 valors, del 0 al 127**. A la taula afegim un **0 a l'esquerra** per mostrar cada codi en un byte de 8 bits. Les extensions de 8 bits, sovint anomenades **ASCII estès**, són diverses i no formen un únic sistema.

ASCII inclou:

- **Caràcters imprimibles:** lletres, dígits, signes i espai.
- **Caràcters de control:** indiquen accions com el salt de línia o la tabulació; no són lletres visibles.

El caràcter **`7`** té el codi **55**: el símbol que escrivim i el seu codi són coses diferents. ASCII estàndard tampoc no inclou caràcters com **ç**, **à** o **€**.

## 2. EBCDIC: el mateix caràcter, un altre codi

**EBCDIC (Extended Binary Coded Decimal Interchange Code)** és una codificació de **8 bits**, associada històricament als grans sistemes d'IBM.

| Caràcter | ASCII (en un byte) | EBCDIC |
| --- | --- | --- |
| A | `01000001` | `11000001` |

**Per interpretar els bits com a text, hem de saber quina codificació s'ha utilitzat.** No cal memoritzar la taula EBCDIC.

## 3. Unicode: caràcters de molts idiomes

Els sistemes anteriors no permetien representar tots els caràcters utilitzats al món. **Unicode** assigna codis als caràcters de molts sistemes d'escriptura, símbols i emojis.

| Caràcter | Codi Unicode |
| --- | --- |
| A | `U+0041` |
| ç | `U+00E7` |
| € | `U+20AC` |

La notació **U+** indica un codi Unicode escrit en **hexadecimal**.

**Unicode defineix el codi; UTF-8, UTF-16 i UTF-32 indiquen com guardar-lo en bytes.** Unicode no està limitat a 16 bits ni a 65.536 caràcters.

| Codificació | Bytes per codi Unicode |
| --- | --- |
| UTF-8 | D'1 a 4 bytes. Els caràcters ASCII ocupen 1 byte. |
| UTF-16 | 2 o 4 bytes. |
| UTF-32 | 4 bytes. |

Per exemple, en **UTF-8**, `A` ocupa **1 byte** i `€` ocupa **3 bytes**. Per tant, **un caràcter no sempre ocupa un byte**.

## 4. Comprova que ho has entès

1. Si `A` té el codi 65, què representa `01000001` en ASCII?
2. Per què no podem dir que ASCII estàndard té 256 valors?
3. Quina diferència hi ha entre Unicode i UTF-8?

??? success "Respostes"
    1. El caràcter **A**.
    2. Perquè utilitza **7 bits**: `2⁷ = 128` valors.
    3. **Unicode** assigna codis als caràcters; **UTF-8** els representa en bytes.

Fonts: [ASCII i EBCDIC (IBM)](https://www.ibm.com/docs/en/zos-basic-skills?topic=mainframe-ebcdic-character-set), [model de codificació de caràcters (Unicode)](https://www.unicode.org/reports/tr17/) i [UTF-8, UTF-16 i UTF-32 (Unicode)](https://www.unicode.org/faq/utf_bom.html).