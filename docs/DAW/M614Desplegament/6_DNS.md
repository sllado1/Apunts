# Bloc 6. DNS i dominis

## Què és el DNS?

El **DNS** (*Domain Name System*) tradueix noms fàcils de recordar, com `www.exemple.cat`, en informació que els ordinadors poden utilitzar per trobar serveis a Internet, com ara una adreça IP. És com una agenda distribuïda: quan un navegador consulta un nom, els servidors DNS busquen el registre corresponent.

El DNS **no allotja la web ni hi envia directament el contingut**, i un registre DNS tampoc no fa una redirecció d'una pàgina web. Indica quin destí s'ha de consultar; el servidor de destinació ha d'estar preparat per respondre.

## Domini, zona DNS i servidor

- **Domini:** el nom registrat, per exemple `exemple.cat`. Es registra a través d'un registrador.
- **Servidors de noms (NS):** indiquen quins servidors gestionen la zona DNS del domini. Si la zona es gestiona en un proveïdor DNS, el domini ha d'utilitzar els NS que aquest proveïdor indica.
- **Zona DNS:** conjunt de registres que defineixen els noms i serveis del domini. Es pot gestionar al registrador o en un proveïdor DNS separat.
- **Servidor web:** màquina o servei que allotja l'aplicació. Té una IP pública o un nom de servei i ha d'acceptar les peticions del domini.

Canviar els registres s'ha de fer al **proveïdor que gestiona la zona autoritativa**. Si edites una zona en un lloc diferent dels NS configurats al domini, els canvis no tindran efecte públic.

## Tipus bàsics de registres DNS

| Tipus | Funció | Exemple d'ús |
| --- | --- | --- |
| **A** | Associa un nom a una adreça IPv4. | `app.exemple.cat` → `203.0.113.25` |
| **AAAA** | Associa un nom a una adreça IPv6. | `app.exemple.cat` → `2001:db8::25` |
| **CNAME** | Fa que un nom sigui un àlies d'un altre nom DNS. El client resol el nom de destinació per obtenir-ne l'adreça. | `www.exemple.cat` → `exemple.cat` |
| **MX** | Indica quins servidors reben el correu del domini i amb quina prioritat. | Servidors de correu del domini |
| **TXT** | Desa text associat a un nom; s'utilitza, entre altres coses, per verificar dominis i publicar polítiques de correu com SPF o instruccions DKIM/DMARC. | Verificació d'un servei extern |
| **NS** | Indica quins servidors són autoritatius per a una zona o subzona. | Delegació de DNS a un proveïdor |
| **CAA** | Indica quines autoritats poden emetre certificats TLS per al domini. | Restringir l'emissió de certificats |

El **TTL** (*Time To Live*) indica quant de temps els resolutors poden conservar un registre a la memòria cau. Per això, després d'un canvi, alguns usuaris poden continuar obtenint el valor anterior fins que caduqui la memòria cau.

## Fer que un subdomini apunti a un altre servidor

Suposem que `exemple.cat` ja apunta al servidor actual i volem que `app.exemple.cat` apunti a un servidor nou amb IP pública IPv4 `203.0.113.25`.

1. Obté del proveïdor del servidor nou la seva **IP pública**. Si l'adreça pot canviar quan es reinicia o es recrea la màquina, assigna una IP estàtica o configura una solució DNS dinàmica abans de publicar el registre.
2. Entra al panell del proveïdor DNS autoritatiu del domini i obre la zona de `exemple.cat`.
3. Crea o modifica un registre amb aquests valors orientatius:

   | Camp | Valor d'exemple |
   | --- | --- |
   | Tipus | `A` |
   | Nom / Host | `app` |
   | Valor / Contingut | `203.0.113.25` |
   | TTL | Per defecte del proveïdor o un valor curt durant les proves |

   Alguns panells esperen `app` al camp **Nom**; d'altres demanen el nom complet `app.exemple.cat`. Segueix el format que indiqui el proveïdor.

4. Si el servidor té una adreça IPv6 i també vols oferir-hi accés per IPv6, afegeix un registre **AAAA** amb aquesta adreça. No publiquis un AAAA si el servidor no pot rebre connexions IPv6.
5. Si prefereixes apuntar el subdomini a **un altre nom DNS** (per exemple, `servidor.proveidor.net`) en lloc d'una IP, crea un **CNAME** `app` → `servidor.proveidor.net`. Un CNAME no és una redirecció web: el navegador continuarà mostrant `app.exemple.cat`.
6. Connecta't al servidor nou i configura el servidor web perquè accepti el nom `app.exemple.cat`. Per exemple, a Apache configura un *VirtualHost* amb `ServerName app.exemple.cat` i la ruta de l'aplicació adequada.
7. Comprova que el tallafoc del sistema i el grup de seguretat del proveïdor permeten el trànsit necessari, habitualment **HTTP (80)** i **HTTPS (443)**. Configura també un certificat TLS vàlid per a `app.exemple.cat`.
8. Espera que s'actualitzin les memòries cau DNS i comprova la resolució i la web.

```text
app.exemple.cat.  A  203.0.113.25
```

El domini principal `exemple.cat` pot continuar apuntant al servidor antic mentre `app.exemple.cat` utilitza el servidor nou. Cada nom té els seus registres. Per apuntar el domini principal a una IP s'utilitza habitualment un registre **A** o **AAAA**; el CNAME a l'arrel del domini no està permès pel DNS estàndard, tot i que alguns proveïdors ofereixen registres d'àlies propis.

!!! warning "Canvis que poden afectar altres serveis"
    No substitueixis els registres **MX**, **TXT** o altres registres existents sense saber per a què serveixen: podries interrompre el correu o la verificació del domini. Per canviar el servidor web, modifica només els registres del nom que vols moure i conserva els altres.

## Comprovar la configuració

Des d'un terminal pots consultar quina adreça resol el subdomini:

```bash

dig app.exemple.cat AAAA
dig app.exemple.cat CNAME
```



Quan la resolució DNS ja retorna la IP nova, però la web no funciona, comprova el servidor, el *VirtualHost*, el tallafoc i el certificat TLS. DNS només ha resolt el nom; no confirma que l'aplicació estigui operativa.

## Idees clau

- Els registres DNS es canvien al proveïdor indicat pels NS autoritatius del domini.
- **A** i **AAAA** apunten a adreces IP; **CNAME** apunta a un altre nom DNS.
- **MX**, **TXT**, **NS** i **CAA** cobreixen serveis i configuracions diferents; no s'han d'esborrar a cegues.
- Per moure un subdomini a un altre servidor, actualitza el seu registre DNS i configura també el servidor nou, el tallafoc i HTTPS.
- El TTL i les memòries cau fan que els canvis no sempre siguin immediats.

Per ampliar-ho, consulta la documentació de [Dominis Dinahosting](https://dinahosting.com/ayuda/tipos-de-registros-dns/).
