True Internet Bonding: 50 Mbps + 50 Mbps = 100 Mbps Single Connection
- <span style="white-space: nowrap;">True Internet bonding joins two ISP speeds (e.g., ISP-1 50 Mbps + ISP-2 50 Mbps) into 100 Mbps output on a single connection. Full 100 Mbps bandwidth works even in IDM for non-resumable downloads.</span>

## 🚀 Use Cases

- Uninterrupted browsing even if one ISP disconnects.
- All ISP connections use one single static public IP from the VPS.
- Create a zero-downtime smart home with bonded ISPs.
- Prevent CCTV downtime during ISP failures.
- Faster game patch updates with combined speed.
- Lower ping and jitter for smoother gameplay.
- Smooth video calls & meetings without interruptions.
- Faster buffering in single-link players like VLC and PotPlayer.
- Increased video streaming buffer speed.
- Bypass ISP throttling on YouTube, Netflix, Prime Video, etc.
- Boosted upload and download speeds.
- Single static public IP from the VPS.
- Non-resumable downloads use full combined bandwidth.
- No trading failures due to ISP drops.
- Mix fiber (FTTH) with wireless (5G) for balanced performance.
- Single TCP connection with combined throughput.
- Aggregate cellular data from different carriers.
- Maintain session continuity during ISP swaps.
- Automatically switch to working connection on failure.
- Full ISP bandwidth utilized even by a single user.

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
