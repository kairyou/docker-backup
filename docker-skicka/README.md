# docker-skicka

Backup files to Google Drive via [skicka](https://github.com/google/skicka)

This image is based on the `alpine:3.5`.
Image size: `12.9 MB`.

#### Usage
```sh
docker run -it --rm kairyou/docker-skicka # list commands
docker run -it --rm kairyou/docker-skicka help # skicka help

# setup
docker run -it --rm -v $HOME/.config/skicka:/root kairyou/docker-skicka init # Initialize the configuration
docker run -it --rm -v $HOME/.config/skicka:/root kairyou/docker-skicka -no-browser-auth ls # Google Authentication
# Copy and paste the URL to your browser, authorize skicka, then copy the `verification code` from your browser to the terminal.
# It will update tokenCacheFile: `.skicka.tokencache.json`

# usage

# list files
docker run -it --rm -v $HOME/.config/skicka:/root kairyou/docker-skicka ls /
# create folder
docker run -it --rm -v $HOME/.config/skicka:/root kairyou/docker-skicka mkdir -p /tmp

# get file contents
docker run -it --rm -v $HOME/.config/skicka:/root kairyou/docker-skicka cat /tmp/t.txt
# remove file or folder
docker run -it --rm -v $HOME/.config/skicka:/root kairyou/docker-skicka rm -r /tmp

# upload folder/file
docker run -it --rm -v $HOME/.config/skicka:/root -v $PWD:/backup kairyou/docker-skicka upload ./folder_or_file /tmp/folder_or_file
# download file to current(PWD) dir
docker run -it --rm -v $HOME/.config/skicka:/root -v $PWD:/backup kairyou/docker-skicka download /tmp/t.txt tmp.txt

# Shortcut for `skicka` command. Open `~/.zshrc` or `~./bashrc` add the following:
alias skicka='docker run -it --rm -v $HOME/.config/skicka:/root -v $(pwd):/backup kairyou/docker-skicka'
# skicka ls; skicka upload ./t.txt /tmp;
```

##### Development
*These are just some notes about development things.*

```sh
# Update the `skicka` executable from github.com/google/skicka
docker build . -f Dockerfile-go-skicka -t go-skicka;
docker run -d --name="tmp" go-skicka; docker cp tmp:/go/bin/skicka ./skicka;
docker rm -f tmp;docker rmi go-skicka;

# docker build --tag kairyou/docker-skicka .
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
