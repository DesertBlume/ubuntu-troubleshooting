# Connect to Enterprise Wi-Fi Using nmcli on Ubuntu 24.04

This guide explains how to connect to an Enterprise Wi-Fi network (such as a university or workplace WPA2-Enterprise network) using `nmcli`, the command-line tool for NetworkManager.

---

## 1. Check your wireless adapter

List all network devices to find your wireless interface name.

```bash
nmcli device status
```

Look for your wireless adapter. It is usually named `wlan0` or something similar like `wlp3s0`. Note this name for the next steps.

---

## 2. Scan for available Wi-Fi networks

See which Wi-Fi networks are available and get the exact SSID.

```bash
nmcli device wifi list
```

Find the SSID you want to connect to. Make sure you have the correct name.

---

## 3. Add the Wi-Fi connection

Replace `wlan0` with your wireless adapter name.
Replace `MySSID` with the SSID of your network.
Replace `MyEnterpriseWiFi` with any name you want to use for this connection.

```bash
nmcli connection add type wifi ifname wlan0 con-name "MyEnterpriseWiFi" ssid "MySSID"
```

---

## 4. Configure Enterprise authentication settings

Modify the connection with your username and password for the network.

Replace `TheUserName` with your network username.
Replace `NetworkPassword` with your network password.

```bash
nmcli connection modify "MyEnterpriseWiFi" \
  802-1x.eap peap \
  802-1x.identity "TheUserName" \
  802-1x.phase2-auth mschapv2 \
  802-1x.password "NetworkPassword"
```

---

## 5. Set the key management to WPA-EAP

Enterprise Wi-Fi uses WPA-EAP.

```bash
nmcli connection modify "MyEnterpriseWiFi" wifi-sec.key-mgmt wpa-eap
```

---

## 6. Connect to the Wi-Fi network

Bring up the connection you created.

```bash
nmcli connection up "MyEnterpriseWiFi"
```

If your details are correct, you should now be connected to the network.

---

## Additional checks and tips

Show all saved connections:

```bash
nmcli connection show
```

Check the status of your devices:

```bash
nmcli device status
```

Bring up the connection again if needed:

```bash
nmcli connection up "MyEnterpriseWiFi"
```

If you run into problems, you can check the NetworkManager logs for details:

```bash
journalctl -u NetworkManager
```

---

This method works for many WPA2-Enterprise networks that use PEAP with MSCHAPv2 (common in universities and workplaces). Some networks may require additional certificate settings. Always follow your network administrator’s instructions if they provide extra configuration details.

---
