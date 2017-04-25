# docker-skicka

Backup files to Google Drive via [skicka](https://github.com/google/skicka)

This image is based on the `golang:1-alpine`.
Image size: `445 MB`.

**Recommend** to use the [docker-skicka-min](../docker-skicka-min) image instead (Smaller size, only `12.3 MB`).


#### Usage
```sh
docker run -it --rm kairyou/docker-skicka # skicka commands
docker run -it --rm kairyou/docker-skicka help # skicka help
docker run -it --rm kairyou/docker-skicka -no-browser-auth ls # authorize skicka
```

<!-- ##### Development -->
<!-- docker build --tag kairyou/docker-skicka . -->
