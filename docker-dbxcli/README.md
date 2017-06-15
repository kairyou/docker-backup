# docker-dbxcli

Backup files to Dropbox via [dbxcli](https://github.com/dropbox/dbxcli)

This image is based on the `alpine`.
Image size: `18.3 MB`.


#### Usage
```sh
docker run -it --rm kairyou/docker-dbxcli # list commands

# setup
docker run -it --rm -v $HOME/.config/dbxcli:/root/.config/dbxcli kairyou/docker-dbxcli du # Dropbox Authentication
# Copy and paste the URL to your browser, authorize dbxcli-personal, then copy the `authorization code` from your browser to the terminal.
# It will creat Dropbox access token: `~/.config/dbxcli/auth.json`

# usage

# list files
docker run -it --rm -v $HOME/.config/dbxcli:/root/.config/dbxcli -v $(pwd):/backup kairyou/docker-dbxcli ls
# create folder
docker run -it --rm -v $HOME/.config/dbxcli:/root/.config/dbxcli kairyou/docker-dbxcli mkdir /tmp/test
# remove file or folder
docker run -it --rm -v $HOME/.config/dbxcli:/root/.config/dbxcli kairyou/docker-dbxcli rm -f /tmp

# upload file (Folder Upload is not support now. https://git.io/vHbIv)
docker run -it --rm -v $HOME/.config/dbxcli:/root/.config/dbxcli -v $PWD:/backup kairyou/docker-dbxcli put ./s.txt /tmp/d.txt
# download file to current(PWD) dir
docker run -it --rm -v $HOME/.config/dbxcli:/root/.config/dbxcli -v $PWD:/backup kairyou/docker-dbxcli get /tmpd.txt tmp.txt

# Search files
docker run -it --rm -v $HOME/.config/dbxcli:/root/.config/dbxcli -v $(pwd):/backup kairyou/docker-dbxcli search filename_keyword
# Move files
docker run -it --rm -v $HOME/.config/dbxcli:/root/.config/dbxcli -v $PWD:/backup kairyou/docker-dbxcli mv source.txt destination.txt

# Shortcut for `skicka` command. Open `~/.zshrc` or `~./bashrc` add the following:
alias dbxcli='docker run -it --rm -v $HOME/.config/dbxcli:/root/.config/dbxcli -v $(pwd):/backup kairyou/docker-dbxcli'
# dbxcli ls;
```

<!-- ##### Development -->
<!-- docker build --tag kairyou/docker-dbxcli . -->
