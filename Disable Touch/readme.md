# Disable Monitor Touch Screen in Wayland
```
cat /proc/bus/input/devices

I: Bus=0018 Vendor=2a94 Product=a811 Version=0100
N: Name="GGT7503:00 2A94:A811"
P: Phys=i2c-GGT7503:00
S: Sysfs=/devices/platform/AMDI0010:03/i2c-0/i2c-GGT7503:00/0018:2A94:A811.0005/input/input20
U: Uniq=
H: Handlers=mouse2 event5 
B: PROP=2
B: EV=1b
B: KEY=400 0 0 0 0 0
B: ABS=260800000000003
B: MSC=20
```
## Thats how i identify the touch driver



``` udevadm info -a -p /devices/platform/AMDI0010:03/i2c-0/i2c-GGT7503:00/0018:2A94:A811.0005/input/input20
```
#### Udevadm info starts with the device specified by the devpath and then
#### walks up the chain of parent devices. It prints for every device
#### found, all possible attributes in the udev rules key format.
#### A rule to match, can be composed by the attributes of the device
#### and the attributes from one single parent device.

```
echo 'SUBSYSTEM=="input", ATTR{id/vendor}=="2a94", ATTR{id/product}=="a811", ATTR{inhibited}="1"' > /etc/udev/rules.d/80-touchscreen.rules

udevadm control --reload && udevadm trigger
```
Or I can manually create a udev rule at "/etc/udev/rules.d/0-example.rules"
