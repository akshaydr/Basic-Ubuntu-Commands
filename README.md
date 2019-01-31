# Basic-Ubuntu-Commands
Basic commands usually helpful when ubuntu is set up newly.

### Permanently adding chmod to a device
#### sudo chmod 777 /dev/ttyUSB0
#### sudo usermod -aG dialout username

## Terminal History Up Arrow setup

#### gedit ~/.bashrc
#### bind '"\e[A": history-search-backward'
#### bind '"\e[B": history-search-forward'
#### source ~/.bashrc

## Bind USB device under a static name

Add some udev rules. 
Edit the /etc/udev/rules.d/10-local.rules to contain:
#### ACTION=="add", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", SYMLINK+="my_uart"

Check for the variables of your device by running
#### udevadm info -a -p  $(udevadm info -q path -n /dev/ttyUSB0)

