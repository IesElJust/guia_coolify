# Abans de començar

La guia utilitza un desplegament real de Zensical des de GitHub. Abans de seguir-lo, prepara:

- Compte al panell de Coolify i accés al projecte assignat.
- Repositori amb els documents i permís per pujar-hi els canvis si és teu.
- Branca que vols publicar.
- Dockerfile provat, seguint [la preparació local](preparar-zensical.md).
- Domini acordat amb l’administració o una adreça de proves autoritzada.

## Identifica el tipus de recurs

| Què vols publicar? | Què cal preparar? |
| --- | --- |
| Zensical o un generador de webs | Compilar i servir els fitxers resultants: és el nostre tutorial. |
| HTML, CSS i JavaScript ja generats | Es pot utilitzar el build pack Static; no necessita la compilació de Zensical. |
| Una API o aplicació amb servidor | Ordre d’inici, port intern i configuració pròpia del llenguatge. |
| Base de dades o servei amb dades | Emmagatzematge persistent, accés i còpies de seguretat. |
| Diversos serveis relacionats | Una definició Docker Compose pot descriure serveis, xarxes i volums. |

Tots són recursos, però no comparteixen els mateixos valors. El port 80 i el Dockerfile d’aquesta guia corresponen a Nginx: no els copies sense revisar-los en una altra aplicació.

La guia desenvolupa el cas de Zensical de principi a fi. La publicació d’APIs, bases de dades i altres serveis requereix les instruccions específiques de cada recurs; la taula ajuda a identificar què caldrà configurar.

## Qui fa cada tasca?

| Persona que publica | Administració del servei |
| --- | --- |
| Prepara codi, documents i Dockerfile. | Proporciona accés i assigna projecte i servidor. |
| Configura el recurs dins dels seus permisos. | Gestiona DNS, proxy, tallafoc i manteniment del VPS. |
| Desplega i comprova el web. | Defineix capacitat, persistència i política de còpies. |

No necessites accés SSH ni el compte d’OVH per seguir el tutorial. Per a un repositori privat, utilitza una integració Git o clau de desplegament autoritzada.

!!! warning "Contingut publicat"

    No incorpores contrasenyes, claus privades ni dades personals al repositori o a les captures. Els fitxers del web final, inclòs el JavaScript, són accessibles als visitants.

Continua amb [la preparació de Zensical](preparar-zensical.md).
