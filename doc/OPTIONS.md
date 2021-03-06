# USB Ninja
## Options File

The USB Ninja will first look to `/boot/usbninja/options.txt` but will fall back to `/lib/usbninja/config/options.txt` for its configuration file.
* If none is supplied, then the defaults listed here will be used instead.
* If there are any errors in `options.txt`, then the line is ignored and the default for that option it set instead.

### Structure of `options.txt`
The format of the file is very simple. Each option is set on a new line and options and values are separated by colons. If multiple values are permitted, then they are separated by commas.
**E.g.**
```
gadget: hid_payload, storage
manufacturer: Xcellerator
productname: Composite USB Device
```

### Settings available to every gadget
|Option|Description|Format|Default Value|
|-|-|-|-|
|`gadget`|The USB gadget(s) to be used|`gadget1, gadget2, etc`|`serial`|
|`post`|(Optional) An executable or script to be run after all the gadgets are setup (See below)|`file` or `/path/to/file`|none|
|`vendorid`|(Optional) The VID presented to the Host OS|`0x????` (two hex bytes)|`0x1d6b`|
|`productid`|(Optional) The PID prestented to the Host OS|`0x????` (two hex bytes)|`0x0104`|
|`serialnumber`|(Optional) The Serial Number of the emulated device|`????????????????` (16 hex characters)|`fedcba9876543210`|
|`manufacturer`|(Optional) The Manufacturer string reported to the Host OS|Up to 32 characters long|`Generic Corp`|
|`productname`|(Optional) The Product Name string reported to the Host OS|Up to 32 characters long|`USB Device`|

**Note:** The `post` script can be either an absolute path or a path relative to `/boot/usbninja/`.

**Note:** The `post` script must also have the executable bit set with `sudo chmod +x /path/to/file`.

### Settings available to certain gadgets
|Option|Gadget|Description|Format|Default Value|
|-|-|-|-|-|
|`delay`|[`hid_payload`](HID.md)|(Optional) The time in milliseconds to leave in between successive HID packets sent to the Host OS|Any integer|`0`|
|`eth_hostaddr`|[`ethernet`](ETHERNET.md)|(Optional) The MAC address of the device _supposedly_ on the other side of the USB-To-Ethernet adapter|`XX:XX:XX:XX:XX:XX`|`48:6f:73:74:50:43`|
|`eth_devaddr`|[`ethernet`](ETHERNET.md)|(Optional) The MAC address reported of the USB-To-Ethernet adapter itself|`XX:XX:XX:XX:XX:XX`|`42:61:64:55:53:42`|
|`storage`|[`storage`](STORAGE.md)|(Optional) An absolute path to an image file.|`/path/to/file`|`/lib/usbninja/storage.img`|
|`storage_ro`|[`storage`](STORAGE.md)|(Optional) Sets the mass storage device as read-only|yes/no|no|
