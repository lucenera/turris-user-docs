---
board: mox
---
# First setup of Turris MOX

## Before you start

{! basics/first-setup/mox_first_setup_warning.md !}

## Connecting cables

As MOX is really modular and therefore what is LAN and what is WAN side could
be a little bit tricky. Decision adheres to the following rules.

* If MOX has just one Ethernet port it is LAN
* If MOX has SFP, SFP is WAN and the rest of ports is LAN (including
  Ethernet port next to the power supply on MOX A)
* If it has switch(es) and no SFP, then all ports in switch are LAN and the
  port next to the power source on MOX A is WAN

When setting up your MOX, connect the cable from your Internet service provider
to WAN port and connect just your trusted device to LAN. **There is no password
during initial setup**. To eliminate potential security risks, setup your MOX
first, go through the update procedure and connect other untrusted devices only
afterwards.

!!! tip
    There is also a way to configure Turris Mox over Wi-Fi by using [configuration
    file and USB drive](./ethernetless.md).

### One Ethernet port device

The trickiest case is if you have **only one Ethernet port**. Therefore we
created a [special guide](mox_cpu_only.md) for the case with just one Ethernet
port such as MOX Start, MOX Pocket Wi-Fi or MOX Power Wi-Fi.

## Entering guide

Once you have all cables connected, you can power up your MOX by connecting the
power supply. Wait for your MOX to boot up. During boot LED will shine red and
once booted up, it will start blinking in heartbeat pattern
(blink-blink-pause).

**First boot can take a while**. During that, MOX detects hardware and decides
what is LAN and what is WAN based on your hardware configuration as described
above. It also tries to detect running DHCP server on LAN side and if it finds
one, it will switch itself into DHCP client mode. If it doesn't find one, it
will configure itself as DHCP server.

!!! tip
	If you have a working zero-conf on your computer, you can access your
    router via <http://turris.local> address.

When booted, you can access the first-run wizard by using a web browser and
entering as URL address of your router. In case of MOX running as DHCP server, web
interface will be at <http://192.168.1.1>.

## First setup without Ethernet

These days it is common that laptops do not have Ethernet socket and that can make
initial configuration of Turris router pretty complicated. Alternative initial
configuration was added in Turris OS 5.2.0. It uses configuration file on USB
flash drive to set password for web configuration interface and to enable Wi-Fi.

Configuration file is in [JSON](https://en.wikipedia.org/wiki/JSON) file format.
You can use following example as a base for your configuration file.
```
{
	"foris_password": "ForisPassword_ChangeThis!",
	"wireless": {
		"ssid": "TurrisConfigWifi",
		"key": "WiFiPassword_ChangeThis!"
	}
}
```
Make sure that you change all passwords!

Save your configuration file to file named `medkit-config.json` to root directory
of USB drive. Following file systems are supported: _ext4_, _Btrfs_, _XFS_ and
_FAT32_.

With prepared USB drive you can connect it to router and perform either [factory
reset](../../hw/omnia/rescue_modes.md#rollback-to-factory-reset) (only if 
[factory version](../tos_versions/#versions-of-turris-os-provided-from-factory) of
your router is Turris OS 5.2.0 or newer) or [flash via
USB](../../hw/omnia/rescue_modes.md#re-flash-router). Note that flash via USB is
highly suggested as factory version of Turris OS in your device might not support
this feature. It also removes possibility of exploit of old security holes.

Configuration is applied on first boot of device (your USB drive has to be
connected at that time). You should eventually be able to connect device you plan
to use for configuration to Wi-Fi network with name as you set (`ssid`). It is
protected by password you set (`key`). Now you are connected to router's LAN
network and you can continue by accessing web configuration interface as described
at the beginning of this article.

USB drive can be safely removed when you access router's configuration interface.
