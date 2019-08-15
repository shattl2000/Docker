FROM ubuntu:16.04

RUN apt-get update \
        && DEBIAN_FRONTEND=noninteractive apt-get upgrade -y \
        && DEBIAN_FRONTEND=noninteractive apt-get install -y \
            dbus \
            dbus-x11 \
            xorg \
            xserver-xorg-legacy \
            xinit \
            xterm \
            chromium-browser \
    && rm -rf /var/lib/apt/lists/*

RUN sed -i "s/allowed_users=console/allowed_users=anybody/;$ a needs_root_rights=yes" /etc/X11/Xwrapper.config

ARG user=user
ARG uid=1000
RUN useradd ${user} -u $uid -m -G adm,dialout,cdrom,sudo,audio,dip,video,plugdev -s /bin/bash

RUN echo '#!/bin/bash' > /root/.xinitrc && \
    echo '/usr/bin/chromium-browser --no-sandbox %U --kiosk --window-size=1366,768 --app=http://ya.ru' >> /root/.xinitrc

RUN echo 'Section "ServerLayout"' > /usr/share/X11/xorg.conf.d/10-monitor-local.conf && \
    echo 'Identifier "ServerLayout0"' >> /usr/share/X11/xorg.conf.d/10-monitor-local.conf && \
    echo 'Option "BlankTime"  "0"' >> /usr/share/X11/xorg.conf.d/10-monitor-local.conf && \
    echo 'Option "StandbyTime" "0"' >> /usr/share/X11/xorg.conf.d/10-monitor-local.conf && \
    echo 'Option "SuspendTime" "0"' >> /usr/share/X11/xorg.conf.d/10-monitor-local.conf && \
    echo 'Option "OffTime" "0"' >> /usr/share/X11/xorg.conf.d/10-monitor-local.conf && \
    echo 'EndSection' >> /usr/share/X11/xorg.conf.d/10-monitor-local.conf && \
    echo ' ' >> /usr/share/X11/xorg.conf.d/10-monitor-local.conf && \
    echo 'Section "Monitor"' >> /usr/share/X11/xorg.conf.d/10-monitor-local.conf && \
    echo 'Identifier    "Monitor0"' >> /usr/share/X11/xorg.conf.d/10-monitor-local.conf && \
    echo 'Option        "DPMS" "false"' >> /usr/share/X11/xorg.conf.d/10-monitor-local.conf && \
    echo 'EndSection' >> /usr/share/X11/xorg.conf.d/10-monitor-local.conf

CMD /usr/bin/startx -- vt7




