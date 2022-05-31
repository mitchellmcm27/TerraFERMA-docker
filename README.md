Provides `mitchellmcm27/terraferma` image, based on `TerraFERMA/dev` but with `arm64` support added.

## MacOS (M1 chip)

Download & install XQuartz

Open XQuartz preferences, go to Security tab, check "Allow connections from network clients" (only needs to be done once)

Restart or quit XQuartz

`xhost +localhost`

`docker run -it -e DISPLAY=host.docker.internal:0 -v /tmp/.x11_unix:/tmp -v $PWD:/home/tfuser/shared mitchellmcm27/terrafirma:master`

Inside the container

`sudo chown -R tfuser /tmp`

Note: it seems that mapping the volume `-v /tmp/.x11_unix:/tmp` may not be necessary (diamond GUI still works), in which case it is also not necessary to `sudo chown -R tfuser /tmp` inside the container.

## Windows Subsystem for Linux (WSL)

Install WSL GUI (WSLg) via WSL Preview from the Microsoft store

Follow the instructions here to set up Ubuntu (https://github.com/microsoft/wslg)

Install Docker Desktop for Windows and make sure the setting `Use the WSL 2 based engine` is enabled

Run Ubuntu and `cd` to your working directory, e.g.: `cd /mnt/d/documents/developer/sz`

Within Ubuntu, run the Docker container: `docker run -it --rm -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v $PWD:/home/tfuser/shared terraferma/dev`

Run `diamond` within the container to make sure the GUI works

