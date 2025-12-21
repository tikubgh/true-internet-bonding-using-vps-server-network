True Internet Bonding: 50 Mbps + 50 Mbps = 100 Mbps Single Connection
- <span style="white-space: nowrap;">True Internet bonding joins two ISP speeds (e.g., ISP-1 50 Mbps + ISP-2 50 Mbps) into 100 Mbps output on a single connection. Full 100 Mbps bandwidth works even in IDM for non-resumable downloads.</span>

## Use Cases
- <span style="white-space: nowrap;">Keep uninterrupted browsing when one ISP disconnects.</span>
- <span style="white-space: nowrap;">All ISP connections use one single static public IP from the VPS.</span>
- <span style="white-space: nowrap;">Create a “zero downtime” smart home with bonded ISPs.</span>
- <span style="white-space: nowrap;">Prevent CCTV downtime.</span>
- <span style="white-space: nowrap;">Faster update patches on games.</span>
- <span style="white-space: nowrap;">Lower ping & jitter during gameplay.</span>
- <span style="white-space: nowrap;">Smooth video apps calls.</span>
- <span style="white-space: nowrap;">Smooth single link buffering speed for video players vlc, potplayer, etc.</span>
- <span style="white-space: nowrap;">Video stream buffer speed increased.</span>
- <span style="white-space: nowrap;">Bypass ISP throttling of YouTube,Netflix,Primevideo etc.</span>
- <span style="white-space: nowrap;">Upload/Download speed increased.</span>
- <span style="white-space: nowrap;">Static public ip address from vps.</span>
- <span style="white-space: nowrap;">Non-resume links used combined bandwidth.</span>
- <span style="white-space: nowrap;">No trade failure due to ISP drops.</span>
- <span style="white-space: nowrap;">Mix fixed-line (Fiber FTTH) with wireless (5G) for balanced performance.</span>
- <span style="white-space: nowrap;">Use a single TCP connection with combined throughput.</span>
- <span style="white-space: nowrap;">Aggregate cellular data from different carriers.</span>
- <span style="white-space: nowrap;">Maintain session continuity during ISP swap.</span>
- <span style="white-space: nowrap;">Automatically switch between connections if one fails.</span>
- <span style="white-space: nowrap;">All ISPs bandwidth fully utilized even by one user.</span>

## ✨ Main Features
- <span style="white-space: nowrap;">If we have a big file size download data with no resume facility with single connection link it can easily download with combined 100 mbps speed.</span>


## 🛠️ Installation Guide

### Server (VPS) Setup
- <span style="white-space: nowrap;">It's in two parts server part vps instalaltion and client part Raspberry-pi openwrt installation,</span>
- <span style="white-space: nowrap;">Installation server: check file "Debian-vps-script" & "AMD-x86-64-ubuntu-22.04-vps-script" Sucessfull Installation: Get the Server Key, username, vps ip address.</span>

### Client (Raspberry Pi) Setup
- <span style="white-space: nowrap;">Installation client: Download Edited Openwrt ( Flash using BalenaEtcher = <a href="https://bit.ly/4pIBwKU">https://bit.ly/4pIBwKU</a> ), RaspberryPi 4B link = <a href="https://bit.ly/44Cfkdf">https://bit.ly/44Cfkdf</a> RaspberryPi 5 Link = <a href="https://bit.ly/4rwfoVO">https://bit.ly/4rwfoVO</a></span>
- <span style="white-space: nowrap;">Insert keys to <a href="http://192.168.100.1/">http://192.168.100.1/</a> > System > MPTCP > Settings Wizard > Add New Server > put server Key, username, vps ip address , Change "Multipath TCP" WAN-1 to Master & WAN-2 to enabled > Save & Apply > Reboot...</span>

## 🙏 Credits
- <span style="white-space: nowrap;">All Thanks for the vps ready script & openwrt edited os by "Ysurac" maintained by open-mptcp-router repos.</span>
