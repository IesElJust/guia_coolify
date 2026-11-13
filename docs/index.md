# Guia de Coolify de l’institut

Aprèn a publicar webs i recursos a la instància de Coolify de l’institut, allotjada en un VPS d’OVH. La guia s’adreça a l’alumnat, el professorat i les persones participants del viver d’empreses.

## Què és Coolify?

Coolify permet gestionar desplegaments des d’un panell web: connectar repositoris, preparar aplicacions, posar-les en funcionament i consultar-ne l’estat. També permet gestionar bases de dades i altres serveis.

La nostra instància és **autoallotjada** (*self-hosted*): l’institut gestiona Coolify i el servidor virtual. El VPS està allotjat a OVH; no és l’ordinador de qui publica.

## Un exemple de principi a fi

Seguirem la publicació real del web de **JustHub Garage**, fet amb Zensical i allotjat en un repositori públic de GitHub. Les captures mostren com connectar-lo, revisar el Dockerfile, afegir dominis i comprovar el desplegament.

1. [Entén Coolify](conceptes.md): projectes, entorns, imatges, contenidors i xarxa.
2. [Revisa els requisits](abans-de-comencar.md) i qui s’encarrega de cada tasca.
3. [Prepara Zensical i prova’l en local](preparar-zensical.md).
4. [Desplega’l a Coolify, pas a pas](web-estatica.md).
5. [Configura domini, DNS i HTTPS](dominis.md), amb l’ajuda de l’administració.
6. [Publica actualitzacions i resol problemes](manteniment.md).

Els conceptes serveixen per a altres recursos. El tutorial pràctic es concentra en Zensical: cada API, base de dades o servei necessitarà la seua configuració d’execució i de dades.

!!! info "Accés al servei"

    Demana a la persona responsable l’adreça del panell, l’accés al projecte i el domini assignat. No cal disposar d’accés administratiu al VPS o a OVH.

Els noms dels controls es mantenen en anglès per trobar-los a les captures. Poden variar segons la versió instal·lada.

Més informació: [conceptes oficials de Coolify](https://coolify.io/docs/concepts).
