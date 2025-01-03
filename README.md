# astroberry-bullseye

Astroberry packages adapted for Debian 11 (bullseye)

Indi source packages grabbed from https://launchpad.net/~mutlaqja/+archive/ubuntu/ppa and recomplied under debian 11.

Compiled for arm64 arch.

armhf packages compiled for cpu armv6 (i.e rpi zero used for guding phd2)

## Installation
  * install raspios-bullseye-lite image
  * add user astrobbery / change user pi -> astroberry
  * update system:
        `sudo apt update && apt upgrade`
  * install dependencies:
  
        sudo apt install lxde lxsession lxterminal realvnc-vnc-server sysstat pixflat-icons gpsd gpsd-tools javascript-common libc-ares2 libexpat1-dev libjs-jquery libjs-sphinxdoc libjs-underscore libnginx-mod-http-geoip libnginx-mod-http-image-filter \
        libnginx-mod-http-xslt-filter libnginx-mod-mail libnginx-mod-stream libnginx-mod-stream-geoip libpython3-dev libpython3.9-dev nginx nginx-common nginx-core python-pip-whl \
        python3-bidict python3-blinker python3-bottle python3-dev python3-distutils python3-engineio python3-flask python3-flask-socketio python3-gevent python3-gevent-websocket \
        python3-greenlet python3-itsdangerous python3-jinja2 python3-jwcrypto python3-lib2to3 python3-pip python3-psutil python3-pyinotify python3-setuptools python3-simplejson \
        python3-socketio python3-websockify python3-werkzeug python3-wheel python3-zope.event python3.9-dev websockify \
        software-properties-common samba network-manager-gnome arc-theme fam qt5-qmltooling-plugins phonon4qt5-backend-gstreamer gstreamer1.0-plugins-ugly gpsd-clients chrony ldapscripts \
         libev4 libcfitsio9 libusb-1.0-0-dev
  * remove not-needed packages:
        `apt --purge remove gnome-\* parcellite`
  * download and install indi core packages from here (build for debian 11), rest indi\* should works from ubuntu "repository ppa:mutlaqja/indinightly" - browse repo https://launchpad.net/~mutlaqja/+archive/ubuntu/ppa/+packages, look for version \*ubuntu20.04.1 and filename ending \*arm64.deb (wget and dpkg -i).  
*If something don't work - let me know - I try to recompile for Debian 11 to meets its dependencies*
  * install astroberry-server-artwork_2.0.1+deb10u1_all.deb and other packages from astroberry repo - https://www.astroberry.io/repo/ - browse repo and grab arm64.deb file
  * install astroberry-server-wui_2.1.0_all.deb and astroberry-server-sysmod_2.0.7_all.deb from here (for new python libs and novnc)
  * other packages you need (:

## Source
  * astroberry-server-wui_2.1.0_all.deb  - https://github.com/sanlupkim/astroberry-server-wui
  * astroberry-server-sysmod_2.0.7_all.deb - https://github.com/sanlupkim/astroberry-server-sysmod
  * All deb-src avaliable at http://e2rd.piekielko.pl/debian/astroberry/deb-src/

## Problems
  * with vnc
    - pi config: set resolution to 1280x960
    - comment dtoverlay=vc4-fkms-v3d in /boot/config.txt
  * with lxde panel (just in half screen):
    remove desktop pager workspaces - https://forums.raspberrypi.com/viewtopic.php?t=337467

## Apps
### firecapture for 64bit system:
firecapture 2.7.14 has arm64 (aarch64) version and works without modification
 
### indi-pylibcamera
indi_pylibcamera debianized version 2.1.1

indi_pulibcamera used for Rpi cameras based on sony starvis imx290|462|327 - https://docs.arducam.com/Raspberry-Pi-Camera/Low-Light/Ultra-Low-Light-Starvis-Camera/

For long exposures (up to 15s) add to /etc/rc.local:
    
    v4l2-ctl -d /dev/v4l-subdev0 --set-ctrl=horizontal_blanking=64255

### oacapture
oacapture compiled for arm64 on rasbpian bullseye (11) - directly from https://github.com/openastroproject/openastro.git

### kstars
kstars depends on libstellarsolver - wget it from astroberry repo - https://www.astroberry.io/repo/pool/main/libs/libstellarsolver/libstellarsolver_2.3+deb11u1_arm64.deb

    wget https://www.astroberry.io/repo/pool/main/libs/libstellarsolver/libstellarsolver_2.3+deb11u1_arm64.deb
    sudo dpkg -i libstellarsolver_2.3+deb11u1_arm64.deb

OR  
add 64-bit repo astroberry for bullseye

    deb https://www.astroberry.io/repo/ **bullseye** main

as described in section "Advanced installation" on wiki page https://www.astroberry.io/docs/index.php?title=Astroberry_Server#Installation
