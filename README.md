Provides `mitchellmcm27/terraferma` image, based on `TerraFERMA/dev` but with `arm64` support added.

## MacOS (M1 chip)

Download & install XQuartz

Open XQuartz preferences, go to Security tab, check "Allow connections from network clients" (only needs to be done once)

Restart or quit XQuartz

`xhost +localhost`

`docker run -it -e DISPLAY=host.docker.internal:0 -v /tmp/.x11_unix:/tmp -v $PWD:/home/tfuser/shared mitchellmcm27/terrafirma:master`

Inside the container

`sudo chown -R tfuser /tmp`
