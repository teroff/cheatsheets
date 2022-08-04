# Simple WPA Supplicant WiFi configuration
#
# Make sure you WPA supplicant is installed
#


# Make a copy the original wpa_supplicant.cofing file
cp /etc/wpa_supplicant/wpa_supplicant.conf /etc/wpa_supplicant.copy.conf

# Find your WiFi interface name
ip link

# Create a config file for you WiFi connection
wpa_passphrase SSID PASSWD > /etc/wpa_supplicant/wpa_supplicant-<WIFI_INTERFACE>.conf

# Add the following lines into the created file
ctrl_interface=/run/wpa_supplicant
update_config=1

# Start and enable all the required services

# DHCPCD
sudo systemctl enable dhcpcd.service
sudo systemctl start dhcpcd.service

# WPA Suplicant @ your WiFi Interface
sudo systemctl enable wpa_supplicant@<WIFI-INTERFACE>.service
sudo systemctl start wpa_supplicant@<WIFI-INTERFACE>.service

# Enjoy your WIFI starting automaticaly