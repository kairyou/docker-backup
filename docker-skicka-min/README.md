# docker-skicka-min

Backup files to Google Drive via [skicka](https://github.com/google/skicka)

## Deprecated
This project was merged to [docker-skicka](../docker-skicka).

**Recommend** to use the [docker-skicka](../docker-skicka) image instead.

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

# list files
docker run -it --rm -v $HOME/.skicka-config:/root kairyou/docker-skicka-min ls /
# create folder
docker run -it --rm -v $HOME/.skicka-config:/root kairyou/docker-skicka-min mkdir -p /tmp

# get file contents
docker run -it --rm -v $HOME/.skicka-config:/root kairyou/docker-skicka-min cat /tmp/t.txt
# remove file or folder
docker run -it --rm -v $HOME/.skicka-config:/root kairyou/docker-skicka-min rm -r /tmp

# upload folder/file
docker run -it --rm -v $HOME/.skicka-config:/root -v $PWD:/backup kairyou/docker-skicka-min upload ./folder_or_file /tmp/folder_or_file
# download file to current(PWD) dir
docker run -it --rm -v $HOME/.skicka-config:/root -v $PWD:/backup kairyou/docker-skicka-min download /tmp/t.txt tmp.txt

# Shortcut for `skicka` command. Open `~/.zshrc` or `~./bashrc` add the following:
alias skicka='docker run -it --rm -v $HOME/.skicka-config:/root -v $(pwd):/backup kairyou/docker-skicka-min'
# skicka ls; skicka upload ./t.txt /tmp;
```
