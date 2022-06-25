# Kioskito

## Uso este documento para instalar un "kiosk" que abre un navegador maximizado.

### Sistema Operativo

Instalar Debian sin gestor de ventanas. La imagen se puede descargar de [acá para pc](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-11.2.0-amd64-netinst.iso) y de [acá para raspberry](https://downloads.raspberrypi.org/raspios_lite_armhf/images/raspios_lite_armhf-2022-01-28/2022-01-28-raspios-bullseye-armhf-lite.zip)

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
autologin-user=arte
user-session=openbox
xserver-command=X -nocursor
```

- Autostart

Si no existe crear el directorio de configuracion de openbox para el usuario nombreDeUsuarioUtilizadoEnLaInstalacio

`mkdir ~/.config/openbox`

Crear el archivo `autostart` dentro del directorio openbox con el siguiente contenido:

```
#!/bin/bash

# screensaver
xset -dpms &
xset s off &

# firefox
firefox --kiosk "file:///home/arte/arte/index.html" &

```

- Boot "silencioso"

Editar `/etc/default/grub` 

```
GRUB_DEFAULT=0
GRUB_TIMEOUT=0
GRUB_DISTRIBUTOR=`lsb_release -i -s 2> /dev/null || echo Debian`
GRUB_CMDLINE_LINUX_DEFAULT="quiet loglevel=0 vt.cur_default=1 splash"
GRUB_CMDLINE_LINUX=""
```
`# update-grub`


- Plymouth

Descargar en /lib/firmware/i915 
https://anduin.linuxfromscratch.org/sources/linux-firmware/i915/


Como root correr

`# plymouth-set-default-theme -R lines`
