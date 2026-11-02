# Bloc 5. Màquines virtuals amb VirtualBox

## Què és VirtualBox?

**Oracle VirtualBox** és un programa de virtualització: permet executar un ordinador virtual dins del nostre ordinador físic. L'ordinador físic és l'**amfitrió** (*host*) i el sistema operatiu instal·lat a la màquina virtual és el **convidat** (*guest*).

```mermaid
flowchart TB
    H["Ordinador físic · amfitrió"]
    V["VirtualBox"]
    VM["Màquina virtual · convidat"]
    OS["Ubuntu/Windows/Altre"]
    H --> V --> VM --> OS
```

La màquina virtual té maquinari virtual propi —com ara memòria, processador, disc i xarxa—, però utilitza els recursos de l'ordinador amfitrió.

## Instal·lació i primera configuració

1. Ves al [web oficial de descàrregues de VirtualBox](https://www.virtualbox.org/wiki/Downloads) i tria el paquet per al sistema operatiu de l'ordinador amfitrió.
2. Executa l'instal·lador i accepta els permisos necessaris. En alguns sistemes caldrà autoritzar controladors de xarxa o reiniciar.
3. Baixa la imatge ISO del sistema operatiu que vols instal·lar a la màquina virtual.
4. A VirtualBox, crea una màquina virtual, selecciona el sistema operatiu i la ISO, i assigna memòria, processadors i espai de disc.

```mermaid
flowchart TD
    D["Descarregar VirtualBox"] --> I["Instal·lar al host"]
    I --> ISO["Obtenir una ISO"]
    ISO --> VM["Crear la màquina virtual"]
    VM --> OS["Instal·lar el sistema convidat"]
```

### Abans de començar

- **Virtualització a la BIOS/UEFI:** comprova que la virtualització de maquinari estigui activada. Pot aparèixer com **Intel VT-x**, **Intel Virtualization Technology**, **AMD-V** o **SVM Mode**. El nom i la ubicació varien segons l'ordinador; normalment es configura a la BIOS/UEFI i cal reiniciar. Si està desactivada, les màquines virtuals de 64 bits poden no iniciar-se o funcionar malament.
- **Recursos:** reserva prou memòria i processadors per al sistema amfitrió. No assignis a la màquina virtual tots els recursos de l'ordinador.
- **Controladors i xarxa:** durant la instal·lació, el sistema pot demanar permís per instal·lar controladors. A Windows, la xarxa pot interrompre's breument mentre s'instal·len els adaptadors virtuals.
- **Hyper-V a Windows:** si una màquina virtual va molt lenta o no s'inicia, Hyper-V o altres funcions de virtualització de Windows poden influir-hi. Comprova la configuració abans de canviar-la i no desactivis funcions de seguretat d'un equip gestionat sense consultar-ne l'administrador.

## Aturar la màquina virtual

Quan tanques una màquina virtual en execució, VirtualBox ofereix diverses opcions:

| Opció | Què fa? | Quan convé? |
| --- | --- | --- |
| **Desar l'estat de la màquina** | Desa l'estat actual i tanca la finestra. En tornar-la a iniciar, continua aproximadament on era. | Si vols reprendre la feina més tard sense tancar els programes. |
| **Enviar el senyal d'aturada** | Demana al sistema convidat que s'apagui de manera normal, com si premessis el botó d'engegada de l'ordinador. | Per apagar la màquina virtual sense perdre dades. Cal que el sistema convidat respongui al senyal. |
| **Apagar la màquina** | Talla l'alimentació virtual immediatament. És com desconnectar l'ordinador de l'endoll. | Només si el sistema s'ha quedat bloquejat i no respon. Es poden perdre dades no desades o malmetre fitxers. |

La forma més segura és **desar la feina i apagar el sistema des del menú d'Ubuntu o Windows convidat**. També pots triar **Enviar el senyal d'aturada** al diàleg de tancament de VirtualBox. No facis servir **Apagar la màquina** com a forma habitual d'aturada.

## Guest Additions a Ubuntu

Les **Guest Additions** s'instal·len dins del sistema convidat. Milloren la integració amb l'amfitrió: ajust automàtic de la mida de pantalla, millor moviment del ratolí i funcions com el porta-retalls compartit.

1. Inicia Ubuntu i, a la finestra de VirtualBox, selecciona **Dispositius → Insereix la imatge de CD de les Guest Additions** (*Devices → Insert Guest Additions CD Image*).
2. A Ubuntu, obre el CD muntat i executa `VBoxLinuxAdditions.run` com a administrador. Si apareix la finestra d'execució del programari, selecciona **Executar**. També ho pots fer des d'un terminal. El CD normalment es munta a `/media/$USER/VBox_GAs_<versió>`; entra a la carpeta (el nom inclou la versió instal·lada):

   ```bash
   cd /media/$USER/VBox_GAs_*/
   sudo sh ./VBoxLinuxAdditions.run
   ```

3. **Només si l'instal·lador indica que falten eines o capçaleres del nucli**, instal·la-les:

   ```bash
   sudo apt update
   sudo apt install build-essential dkms linux-headers-$(uname -r)
   ```

   Aquest pas no cal fer-lo sempre: prepara Ubuntu per compilar els mòduls quan les eines necessàries no hi són. Quan acabi, **torna a executar l'instal·lador de les Guest Additions des del CD** (pas 2).

4. Reinicia Ubuntu perquè els controladors s'activin:

   ```bash
   sudo reboot
   ```

Les Guest Additions han de correspondre a la versió de VirtualBox instal·lada a l'amfitrió. Si Secure Boot impedeix carregar algun mòdul, segueix l'avís d'Ubuntu per autoritzar-lo o consulta l'administrador de l'equip.

### Si les Guest Additions no funcionen

Obre **Terminal** a Ubuntu (`Ctrl`+`Alt`+`T`) i executa aquestes comprovacions després de reiniciar. Escriu cada ordre i prem `Retorn`:

1. **Comprova si els processos de Guest Additions s'estan executant:**

   ```bash
   pgrep -a 'VBoxProcess'
   pgrep -a 'VBoxClient'
   pgrep -a 'VBoxService'
   ```

   Si apareixen processos `VBoxClient` o `VBoxService`, els serveis s'han iniciat. Si no apareix cap resultat, continua amb les comprovacions següents.

2. **Comprova si els mòduls del nucli s'han carregat:**

   ```bash
   lsmod | grep vbox
   ```

   Haurien d'aparèixer mòduls com `vboxguest` i, en alguns sistemes, `vboxsf` o `vboxvideo`. Si no apareix res, poden faltar capçaleres durant la instal·lació o Secure Boot pot haver blocat els mòduls.

3. **Comprova que hi ha el registre d'instal·lació i consulta'n les darreres línies:**

   ```bash
   sudo tail -n 40 /var/log/vboxadd-setup.log
   ```

   Introdueix la contrasenya d'Ubuntu si la demana. El terminal no mostra els caràcters de la contrasenya mentre l'escrius; prem `Retorn` en acabar. Busca missatges amb `error` o `failed`. Si el fitxer no existeix, l'instal·lador pot no haver-se executat.

4. **Si falten capçaleres o eines**, comprova el nucli actual i instal·la els paquets corresponents; després torna a executar l'instal·lador del CD i reinicia:

   ```bash
   sudo apt update
   sudo apt install build-essential dkms linux-headers-$(uname -r)
   ```

5. **Si els mòduls no es carreguen i Secure Boot està activat**, durant l'arrencada pot aparèixer la pantalla blava MOK per autoritzar-los.  Comprova també que la imatge de Guest Additions sigui de la mateixa versió que VirtualBox.

Si continua fallant, copia la sortida de `pgrep`, `lsmod` i les línies d'error del registre per compartir-les amb el professor.

## Connectar un dispositiu USB

Per passar un USB de l'ordinador amfitrió a la màquina virtual:

1. Apaga la màquina virtual i obre **Configuració → USB**.
2. Activa el controlador USB que necessitis: **USB 1.1**, **USB 2.0** o **USB 3.0**. Per utilitzar USB 2.0 o 3.0 pot caldre instal·lar l'Extension Pack a l'amfitrió.
3. Inicia la màquina virtual. Al menú **Dispositius → USB**, selecciona el dispositiu que vols connectar.
4. Per tornar-lo a l'amfitrió, desmarca'l al mateix menú abans de fer-lo servir fora de la màquina virtual.

### Quin controlador USB escollir?

El controlador determina la versió i la velocitat màxima de transmissió que pot utilitzar la màquina virtual: USB 1.1 és més lent que USB 2.0, i USB 3.0 permet velocitats més altes. Escull una versió compatible amb el dispositiu i amb l'ús que en faràs; una versió més nova no garanteix que el dispositiu funcioni més de pressa si el dispositiu o el port de l'amfitrió no la suporten.

La versió del controlador **no determina si VirtualBox veu el dispositiu**. Si no apareix al menú **Dispositius → USB**, comprova que el controlador estigui activat, que l'Extension Pack estigui instal·lat si cal, i que l'amfitrió i VirtualBox puguin accedir al dispositiu. Els filtres USB només serveixen per automatitzar la connexió.

### Filtres USB

Un **filtre USB** és una regla que permet a VirtualBox reconèixer un dispositiu i connectar-lo automàticament a una màquina virtual quan l'endolles. Sense filtre, pots connectar-lo manualment des de **Dispositius → USB** cada vegada.

Per crear-ne un, connecta el dispositiu a l'ordinador amfitrió i apaga la màquina virtual. Obre **Configuració → USB**, comprova que el controlador USB adequat està activat i prem la icona d'afegir filtre (un símbol **+**). Tria el dispositiu de la llista i desa els canvis. En iniciar la màquina virtual, VirtualBox l'assignarà automàticament al convidat.

Fes servir un filtre només si connectes sovint el mateix dispositiu a la mateixa màquina virtual. Mentre el dispositiu està connectat al convidat, no es pot fer servir des de l'amfitrió. Si vols tornar-lo a l'amfitrió, desconnecta'l des del menú **Dispositius → USB**.

```mermaid
flowchart TD
    U["Dispositiu USB"] -->|Connectat al menú Dispositius| VM["Ubuntu virtual"]
    VM -. "Desconnectar per recuperar-lo" .-> H["Ordinador amfitrió"]
```

Mentre l'USB està connectat al convidat, normalment no està disponible per a l'amfitrió. En un amfitrió Linux, també cal que el compte tingui permisos per utilitzar VirtualBox i els dispositius USB.

!!! note "Extension Pack i llicència"
    L'Extension Pack és diferent de les Guest Additions: s'instal·la a l'**amfitrió** i afegeix funcions com el suport USB 2.0/3.0. Consulta les condicions de llicència vigents al [web oficial](https://www.virtualbox.org/wiki/Downloads), especialment si l'ús no és personal o educatiu.

Fonts: [descàrregues oficials de VirtualBox](https://www.virtualbox.org/wiki/Downloads), [manual de VirtualBox: Guest Additions](https://www.virtualbox.org/manual/ch04.html) i [manual de VirtualBox: configuració USB](https://www.virtualbox.org/manual/ch03.html#settings-usb).
