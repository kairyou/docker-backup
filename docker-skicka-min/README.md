# docker-skicka-min

Backup files to Google Drive via [skicka](https://github.com/google/skicka)

This image is based on the `alpine:3.5`.
Image size: `12.3 MB`.

#### Usage
```sh
docker run -it --rm kairyou/docker-skicka-min # skicka commands
docker run -it --rm kairyou/docker-skicka help # skicka help
docker run -it --rm kairyou/docker-skicka -no-browser-auth ls # authorize skicka
```


###### Development
*These are just some notes about development things.*

Update the `skicka` executable from [docker-skicka](../docker-skicka)
```sh
docker run -d --name="tmp" kairyou/docker-skicka;
docker cp tmp:/go/bin/skicka ./skicka; docker rm -f tmp;
```
<!-- docker build --tag kairyou/docker-skicka-min . -->
