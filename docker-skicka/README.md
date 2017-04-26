# docker-skicka

Backup files to Google Drive via [skicka](https://github.com/google/skicka)

This image is based on the `golang:1-alpine`.
Image size: `445 MB`.

**Recommend** to use the [docker-skicka-min](../docker-skicka-min) image instead (Smaller size, only `12.3 MB`).


#### Usage
```sh
docker run -it --rm kairyou/docker-skicka # list commands
docker run -it --rm kairyou/docker-skicka help # skicka help

# setup
docker run -it --rm -v $HOME/.skicka-config:/root kairyou/docker-skicka init # skicka init
docker run -it --rm -v $HOME/.skicka-config:/root kairyou/docker-skicka -no-browser-auth ls # authorize skicka
# Copy and paste the URL to your browser, authorize skicka, then copy the `verification code` from your browser to the terminal.
# It will update tokenCacheFile: `/root/.skicka.tokencache.json`

# usage
docker run -it --rm -v $HOME/.skicka-config:/root -v $PWD:/backup kairyou/docker-skicka ls / # list files
docker run -it --rm -v $HOME/.skicka-config:/root -v $PWD:/backup kairyou/docker-skicka mkdir /tmp # create folder

docker run -it --rm -v $HOME/.skicka-config:/root -v $PWD:/backup kairyou/docker-skicka upload ./test.txt /tmp/t.txt # upload file
docker run -it --rm -v $HOME/.skicka-config:/root -v $PWD:/backup kairyou/docker-skicka cat /tmp/t.txt # get file contents

docker run -it --rm -v $HOME/.skicka-config:/root -v $PWD:/backup kairyou/docker-skicka download /tmp/t.txt tmp.txt # download file to `/root` dir
docker run -it --rm -v $HOME/.skicka-config:/root -v $PWD:/backup kairyou/docker-skicka rm -r /tmp # remove file or folder
```

<!-- ##### Development -->
<!-- docker build --tag kairyou/docker-skicka . -->
