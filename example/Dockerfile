FROM resin/rpi-raspbian
MAINTAINER Ludovic Roguet <code@fourteenislands.io>

# Base layer
ENV ARCH=arm
ENV CROSS_COMPILE=/usr/bin/

# Install some packages
# #1:   20160803 - Added net-tools and nmap for https://home-assistant.io/components/device_tracker.nmap_scanner/
# #3:   20161021 - Added ssh for https://home-assistant.io/components/device_tracker.asuswrt/
# #8:   20170313 - Added ping for https://home-assistant.io/components/switch.wake_on_lan/
# #10:  20170328 - Added libffi-dev, libpython-dev and libssl-dev for https://home-assistant.io/components/notify.html5/
RUN apt-get update && \
    apt-get install --no-install-recommends build-essential python3-dev python3-pip \
      libffi-dev libpython-dev libssl-dev  net-tools nmap iputils-ping ssh \
      wget python && \
      apt-get clean &&     rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install node.js
RUN wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.xz && \
 tar -xvf https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.xz && \
 cd node-v6.10.2-linux-armv6l && cp -R * /usr/local/
 
# Install homebridge && plugins
RUN npm install -g --unsafe-perm homebridge && npm install -g homebridge-homeassistant

# Mouting point for the user's configuration
VOLUME /config

# Start Home Assistant
CMD [ "python3", "-m", "homeassistant", "--config", "/config" ]

# Install Home Assistant
RUN pip3 install pycrypto homeassistant==0.43.0
