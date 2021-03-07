# Valheim Dedicated Controls

## Connecting
### Windows
1. download `putty` and `puttygen`
    * [download page](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
1. Open puttygen
    1. change the number of bits to `4096`
    1. click generate and follow directions
    1. save public and private key somewhere safe
    1. send Ricky the contents of `Public key for pasing into OpenSSH...`
1. once Ricky has set up your pub key, the following will work
1. open putty
    1. on left sidebar, find `Connection -> SSH -> Auth`
    1. there is a field near the bottom asking for private key, click `browse`
    1. return to `Session` in your sidebar
    1. in host put `valheim@valheim.redig.me`
    1. name the session `Valheim` and save it
        1. note that if you accidentally hit save while `Valheim` is selected with the incorrect data, it will overwrite without prompt!
1. Once this is all set up, in the future you will only need open `putty`, select `Valheim`, click `Load`, and connect

## Once Connected
1. Basics
    * `cd` changes directory
    * `ls` list directory contents
    * `dc` alias for `docker-compose`
1. the server is located in `valheim-base`
1. run `cd valheim-base` and then run either `dc up -d` to start the server, or `dc down` to stop the server