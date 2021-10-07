![](RackMultipart20211007-4-7ma4kz_html_f82d96c26cc03594.png)

## **Diari Oficial de la Generalitat de Catalunya**

## **Document d&#39;integració del servei**

 ![](RackMultipart20211007-4-7ma4kz_html_9b4dd0d250015309.gif) ![](RackMultipart20211007-4-7ma4kz_html_87fa512ea052536a.gif) ![](RackMultipart20211007-4-7ma4kz_html_951ed91e1bcd9028.gif) ![](RackMultipart20211007-4-7ma4kz_html_1eb070f55a9c9a8.gif)

Realitzat per: Departament d&#39;Operacions – Unitat de Projectes

Versió: 2.0

Data: 7/10/2021

 ![](RackMultipart20211007-4-7ma4kz_html_e7cf959e7fe4dc1d.png)

**Control del document**

**Informació general**

| **Títol:** | Diari Oficial de la Generalitat de Catalunya. Document d&#39;integració del servei |
| --- | --- |
| **Creat per:** | Departament d&#39;Operacions – Unitat de Projectes |
| **A revisar per:** | Departament d&#39;Operacions – Suport a Integracions |
| **A aprovar per:** | Departament d&#39;Operacions – Suport a Integracions |
| **Llista de distribució:** |
| **Nom del document:** | DI - DOGC.doc |

**Històric de revisions**

| **Versió** | **Data** | **Autor** | **Comentaris** |
| --- | --- | --- | --- |
| V1.0 | 18/06/2012 | Roger Noguera i Arnau | Creació del document. |
| V1.1 | 02/04/2014 | Roger Noguera i Arnau | Adaptació a canvis en els serveis del DOGC |
| V2.0 | 18/07/2016 | Roger Noguera i Arnau | Suport de publicació al TEU del BOE via DOGC. |

# **Índex** #

1. Introducció
2. Transmissions de dades disponibles
3. Missatgeria del servei
   1. Sol·licitud de publicació
      1. Petició – dades específiques
      2. Petició – dades genèriques
      3. Resposta – dades específiques
   2. Consulta d&#39;estat
      1. Petició – dades específiques
      2. Resposta – dades específiques
   3. Operacions sobre una publicació
      1. Petició – dades específiques
      2. Resposta – dades específiques

# 1 Introducció

Aquest document detalla la missatgeria associada al servei de publicació del Diari Oficial de la Generalitat de Catalunya (en endavant DOGC).

Per poder realitzar la integració cal conèixer prèviament la següent documentació:

- Document d&#39;_Especificació de missatgeria pel consum de productes de la plataforma PCI_ del Consorci AOC.

# 2 Transmissions de dades disponibles

Les operacions disponibles a través del servei són les que es presenten a continuació:

| **EMISSOR** |
| --- |
| DOGC (Diari Oficial de la Generalitat de Catalunya) |
| **PRODUCTE** | **MODALITAT** | **DESCRIPCIO** |
| **DOGC** | DOGC | Operacions del servei de publicació del DOGC:

- Sol·licitud de publicació i càrrega de fitxers
- Consulta d&#39;estat d&#39;una publicació
- Realitzar operacions sobre una publicació

# 3 Missatgeria del servei

A continuació es detalla la missatgeria corresponent al bloc de dades específiques de les diferents operacions del servei.

L&#39;organisme que realitza la publicació s&#39;identifica en l&#39;element de la missatgeria genèrica DatosAutorizacion/IdentificadorSolicitante.
 En cas que la integració es realitzi via una plataforma intermediària – **com en el cas de la PCSP** - caldrà informar el codi INE10 de l&#39;organisme emissor del document a l&#39;element IdSolicitanteOriginal.

## 3.1 Sol·licitud de publicació

### 3.1.1 Petició – dades específiques

| _Element_ | _Descripció_ |
| --- | --- |
 /peticioSolicitudPublicacio/identificador | Codi de document del sistema origen (únic).
 /peticioSolicitudPublicacio/ordreInsercio | XML codificat en Base64 amb la informació del document a publicar. L&#39;ordre d&#39;inserció ha d&#39;estar signada en format XAdES-BES (signatura bàsica, _enveloped_) emprant un certificat de signatura reconeguda (nivell 4). En el cas d&#39;EACAT l&#39;ordre d&#39;inserció no estarà signada i la signatura s&#39;enviarà en un fitxer a banda de tipus signatura (tipus 4). En aquest cas el format de la signatura serà CAdES. Per més detalls sobre l&#39;estructura del XML consulteu l&#39;apartat 3.1.1.1 d&#39;aquest document.
 /peticioSolicitudPublicacio/registre | Bloc de dades corresponent a la informació de registre. Només s&#39;ha d&#39;informar quan la petició procedeix d&#39;EACAT. Per a la resta de sistemes els assentaments es realitzaran automàticament.
/registre/registreSortida/numero|Número d&#39;assentament de sortida de l&#39;organisme.
/registre/registreSortida/data|Data d&#39;assentament de sortida de l&#39;organisme.
/registre/registreEntrada/numero|Número d&#39;assentament d&#39;entrada a l&#39;EADOP.
/registre/registreEntrada/data|Data d&#39;assentament d&#39;entrada a l&#39;EADOP.

#### 3.1.1.1 Ordre d&#39;inserció

El DOGC requereix que tota operació relacionada amb una publicació vagi acompanyada d&#39;un XML signat emprant un certificat de signatura reconeguda (nivell 4) amb les dades de la sol·licitud de publicació.

| _Element_ | _Descripció_ |
| --- | --- |
/ordreInsercio/document | Bloc de dades corresponent al document a publicar.
/document/identificador | Codi de document del sistema origen (el mateix que s&#39;informa a l&#39;element peticioSolicitudPublicacio /identificador).  Pels serveis externs a EACAT, aquest identificador haurà de tenir un prefix que identifiqui el servei d&#39;origen. Cal acordar amb el Consorci AOC el prefix que cada requeridor ha d&#39;emprar.
/document/titol | Títol del document. Com a mínim s&#39;ha d&#39;informar un títol (en català o castellà).
/document/idioma | Codi d&#39;idioma: 1: ca\_es: català, 2: es: castellà, 3: oc\_es: aranès
/document/tipus | Tipus de document:<ul><li>009: Resolució</li><li>010: Circular</li><li>011: Edicte</li><li>012: Anunci</li><li>013: Decret de l&#39;Administració local</li><li>015: Correcció d&#39;errades</li><li>018: Instrucció</li><li>019: Acord</li><li>140: Dictamen</li><li>150: Ordenança municipal</li></ul>|
/document/observacions | Observacions de l&#39;usuari que publica.
/document/data | Data del document a publicar.
/document/dadesPersonals | Indica si el document conté dades de caràcter personal (S / N).
/ordreInsercio/fitxers | Bloc de dades corresponent als fitxers a publicar.
/ordreInsercio/fitxers/fitxer | Bloc de dades corresponent a un fitxer a publicar.
/fitxer/identificador | Identificador de document. Únic en la petició. Per identificar cada adjunt, caldrà alinear l&#39;atribut Fichero@Id del bloc de dades genèriques amb l&#39;element identificador de cadascun dels document informats a les dades específiques de la sol·licitud.  En cas de transferència de fitxers adjunts seguint l&#39;estàndard MTOM, cal informar els adjunts en l&#39;element Contenido del bloc de dades genèriques Ficheros destinat a aquest efecte. La grandària màxima de fitxer suportada són 10MB.

/fitxer/nom | Nom del fitxer. El nom del fitxer no es pot repetir en la mateixa ordre d&#39;inserció.
 Només s&#39;accepten caràcters alfanumèrics (sense accents) i els caràcters &#39;.&#39;, &#39;-&#39;, &#39;\_&#39; i &#39; &#39;.

/fitxer/idioma | Codi d&#39;idioma:
- ca\_es: català
- es: castellà
- oc\_es: aranès

/fitxer/tipus | Tipus de fitxer:
- 1: Principal (.doc, .docx i .rtf)
- 2: Annex (.doc, .docx i .rtf)
- 3: Imatges i PDFs (.pdf, .jpg. tiff)
- 4: Fitxer signatura si la petició procedeix d&#39;EACAT.
/fitxer/ordre | Ordre en que es publicaran els annexos al final del document principal. Obligatori pel tipus de fitxers annex (2).

/fitxer/hash | Resum criptogràfic del fitxer adjunt (SHA-1).
/ordreInsercio/usuaris | Bloc de dades corresponent a les dades de l&#39;usuari que signa la sol·licitud i el contacte.

/usuaris/signadorNom | Nom de l&#39;usuari que signa la sol·licitud.
/usuaris/signadorCorreu | Correu de l&#39;usuari que signa la sol·licitud. |
/usuaris/signadorTelefon | Telèfon de l&#39;usuari que signa la sol·licitud. |
/usuaris/signadorNIF | NIF de l&#39;usuari que signa la sol·licitud. |
/usuaris/contacteNom | Nom de l&#39;usuari de contacte. |
/usuaris/contacteCorreu | Correu de l&#39;usuari de contacte. |
/usuaris/contacteTelefon | Telèfon de l&#39;usuari de contacte. |
/ordreInsercio/exempcioPagament | Bloc de dades corresponent a la informació de d&#39;exempció de pagament. Cal informar-lo quan l&#39;usuari sol·licita publicar un anunci gratuït.

/exempcioPagament/lleiExempcio | Identificació de la llei que regula l&#39;exempció del pagament.

/exempcioPagament/articleExempcio | Identificació de l&#39;article que regula l&#39;exempció del pagament.

/ordreInsercio/pagament | Bloc de dades corresponent a la informació de pagament.

/pagament/taxa | Taxa aplicada:- 1: taxa normal.
- 2: taxa urgent.

/pagament/pagamentTercer | Bloc de dades corresponent a la informació de pagament quan el pagament va a càrrec d&#39;un tercer i no de l&#39;organisme que sol·licita la publicació.

/pagamentTercer/nom | Nom o raó social del pagador. 
/pagamentTercer/NIF | NIF del pagador. 
/pagamentTercer/adreca | Adreça del pagador. 
/pagamentTercer/codiPostal | Codi postal del pagador. 
/pagamentTercer/poblacio | Població del pagador. 
/pagamentTercer/telefon | Telèfon del pagador. 
/pagamentTercer/correu | Correu electrònic del pagador. 
/ordreInsercio/condicioPublicacio | Bloc de dades corresponent a les condicions de publicació del document.
 Per més detalls sobre les condicions de publicació admeses en base al mode de pagament consulteu l&#39;apartat 3.1.1.2 d&#39;aquest document.

/condicioPublicacio/condicio | Condició de publicació:
- 0: en qualsevol data
- 1: urgent (només disponible si està exempt de pagament
- 2: data concreta (segons element data)
- 3: no abans de la data de publicació especificada (a l&#39;element data)
- 4: juntament amb un altre document (identificat per identificadorRelacionat)
- 5: després d&#39;un altre document (identificat per identificadorRelacionat)

/condicioPublicacio/identificadorRelacionat | Identificador del document en el sistema origen relacionat.
 EACAT no realitzarà cap tipus de validació d&#39;existència de les publicacions referenciades.

/condicioPublicacio/data | Data de condició de publicació.

/boe | Bloc de dades corresponent a la informació específica de publicació al BOE, en cas que també es vulgui publicar l&#39;anunci al Tablón Edictal Único.

/boe/dir3 |

/boe/lgt | S si l&#39;anunci s&#39;ha de publicar conforme el disposat a l&#39;article 112 de la Ley 58/2003 (Ley General Tributaria).

/boe/materia | Matèria. Vegeu annex Matèries BOE. |
/boe/materia@id | Identificador de matèria. Vegeu annex Matèries BOE. |
/boe/procediment | Text lliure que permet construir de manera automatitzada el títol de l&#39;anunci BOE. No ha de contenir dades de caràcter personal.
 El títol generat tindrà el següent format:
[entitat emisora]. Anuncio de notificación de [data] en procedimiento[s] [procediment].
 L&#39;atribut plural (S/N) indicarà si cal emprar-se el plural en la paraula procediment.
 La data que s&#39;emprarà a l&#39;hora de composar el títol de l&#39;anunci és la informada a //document/data.

/boe/procediment@plural |
/boe/formaPublicacio | Forma de publicació:
- E: extracte
- I: Íntegra
/boe/peuSignatura/localitat | Població on té lloc la signatura.

/boe/peuSignatura/signador | Càrrec i nom i dos cognoms del signatari. En els casos d&#39;actuació administrativa automatitzada pot consistir únicament en la identificació de l&#39;organisme o unitat signatària. En cas d&#39;alteració de la competència caldrà incloure les referències corresponents.