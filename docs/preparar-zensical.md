# Preparar Zensical i provar-lo en local

Zensical transforma Markdown en HTML, CSS i JavaScript. Per defecte, `zensical build` escriu el resultat a `site/`. [Referència de construcció](https://zensical.org/docs/usage/build/).

## 1. Prepara els fitxers

Una estructura senzilla és:

```text
repositori/
├── zensical.toml
├── docs/
│   ├── index.md
│   └── img/
├── dockerfile
└── .dockerignore
```

Adapta les rutes si el projecte utilitza una altra estructura; no cal reorganitzar un projecte que funciona.

## 2. Entén el Dockerfile

El [dockerfile de referència](https://github.com/IesElJust/garage_landing_page/blob/main/dockerfile) utilitza dues etapes. Aquest és el mateix procés amb comentaris resumits:

```dockerfile title="dockerfile"
# Genera el web
FROM python:3.12-slim AS builder
WORKDIR /app
RUN pip install --no-cache-dir zensical
COPY . .
RUN zensical build

# Serveix el resultat
FROM nginx:alpine
COPY --from=builder /app/site/ /usr/share/nginx/html/
EXPOSE 80
```

| Instrucció | Funció |
| --- | --- |
| Primer `FROM` | Prepara Python per executar Zensical. |
| `WORKDIR /app` | Crea i selecciona el directori de treball dins de la imatge. |
| `RUN pip install ...` | Instal·la Zensical durant la construcció. |
| `COPY . .` | Copia els fitxers del context a `/app`. |
| `RUN zensical build` | Genera `/app/site/` amb la sortida predeterminada. |
| Segon `FROM` | Comença la imatge final amb Nginx. |
| `COPY --from=builder ...` | Copia el web generat a la carpeta pública de Nginx. |
| `EXPOSE 80` | Declara el port intern previst; no publica un port del VPS per si mateix. |

`/app` és una carpeta dins de la construcció Docker: no has de crear-la al repositori. La imatge final conté Nginx i el web; Python es queda a l’etapa de construcció.

!!! tip "Versions reproduïbles"

    L’exemple instal·la la versió de Zensical disponible en construir. Per a un projecte estable, fixa la versió provada en les dependències. Revisa també les versions de les imatges base quan les actualitzes.

## 3. Exclou fitxers innecessaris

Crea un `.dockerignore` a l’arrel:

```text title=".dockerignore"
.git
.cache
site
.venv
venv
```

Així no es copia el resultat local ni l’entorn Python. Afegeix també `site/` al `.gitignore` si encara no hi és: és un resultat generat.

## 4. Prova el procés al teu ordinador

Amb Docker instal·lat i en funcionament, executa des de l’arrel del repositori:

```sh
docker build -f dockerfile -t zensical-local .
```

`-f dockerfile` indica el nom en minúscules de l’exemple. Si es diu `Dockerfile`, pots ometre aquesta opció. El punt final indica el context de construcció.

Quan acabe, executa:

```sh
docker run --rm -p 127.0.0.1:8080:80 --name zensical-prova zensical-local
```

Obri **http://localhost:8080**. El port `8080` del teu ordinador es connecta al `80` del contenidor. Si està ocupat, utilitza un altre port local, com `8081`.

Revisa pàgines, imatges i navegació. Prem **Ctrl+C** per aturar-lo; `--rm` suprimeix el contenidor, però conserva la imatge. Després de modificar els documents, torna a construir i executar per veure els canvis.

## 5. Puja els canvis

Comprova que la branca de GitHub conté els documents, la configuració, el Dockerfile i els fitxers auxiliars necessaris. Continua amb [el desplegament a Coolify](web-estatica.md).
