# RTL88x2BU-Android-Drivers_rtl8812au

> Ready-to-compile RTL88x2BU/RTL8812AU drivers for Android — no source edits required; ideal for NetHunter

## 📋 Overview

This repository contains pre-configured RTL88x2BU and RTL8812AU wireless drivers specifically optimized for Android environments. These drivers are **ready to compile as kernel modules** without requiring any modifications to the source code, making them perfect for Android penetration testing distributions like Kali NetHunter.

## ✨ Features

- **Zero Configuration Required** - Compile directly without source modifications
- **Android Optimized** - Pre-configured for Android kernel environments
- **NetHunter Ready** - Tested and working with Kali NetHunter
- **Monitor Mode Support** - Full monitor mode and packet injection capabilities
- **Universal Compatibility** - Works with RTL88x2BU and RTL8812AU chipsets

## 🔧 Supported Chipsets

This driver supports wireless adapters based on the following Realtek chipsets:

- RTL8812AU
- RTL8822BU
- RTL8812BU
- RTL8822CU

## 📦 Prerequisites

Before compiling, ensure you have the following:

- Android kernel source code
- Cross-compilation toolchain for your target architecture
- Basic knowledge of kernel module compilation
- `make`, `gcc`, and kernel build essentials

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/ShorterKing/RTL88x2BU-Android-Drivers_rtl8812au.git
cd RTL88x2BU-Android-Drivers_rtl8812au
```

### 2. Set Environment Variables

```bash
export ARCH=arm64  # or arm, depending on your device
export CROSS_COMPILE=aarch64-linux-android-  # adjust for your toolchain
export KERNEL_DIR=/path/to/your/kernel/source
```

### 3. Compile the Driver

```bash
make -j$(nproc)
```

### 4. Install the Module

```bash
# Push to device
adb push 88x2bu.ko /sdcard/

# Load the module (requires root)
adb shell
su
insmod /sdcard/88x2bu.ko
```

## 🎯 NetHunter Integration

### Loading the Driver in NetHunter

```bash
# Copy module to system
cp 88x2bu.ko /system/lib/modules/

# Load module
insmod /system/lib/modules/88x2bu.ko

# Verify interface
ifconfig wlan1  # or your wireless interface name
```

### Enable Monitor Mode

```bash
# Bring interface down
ifconfig wlan1 down

# Set monitor mode
iwconfig wlan1 mode monitor

# Bring interface up
ifconfig wlan1 up
```

## 🛠️ Advanced Configuration

### Custom Compilation Options

Edit the `Makefile` to customize build options:

```makefile
CONFIG_PLATFORM_I386_PC = n
CONFIG_PLATFORM_ARM_ANDROID = y
CONFIG_POWER_SAVING = y
```

### Module Parameters

Load the module with custom parameters:

```bash
insmod 88x2bu.ko rtw_drv_log_level=4 rtw_led_ctrl=1
```

Common parameters:
- `rtw_drv_log_level` - Debug logging level (0-4)
- `rtw_led_ctrl` - LED control (0/1)
- `rtw_power_mgnt` - Power management (0/1/2)

## 🐛 Troubleshooting

### Module Fails to Load

```bash
# Check kernel logs
dmesg | tail -n 50

# Verify kernel version compatibility
uname -r
modinfo 88x2bu.ko
```

### Interface Not Appearing

```bash
# Check if module is loaded
lsmod | grep 88x2bu

# Check USB device recognition
lsusb
```

### Monitor Mode Issues

```bash
# Try alternative method
ip link set wlan1 down
iw dev wlan1 set type monitor
ip link set wlan1 up
```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the GPL-2.0 License - see the [LICENSE](LICENSE) file for details.

## ⚠️ Disclaimer

This driver is provided for educational and legitimate security testing purposes only. Users are responsible for ensuring compliance with local laws and regulations regarding wireless network testing and monitoring.

## 🙏 Acknowledgments

- Realtek for the original driver source code
- Kali NetHunter team for Android penetration testing framework
- The open-source community for continuous improvements

## 📞 Support

- **Issues**: Please use the [GitHub Issues](https://github.com/ShorterKing/RTL88x2BU-Android-Drivers_rtl8812au/issues) page

## 🔗 Related Projects

- [Kali NetHunter](https://github.com/ShorterKing/Nethunter-Kernel-Redmi5A-Riva)
- [RTW88-Android-Drivers](https://github.com/ShorterKing/RTW88-Android-Drivers)

---

**Note**: Always ensure you have proper authorization before testing on any wireless network. Unauthorized access to networks is illegal.

Made with ❤️ for the Android security community
