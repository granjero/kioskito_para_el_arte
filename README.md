# Kioskito Para El Arte

## Este documento sirve para instalar un "kiosk" que abre un navegador maximizado.

### Sistema Operativo

Instalar debian sin gestor de ventanas. La imagen se puede descargar de [acá para pc](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-11.2.0-amd64-netinst.iso) y de [acá para raspberry](https://downloads.raspberrypi.org/raspios_lite_armhf/images/raspios_lite_armhf-2022-01-28/2022-01-28-raspios-bullseye-armhf-lite.zip)
El nombre de usuario que se use va en el archivo de configuración de lightdm.

### Aplicaciones

Instalar: 
  - xorg 
  - chromium 
  - openbox 
  - lightdm
  - openssh-server
  - unclutter

`$ su - root`

`$ apt -y install xorg chromium openbox lightdm openssh-server unclutter`

### Configuraciones

- Autologin 

Editar el script lightdm config /etc/lightdm/lightdm.conf para el autologin. Sólo debe contener esto:
```
[SeatDefaults]
autologin-user=nombreDeUsuarioUtilizadoEnLaInstalacion
user-session=openbox
xserver-command=X -nocursor
```

- Autostart

Si no existe crear el directorio de configuracion de openbox para el usuario nombreDeUsuarioUtilizadoEnLaInstalacio

`mkdir ~/.config/openbox`

Crear el archivo `autostart` dentro del directorio openbox con el siguiente contenido:

```
#!/bin/bash

@unclutter -idle 0.1 &

chromium \
    --no-first-run \
    --disable \
    --disable-translate \
    --disable-infobars \
    --disable-suggestions-service \
    --disable-save-password-bubble \
    --start-maximized \
    --kiosk "http://www.google.com" &

```
