# Actualitzacions i problemes habituals

## Publica una actualització de Zensical

1. Modifica Markdown, imatges o configuració.
2. Comprova el projecte en local; si has canviat dependències o el Dockerfile, prova també la construcció Docker.
3. Puja els canvis a la branca configurada, `main` en l’exemple.
4. Entra al recurs i prem **Deploy** o **Redeploy**, segons el seu estat.
5. Revisa el commit de l’historial i els registres.
6. Obri el web i comprova que apareix el contingut nou.

Coolify torna a preparar la imatge a partir del repositori, aprofitant la memòria cau de construcció quan pot. No cal pujar `site/` ni editar el contenidor. Reiniciar un contenidor existent no és el mateix que construir una versió amb codi nou.

El desplegament automàtic depèn de la integració Git i els webhooks configurats: un repositori públic no implica que estiga activat. El tutorial utilitza el desplegament manual.

Si disposes de `staging`, valida-hi els canvis abans de publicar-los en producció.

## Distingeix les comprovacions

| Indicador | Què et diu? |
| --- | --- |
| **DNS matches** | La comprovació DNS del panell coincideix; no garanteix que l’aplicació funcione. |
| Desplegament completat | El procés ha acabat; verifica també el contingut al navegador. |
| **Running (no healthcheck)** | El contenidor s’executa sense una comprovació de salut configurada. |

## Localitza la fase que falla

| Símptoma | Què has de revisar? |
| --- | --- |
| Check Repository falla | URL, branca, visibilitat i permisos de lectura. |
| No troba el Dockerfile | Nom exacte, majúscules i minúscules, branca i directori base. |
| Falla la instal·lació de Zensical | Primer error de `pip`, dependències i connectivitat durant la construcció. |
| Falla `zensical build` | Registres de construcció, configuració i fitxers que falten al repositori. |
| No existeix `/app/site/` en copiar | Que la compilació haja generat la sortida esperada; revisa `site_dir` i el directori de treball. |
| Apareix la portada predeterminada de Nginx | Que el resultat s’haja copiat a `/usr/share/nginx/html/` i s’estiga desplegant la imatge correcta. |
| Falten imatges o estils | Rutes, majúscules, fitxers pujats i configuració de l’URL del web. |
| El domini no respon | Estat del contenidor, port intern 80, DNS i encaminament del proxy. |
| Avís de certificat | Domini configurat, DNS i ports públics 80/443; consulta l’administració. |
| Es veu la versió anterior | Branca, commit desplegat, resultat de l’últim desplegament i memòria cau del navegador. |

Els **registres de desplegament** expliquen la descàrrega i la construcció. Els **registres d’execució** expliquen què passa amb el contenidor ja iniciat. Comença pel primer error rellevant, perquè sovint provoca els següents.

## Demana ajuda

Indica projecte, entorn, recurs, hora de l’error i commit que volies publicar. Afegeix el fragment rellevant dels registres després de comprovar que no conté secrets ni dades personals.

Abans d’eliminar un recurs per resoldre un error, revisa els registres i consulta la persona responsable. Si una actualització falla, identifica l’última revisió que funcionava abans de decidir com recuperar-la.

Referència: [diagnòstic de certificats de Coolify](https://coolify.io/docs/troubleshoot/dns-and-domains/lets-encrypt-not-working).
