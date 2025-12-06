True Internet bonding joint two ISP internet speed example 50mbps (ISP-1) & 50 mbps (ISP-2) equals 100mbps output using single connection IDM full 100 mbps bandwidth.
Main Features:-
If we have a big file size download data with no resume facility with single connection link it can easily download with combined 100 mbps speed.

It's in two parts server part vps instalaltion and client part Raspberry-pi openwrt installation,

Installation server: check file "Debian-vps-script" & "AMD-x86-64-ubuntu-22.04-vps-script"
Sucessfull Installation: Get the Server Key, username, vps ip address.

Installation client: Download Edited Openwrt ( Flash using BalenaEtcher = https://bit.ly/4pIBwKU ),
RaspberryPi 4B link = https://bit.ly/44Cfkdf
RaspberryPi 5 Link = https://bit.ly/4rwfoVO

Insert keys to http://192.168.100.1/ > System > MPTCP > Settings Wizard > Add New Server > put server Key, username, vps ip address ,  Change "Multipath TCP" WAN-1 to Master & WAN-2 to enabled > Save & Apply > Reboot...

All Thanks for the vps ready script & openwrt edited os by "Ysurac" maintained by open-mptcp-router repos.
