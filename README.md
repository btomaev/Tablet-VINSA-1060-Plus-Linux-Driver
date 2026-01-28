 
# Linux Driver for VINSA 1060 Plus Drawing Tablet (V2)

Linux driver for the VINSA 1060 Plus drawing tablet with full pressure sensitivity and button support. Chipset: 08f2:6811

_(It would be interesting if someone has a Huion H1060p tablet and can test the driver to see if it works.)_

The [marvinbelfort](https://github.com/marvinbelfort/mx002_linux_driver) driver has been adapted and expanded for this graphics tablet, improving sensitivity and providing two modes of use: one mouse-like, which uses a smaller area of ​​the tablet and is also customizable according to preferences, and another tablet-like mode, which occupies the entire area and offers greater sensitivity for artistic drawing imitating the Windows driver.

## 📦 Installation
You need to have Rust installed previously.

Clone the repository
```bash
git clone https://github.com/btomaev/Tablet-VINSA-1060-Plus-Linux-Driver.git vinsa-1060-driver
```

Build the driver
```bash
cd vinsa-1060-driver
cargo build --release
chmod +x target/release/v1060p-driver
sudo cp target/release/v1060p-driver /usr/bin/
```

For Install udev rules
```bash
sudo cat <<EOF >> /etc/udev/rules.d/99-vinsa-tablet.rules
SUBSYSTEM=="usb", ATTR{idVendor}=="08f2", ATTR{idProduct}=="6811", MODE="0666"
SUBSYSTEM=="input", GROUP="input", MODE="0666"
KERNEL=="uinput", MODE="0666", GROUP="input"
EOF
```

Reload rules
```bash
sudo udevadm control --reload-rules
sudo udevadm trigger
```

## Configuration
Run v1060p-driver --config and adjust settings or edit `~/.config/v1060p-driver/settings.json`

## References
- [marvinbelfort](https://github.com/marvinbelfort) - Initial research
- [DIGImend/10moons-tools](https://github.com/DIGImend/10moons-tools) - Expanded mode enablement
- [alex-s-v/10moons-driver](https://github.com/alex-s-v/10moons-driver) - User-space driver approach
