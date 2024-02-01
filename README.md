[Official docs](https://terraferma.github.io/)

[Wiki](https://github.com/terraferma/terraferma/wiki)

[Installation](https://github.com/terraferma/terraferma/wiki/Installation#docker)

## MacOS (M1 chip)

Download & install XQuartz

Open XQuartz preferences, go to Security tab, check "Allow connections from network clients" (only needs to be done once)

Restart or quit XQuartz

`xhost +localhost`

`docker run -it -e DISPLAY=host.docker.internal:0 -v /tmp/.x11_unix:/tmp -v $PWD:/home/tfuser/shared terraferma/dev`

Inside the container

`sudo chown -R tfuser /tmp`

Note: it seems that mapping the volume `-v /tmp/.x11_unix:/tmp` may not be necessary (diamond GUI still works), in which case it is also not necessary to `sudo chown -R tfuser /tmp` inside the container.

## Windows Subsystem for Linux (WSL)

WSL GUI (WSLg) is now included in the WSL installation from the Microsoft Store (see https://github.com/microsoft/wslg).

If using Docker Desktop for Windows, make sure the setting `Use the WSL 2 based engine` is enabled.

If using Docker inside of WSL, just make sure it's ready to go.
You can either interact with TerraFerma through a terminal, or using remote containers in VS Code.

### Terminal

Within WSL `cd` to your working directory, e.g.: `cd /mnt/d/documents/developer/working`

Run the Docker container: `docker run -it --rm -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v $PWD:/home/tfuser/shared terraferma/dev`. This command passes the `DISPLAY` environment variable to the container, and binds an X11 directory that is required by the display.

Run `diamond` within the container to verify the GUI works.

### VS Code (version 1.85.2)

As of now, the Linux image used by TerraFerma is only supported by VS Code versions <1.86 (e.g., 1.85.2 is good).
Download older versions in "portable mode" (.zip or .tar.gz) so that your regular installation of VS Code is not affected.

Older versions are available here and can be downloaded by the appropriate URL: https://code.visualstudio.com/docs/supporting/faq#_previous-release-versions

For Windows x64, the URL to download the .zip file is: https://update.code.visualstudio.com/1.85.2/win32-x64-archive/stable

For macOS (Apple Silicon), the URL to download the .tar.gz file is: https://update.code.visualstudio.com/1.85.2/darwin-arm64/stable

Instructions for installing the portable version of VS Code are here https://code.visualstudio.com/docs/editor/portable .
Note that in Windows, this cannot be unzipped to Program Files or other system-wide directories. Instead, unzip the folder into the AppData directory, i.e., `C:\Users\{username}\AppData\Local\Programs\`

In Windows (not WSL or Docker), open your working directory in VS Code 1.85.2 and create a simple Dockerfile:

```dockerfile
FROM terraferma/dev
ENV DISPLAY=$DISPLAY
USER tfuser
```

Choose to "Reopen in container", choose "existing Dockerfile", and it should work, including the `diamond` GUI.
