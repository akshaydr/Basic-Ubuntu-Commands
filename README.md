# Basic-Ubuntu-Commands
Basic commands usually helpful when ubuntu is set up newly.

### Permanently adding chmod to a device
```
sudo chmod 777 /dev/ttyUSB0
sudo usermod -aG dialout username
```
Replace username with your username and then logout and login to apply the changes.

### Terminal History Up Arrow setup
```
gedit ~/.bashrc
bind '"\e[A": history-search-backward'
bind '"\e[B": history-search-forward'
source ~/.bashrc
```
### Bind USB device under a static name

Add some udev rules. 
Edit the `/etc/udev/rules.d/10-local.rules` to contain:
```
ACTION=="add", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", SYMLINK+="my_uart"
```
Check for the variables of your device by running
```
udevadm info -a -p  $(udevadm info -q path -n /dev/ttyUSB0)
```

### Setting up a wireless static IP on RaspberrPi
Run the following command on a terminal
```
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```
Replace the text with the text below. Change ssid to your hotspot SSID. and psk with your hotspot password. Rest remain same
```
network={
ssid="username"
psk="password"
proto=RSN
key_mgmt=WPA-PSK
pairwise=CCMP
auth_alg=OPEN
}
```
Save the file and run the following command on a new terminal.
```
sudo nano /etc/network/interfaces
```
Replace the text with the text below. Change the address to desired static IP address.
```
# /etc/network/interfaces

auto wlan0

iface lo inet loopback
iface eth0 inet dhcp

allow-hotplug wlan0
iface wlan0 inet static
address 192.168.225.2
netmask 255.255.255.0
gateway 192.168.225.1
wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
iface default inet dhcp
```
Restart RaspberryPi.
