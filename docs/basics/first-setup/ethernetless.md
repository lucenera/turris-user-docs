---
board: mox, omnia
competency: intermediate
---
# First setup of Turris Omnia and Mox without Ethernet LAN

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

With prepared USB drive you can connect it to router and perform either factory
reset ([Omnia](../../hw/omnia/rescue_modes.md#rollback-to-factory-reset),
[Mox](../../hw/mox/rescue_modes.md#rollback-to-factory-reset)) or flash via USB
([Omnia](../../hw/omnia/rescue_modes.md#re-flash-router),
[Mox](../../hw/mox/rescue_modes.md#re-flash-router)). Note that flash via USB is
highly suggested as factory version of Turris OS in your device might not support
this feature. It also removes possibility of exploit of old security holes.

!!! warning
	Configuration file as described here can be used with __factory reset__ only
	if router's [factory
	version](../tos_versions.md#versions-of-turris-os-provided-from-factory) is
	Turris OS 5.2.0 or newer.

Configuration is applied on first boot of device (the USB drive with configuration
file has to be connected at that time). You should eventually be able to connect
to Wi-Fi network with name as you set (`ssid`) device you plan to use for
configuration. Wi-Fi is protected by password you set (`key`). With that you are
connected to router's LAN network and you can continue by accessing web
configuration interface as described in your router's specific first setup guide.

USB drive can be safely removed when you access router's configuration interface.

Don't forget to remove configuration file from USB drive afterward or change all
auto-configured passwords to prevent password leakage when you reuse drive for
something else.
