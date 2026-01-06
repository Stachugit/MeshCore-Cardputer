# MeshCore-Cardputer

Enhanced TFT user interface for MeshCore mesh networking firmware, optimized for M5Stack Cardputer.

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
- **Device**: M5Stack Cardputer (ESP32-S3)
- **Display**: 240x135 TFT
- **LoRa Module**: DX-LR30-900M22SP (based on SX1262 chip)

### Software
- **Build System**: PlatformIO
- **Initial Setup**: MeshCore mobile app (for configuration)

##  LoRa Module Wiring

The project uses the **DX-LR30-900M22SP** LoRa module (SX1262 chipset). Connect as follows:

| Module Pin | Cardputer GPIO | Description |
|------------|----------------|-------------|
| VCC        | 3V3            | Power supply |
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

**Note**: The RXEN and TXEN pins are used for controlling the external RF switch on this module.

##  Building & Flashing

```bash
# Clone the repository
git clone https://github.com/[your-username]/MeshCore-Cardputer.git
cd MeshCore-Cardputer

# Build and upload
pio run -e m5stack_cardputer_companion_headless --target upload
```

##  Initial Setup

**Important**: Before using the Cardputer UI, you must first configure the device using the **MeshCore mobile app**:

1. Flash the firmware to your M5Stack Cardputer
2. Download the MeshCore app on your smartphone
3. Connect to the Cardputer via Bluetooth
4. Configure essential settings:
   - Node name
   - Region/frequency settings
   - Network keys
   - Channel configuration

**Future Updates**: Some settings will be configurable directly on the Cardputer without needing the mobile app.

##  Project Structure

```
MeshCore-Cardputer/
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

##  Screenshots

*(soon)*

##  Links

- Original MeshCore: [[Link](https://github.com/meshcore-dev/MeshCore)]
- M5Stack Cardputer: https://shop.m5stack.com/products/m5stack-cardputer-kit-w-m5stamps3

##  Disclaimer

This is an independent UI modification. For core mesh networking functionality and protocol questions, refer to the original MeshCore project.

---

**Version**: 1.0.0  
**Last Updated**: January 6, 2026
