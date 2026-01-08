# 🔥 **MeshCore-Cardputer-ADV** - **NOW ON M5Burner!** 🔥

**Search on M5Burner:**

`⚠️Experimental, might not work⚠️`
- `MeshCore-Cardputer-ADV M5Stack Cap LoRa868 version!!!!`
   
- `MeshCore-Cardputer-ADV DX-LR30 version (check github for more info)`

[![Buy Me a Coffee](https://img.buymeacoffee.com/button-api/?text=Buy%20me%20a%20coffee&emoji=☕&slug=Stachu&button_colour=ff8800&font_colour=000000&font_family=Lato&outline_colour=000000&coffee_colour=FFDD00)](https://buymeacoffee.com/Stachu)

Enhanced TFT user interface for MeshCore mesh networking firmware, optimized for M5Stack Cardputer-Adv.

![MeshCore-Cardputer-ADV](docs/images/title.JPG)
*Custom TFT UI for M5Stack Cardputer-Adv with DX-LR30-900M22SP LoRa module*

##  Features

###  Modern Chat Interface
- **Chat Bubbles**: Chat-style message bubbles with sender names
- **Dynamic Text Sizing**: Automatic font adjustment based on message length
- **Message Scrolling**: Navigate through chat history with FN+UP; and FN+DOWN.
- **150-character limit** with real-time counter

###  Notifications
- Full-screen notification popup for incoming messages
- Auto-dismiss after timeout

###  Customizable Themes
- **18 Color Options**: White, Black, Red, Green, Blue, Yellow, Cyan, Magenta, Orange, Pink, Purple, Brown, Gray, Light Blue, Light Green, Dark Blue, Dark Green, Dark Red
- **Main Color**: Text and UI elements
- **Secondary Color**: Background
- **Brightness Control**: 0-100% adjustment
- **Persistent Settings**: Saved across restarts (uses Preferences API)

###  Search & Navigation
- Real-time contact/channel search
- Filter as you type
- Navigate with keyboard: `;` (arrow up), `.` (arrow down), `,` (arrow left), `/` (arrow right)
- Backspace hold to clear input

###  Keyboard Features
- Full QWERTY support
- FN+`(escape) to exit/back
- OPT button is also used as escape
- Emoji filtering for display stability

##  Requirements

### Hardware
- **Device**: M5Stack Cardputer-Adv (ESP32-S3)
- **Display**: 240x135 TFT
- **LoRa Module**: 
  - DX-LR30-900M22SP (based on SX1262 chip) - custom wiring required
  - **M5Stack Cap LoRa868** (RA-01SH/SX1262) - plug-and-play solution

### Software
- **Build System**: PlatformIO
- **Initial Setup**: MeshCore mobile app (for configuration)

##  LoRa Module Options

### Option 1: M5Stack Cap LoRa868 (Recommended for Beginners)

The **M5Stack Cap LoRa868** is an official accessory that connects directly to the Cardputer-Adv without any custom wiring. Simply attach it to the back of your Cardputer-Adv.

- **Module**: RA-01SH (SX1262 chipset)
- **Frequency**: 863-870 MHz (EU868)
- **Documentation**: [Cap LoRa868 Docs](https://docs.m5stack.com/en/cap/Cap_LoRa868)
- **Advantage**: No soldering or voltage conversion needed

### Option 2: DX-LR30-900M22SP (Custom Build)

For advanced users who want a custom build, the **DX-LR30-900M22SP** module (SX1262 chipset) can be used with custom wiring:

![LoRa Module](docs/images/lora-module.jpg)
*DX-LR30-900M22SP LoRa Module (SX1262)*

| Module Pin | Cardputer GPIO | Description |
|------------|----------------|-------------|
| VCC        | 3V3            | Power supply (3.3V) |
| GND        | GND            | Ground |
| NSS        | G5             | Chip Select |
| NRST       | G3             | Reset |
| MOSI       | G14            | SPI MOSI |
| SCK        | G40            | SPI Clock |
| DIO1       | G4             | Interrupt |
| MISO       | G39            | SPI MISO |
| DIO2       | NC             | Not Connected |
| BUSY       | G6             | Busy signal |
| RXEN       | G13            | RX Enable |
| TXEN       | G15            | TX Enable |

![Cardputer-Adv with LoRa](docs/images/cardputer-with-lora.jpg)
*M5Stack Cardputer-Adv with DX-LR30-900M22SP module installed*

###  Important: 3.3V Power Requirement

**The DX-LR30-900M22SP module requires 3.3V power supply.** The Cardputer-Adv's 5V pin cannot be used directly.

You have two options:

1. **Use a 3.3V Step-Down Converter**  
   Add a voltage regulator between the 5V pin and the LoRa module's VCC.

2. **Modify the Cardputer-Adv for 3.3V Output** (Recommended)  
   Follow this guide to add a 3.3V pin to your Cardputer-Adv:  
    [Cardputer-Adv 3.3V Mod Guide (Reddit)](https://www.reddit.com/r/CardPuter/comments/1pjlkby/cardputer_adv_33v_mod/)

**Note**: Using 5V on the LoRa module will damage it permanently!

##  Building & Flashing

### Pre-compiled Binaries (Recommended)

**Ready-to-flash .bin files are available in [Releases](https://github.com/Stachugit/MeshCore-Cardputer-ADV/releases):**

- `firmware_Cap_LoRa868.bin` - For M5Stack Cap LoRa868
- `firmware_DX-LR30.bin` - For custom DX-LR30-900M22SP module

Flash using your preferred tool (esptool.py, ESP Flash Download Tool, or web flasher).

### Building from Source

### For Custom DX-LR30-900M22SP Module:
```bash
# Clone the repository
git clone https://github.com/Stachugit/MeshCore-Cardputer-ADV.git
cd MeshCore-Cardputer-ADV

# Build and upload
pio run -e CardputerADV_keyboard_UI --target upload
```

### For M5Stack Cap LoRa868:
```bash
# Build and upload for Cap LoRa868
pio run -e CardputerADV_keyboard_UI_Cap_LoRa868 --target upload
```

##  Initial Setup

**Important**: Before using the Cardputer-Adv UI, you must first configure the device using the **MeshCore mobile app**:

1. Flash the firmware to your M5Stack Cardputer-Adv
2. Download the MeshCore app on your smartphone
3. Connect to the Cardputer-Adv via Bluetooth
4. Configure essential settings:
   - Node name
   - Region/frequency settings
   - Network keys
   - Channel configuration

**Future Updates**: Some settings will be configurable directly on the Cardputer-Adv without needing the mobile app.

##  Project Structure

```
MeshCore-Cardputer-ADV/
 examples/
    companion_radio/
        ui-keyboard/          # Main UI implementation
            UITask.cpp        # Core UI logic
            UITask.h          # UI header
            settings_impl.cpp # Settings persistence
            ...
 src/                          # MeshCore core
 lib/                          # Libraries
 arch/                         # Architecture definitions
 boards/                       # Board configurations
 platformio.ini                # Build configuration
 README.md
```

##  Usage

### Navigation
- **`;`** - Navigate up
- **`.`** - Navigate down
- **`,`** - Navigate left / Switch to Contacts
- **`/`** - Navigate right / Switch to Channels
- **Enter/Space** - Select
- **FN+`** - Back/Exit
- **OPT** - Alternative back button

### Chat Controls
- Type normally to compose message
- **Enter** - Send message
- **Backspace** - Delete character
- **Hold Backspace (1.5s)** - Clear entire message
- **FN+;** - Scroll to older messages
- **FN+.** - Scroll to newer messages

### Settings Menu
- Access via hamburger menu icon () in top-left corner
- Adjust **Brightness**:   arrows
- Select **Main Color**:   to cycle through colors
- Select **Secondary Color**:   to cycle through colors
- **Save** - Store settings
- **Back** - Discard changes

##  Technical Details

### Memory Management
- **Settings Storage**: NVS (Preferences API) - isolated from mesh data
- **Chat History**: 50-message circular buffer per conversation
- **Contact Filtering**: Real-time case-insensitive search

### Display Features
- **Auto-off**: 5 minutes of inactivity
- **Smart Refresh**: Only updates when needed
- **Notification Duration**: 3 seconds
- **Text Filtering**: Removes emojis and non-ASCII for stability

### Color System
- RGB565 format (16-bit color)
- Dynamic theme application
- Per-element color control

### Radio Configuration
- **Chipset**: Semtech SX1262
- **Frequency**: 868.0 MHz (EU868)
- **Bandwidth**: 125 kHz
- **Spreading Factor**: 11
- **Coding Rate**: 4/5
- **TX Power**: 22 dBm

##  Credits

### Based On
This project is a UI modification of [MeshCore](https://github.com/meshcore-dev/MeshCore]) mesh networking firmware.

### Original MeshCore
- Core mesh networking functionality
- Radio communication (LoRa/ESP-NOW)
- Contact/channel management
- Message routing

### UI Modifications
- TFT interface redesign
- Chat bubble system
- Settings menu with theme customization
- Enhanced keyboard navigation
- Notification system

##  License

This project maintains the same license as the original MeshCore firmware. See [license.txt](license.txt) for details.

##  Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest features
- Submit pull requests
- Improve documentation

##  Links

- Original MeshCore: [[Link](https://github.com/meshcore-dev/MeshCore)]
- M5Stack Cardputer-ADV: https://shop.m5stack.com/products/m5stack-cardputer-adv-version-esp32-s3
- M5Stack Cap LoRa868: https://docs.m5stack.com/en/cap/Cap_LoRa868
- Cardputer-Adv 3.3V Mod: https://www.reddit.com/r/CardPuter/comments/1pjlkby/cardputer_adv_33v_mod/

##  Disclaimer

This is an independent UI modification. For core mesh networking functionality and protocol questions, refer to the original MeshCore project.

**Hardware Safety**: Ensure proper voltage levels when connecting the LoRa module. Using incorrect voltage will damage the module permanently.

---

**Version**: 1.0.0  
**Last Updated**: January 6, 2026
