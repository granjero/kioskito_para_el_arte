# Kioskito Para El Arte

## Este documento sirve para instalar un "kiosk" que abre un navegador maximizado.

### Sistema Operativo

Instalar debian sin gestor de ventanas. La imagen se puede descargar de [acá para pc](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-11.2.0-amd64-netinst.iso) y de [acá para raspberry](https://downloads.raspberrypi.org/raspios_lite_armhf/images/raspios_lite_armhf-2022-01-28/2022-01-28-raspios-bullseye-armhf-lite.zip)

El nombre de usuario utilizado en la instalación será utilizado en el archivo de configuración de lightdm.



### Aplicaciones

Instalar: 
  - xorg 
  - firefox 
  - openbox 
  - lightdm
  - openssh-server

`$ su - root`

`# apt -y install xorg firefox-esr openbox lightdm openssh-server`


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

firefox --kiosk "file:///home/path_to_the_arte" &

```

- Boot "silencioso"

Editar `/etc/default/grub` 

```
GRUB_DEFAULT=0
GRUB_TIMEOUT=0
GRUB_DISTRIBUTOR=`lsb_release -i -s 2> /dev/null || echo Debian`
GRUB_CMDLINE_LINUX_DEFAULT="quiet loglevel=0 vt.global_cursor_default=0 splash"
GRUB_CMDLINE_LINUX=""
```
`# update-grub`


TODO

plymouth

