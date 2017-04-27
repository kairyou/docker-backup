# docker-skicka-min

Backup files to Google Drive via [skicka](https://github.com/google/skicka)

This image is based on the `alpine:3.5`.
Image size: `12.9 MB`.

#### Usage
```sh
docker run -it --rm kairyou/docker-skicka-min # list commands
docker run -it --rm kairyou/docker-skicka-min help # skicka help

# setup
docker run -it --rm -v $HOME/.skicka-config:/root kairyou/docker-skicka-min init # Initialize the configuration
docker run -it --rm -v $HOME/.skicka-config:/root kairyou/docker-skicka-min -no-browser-auth ls # Google Authentication
# Copy and paste the URL to your browser, authorize skicka, then copy the `verification code` from your browser to the terminal.
# It will update tokenCacheFile: `.skicka.tokencache.json`

# usage
docker run -it --rm -v $HOME/.skicka-config:/root kairyou/docker-skicka-min ls / # list files
docker run -it --rm -v $HOME/.skicka-config:/root kairyou/docker-skicka-min mkdir /tmp # create folder

docker run -it --rm -v $HOME/.skicka-config:/root kairyou/docker-skicka-min cat /tmp/t.txt # get file contents
docker run -it --rm -v $HOME/.skicka-config:/root kairyou/docker-skicka-min rm -r /tmp # remove file or folder

docker run -it --rm -v $HOME/.skicka-config:/root -v $PWD:/backup kairyou/docker-skicka-min upload ./test.txt /tmp/t.txt # upload file
docker run -it --rm -v $HOME/.skicka-config:/root -v $PWD:/backup kairyou/docker-skicka-min download /tmp/t.txt tmp.txt # download file to current(PWD) dir

# Shortcut for `skicka` command. Open `~/.zshrc` or `~./bashrc` add the following:
alias skicka='docker run -it --rm -v $HOME/.skicka-config:/root -v $(pwd):/backup kairyou/docker-skicka-min'
# skicka ls; skicka upload ./t.txt /tmp;
```

##### Development
*These are just some notes about development things.*

```sh
# Update the `skicka` executable from [kairyou/docker-skicka](github.com/kairyou/docker-backup/docker-skicka)
docker run -d --name="tmp" kairyou/docker-skicka;
docker cp tmp:/go/bin/skicka ./skicka; docker rm -f tmp;
# docker build --tag kairyou/docker-skicka-min .
```

##### Specify `client_id` and `clientsecret`
- [Enable Google Drive API](https://console.developers.google.com/apis/api/drive.googleapis.com/overview)
- [Create credentials](https://console.developers.google.com/apis/credentials/wizard?api=drive.googleapis.com)
    - Where will you be calling the API from:  `Other UI`
    - What data will you be accessing: `User data`
    - What credentials do I need:
    - Create an OAuth 2.0 client ID, name: `drive_client_1`
    - Product name shown to users: `google_drive`, Continue.
- Download credentials, copy `client_id` and `clientsecret` into `.skicka.config`.
- Google Authentication, `skicka -no-browser-auth ls`.
