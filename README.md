### 腾达U9 无线网卡 UBUNTU16.04驱动
```
mkdir -p ~/build
cd ~/build
git clone https://github.com/zshiningstar/TengDa_U9.git
```
```
cd TengDa_U9
make
sudo make install
```
```
ls /lib/modules/$(uname -r)/kernel/drivers/net/wireless/realtek/rtl8821cu
* 出现如下则说明安装成功
8821cu.ko
```
```
lsusb
* 列表会出现
Bus 001 Device 006: ID 0bda:1a2b Realtek Semiconductor Corp.
```
```
sudo usb_modeswitch -KW -v 0bda -p 1a2b
```
### 永久权限
```
sudo gedit /lib/udev/rules.d/40-usb_modeswitch.rules
在结束行之前附加LABEL="modeswitch_rules_end"以下内容：
* Realtek 8211CU Wifi AC USB
ATTR{idVendor}=="0bda", ATTR{idProduct}=="1a2b", RUN+="/usr/sbin/usb_modeswitch -K -v 0bda -p 1a2b"
```

