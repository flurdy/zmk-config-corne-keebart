# ZMK Config - Corne Keebart

ZMK firmware configuration for custom split keyboards with ZMK Studio support.

## Supported Keyboards

This configuration supports two keyboard variants:

### 1. Corne Choc Pro
- Custom Corne-style split keyboard with Choc switches
- 42 keys (6×3 + 3 thumb keys per side)
- 2 rotary encoders (one per side)
- Nice!View display support
- ZMK Studio enabled

### 2. Piantor Pro BT
- 42-key split keyboard
- Nice!View display support
- ZMK Studio enabled
- Standard 3×6+3 layout

## Features

- **ZMK Studio Support**: Real-time keymap editing via USB
- **Nice!View Displays**: OLED display integration for both keyboards
- **Bluetooth**: Multiple device pairing (up to 5 devices)
- **RGB Support**: RGB underglow control
- **Rotary Encoders**: Volume, page scrolling, media controls, and brightness (Corne Choc Pro)
- **Multiple Layers**: 
  - Layer 0: QWERTY (default)
  - Layer 1: Numbers & Bluetooth controls
  - Layer 2: Symbols
  - Layers 3-8: Extra customizable layers

## Keymap Overview

**IMPORTANT: This configuration is designed for use with OS set to Colemak layout!**

The keyboard has two primary layouts that work with your OS Colemak setting:

### Default Layer (Layer 0) - "QWERTY codes → Colemak output"

- **What it does**: Sends QWERTY keycodes to your Colemak OS
- **What you get**: Colemak layout when typing
- **When to use**: Normal daily use when you want Colemak
- This is the default layer when your keyboard starts up

### Colemak Layer (Layer 3) - "Colemak codes → QWERTY output"

- **What it does**: Sends Colemak keycodes to your Colemak OS  
- **What you get**: QWERTY layout when typing
- **When to use**: When you need QWERTY temporarily (gaming, teaching someone, etc.)
- **How to toggle**: Press the toggle key on Layer 1 (Number layer, right home row after arrow keys)

### Why This Setup?

This configuration solves a common problem: keeping your OS in Colemak mode so your laptop keyboard works as expected, while still being able to switch your ZMK keyboard between Colemak and QWERTY as needed.

**Editing keymap files**: You can edit the `.keymap` files thinking in standard key positions (Q-W-E-R-T-Y) because the labels match physical positions, not the output!

### Layer Details

#### Default Layer (QWERTY codes for Colemak OS)

Standard QWERTY layout with:
- Tab, Ctrl, Shift modifiers on the left
- Layer access via thumb keys
- Backspace, quotes, and Escape on the right

#### Colemak Layer (Toggle for QWERTY)

- Activated by toggle key on Layer 1 (right home row, after arrow keys)
- Outputs Colemak codes → OS interprets as Colemak → You get QWERTY
- Same modifiers and layer keys as default layer
- Press toggle again to return to Colemak typing

### Lower Layer (Numbers)
- Number row (1-9, 0)
- Bluetooth device selection (BT1-BT5)
- Bluetooth clear
- RGB toggle
- System reset and bootloader access
- ZMK Studio unlock
- Arrow keys on the right side
- **Layout toggle key** (right home row, after arrows) - switches between Colemak and QWERTY output

### Raise Layer (Symbols)
- Special characters and symbols
- Brackets, parentheses, braces
- Mathematical operators
- Backslash, pipe, tilde, grave

## Building Firmware

This repository uses GitHub Actions to automatically build firmware for all keyboard variants.

### Automatic Builds

Every push to the repository triggers automatic firmware builds for:
- Corne Choc Pro (left/right with Nice!View)
- Piantor Pro BT (left/right with Nice!View)
- Settings reset builds for both keyboards

Firmware files are available as artifacts in the GitHub Actions tab.

### Local Development

To build locally, you'll need the ZMK development environment:

1. Clone this repository
2. Install [Zephyr dependencies](https://zmk.dev/docs/development/setup)
3. Initialize west workspace:
   ```bash
   west init -l config/
   west update
   ```
4. Build for your keyboard:
   ```bash
   # Corne Choc Pro Left
   west build -p -b corne_choc_pro_left -- -DSHIELD=nice_view -DCONFIG_ZMK_STUDIO=y
   
   # Corne Choc Pro Right
   west build -p -b corne_choc_pro_right -- -DSHIELD=nice_view
   
   # Piantor Pro BT Left
   west build -p -b piantor_pro_bt_left -- -DSHIELD=nice_view -DCONFIG_ZMK_STUDIO=y
   
   # Piantor Pro BT Right
   west build -p -b piantor_pro_bt_right -- -DSHIELD=nice_view
   ```

## Installation

1. Download the latest firmware from GitHub Actions artifacts
2. Extract the `.uf2` files
3. Connect your keyboard half via USB while holding the reset button
4. The keyboard will appear as a USB drive
5. Copy the appropriate `.uf2` file to the drive
6. The keyboard will automatically reboot with the new firmware
7. Repeat for the other half

## ZMK Studio

ZMK Studio allows real-time keymap editing without rebuilding firmware.

### Unlocking Studio Mode

To access ZMK Studio:
1. Connect your keyboard via USB
2. Press the Studio unlock key combo (found on Layer 1)
3. Open ZMK Studio in your browser
4. Edit your keymap in real-time

### Studio Features
- Live keymap editing
- Layer management
- Behavior configuration
- Display customization

## Customization

### Modifying Keymaps

Keymap files are located in:
- `config/corne_choc_pro.keymap` - Corne Choc Pro layout
- `config/piantor_pro_bt.keymap` - Piantor Pro BT layout

Edit these files to customize your layout, then commit and push to trigger automatic builds.

### Board Definitions

Custom board definitions are in:
- `boards/arm/corne_choc_pro/` - Corne Choc Pro board files
- `boards/arm/piantor_pro_bt/` - Piantor Pro BT board files

### Build Configuration

Build matrix is defined in `build.yaml`. Modify this to:
- Add/remove keyboard variants
- Enable/disable shields
- Add build flags
- Configure artifacts

## Bluetooth Pairing

To pair with a device:
1. Select a profile slot (Layer 1: keys 1-5 = BT1-BT5)
2. Put your device in Bluetooth discovery mode
3. Select "Corne Choc Pro" or "Piantor Pro BT" from available devices
4. Switch between paired devices using the same profile keys

To clear a profile:
- Press the Bluetooth clear key (Layer 1, left bottom corner)

## Troubleshooting

### Settings Reset

If you experience pairing or configuration issues:
1. Download the settings reset firmware for your keyboard
2. Flash it following the installation instructions
3. Flash your normal firmware again
4. Re-pair your Bluetooth devices

### Bootloader Access

To force bootloader mode:
- Press the bootloader key (Layer 1) or
- Double-tap the reset button on your keyboard

### Split Communication Issues

If the halves aren't communicating:
1. Reset both halves
2. Clear Bluetooth bonds on both devices
3. Ensure both halves are running matching firmware versions

## Resources

- [ZMK Documentation](https://zmk.dev/)
- [ZMK Studio](https://zmk.studio/)
- [Keymap Editor](https://nickcoutsos.github.io/keymap-editor/)
- [ZMK Discord](https://zmk.dev/community/discord/invite)

## License

This configuration is released under the MIT License. See individual files for copyright information.

## Credits

- ZMK Firmware: [zmkfirmware/zmk](https://github.com/zmkfirmware/zmk)
- Corne Keyboard: [foostan/crkbd](https://github.com/foostan/crkbd)
- Piantor: Based on Beekeeb's Piantor design
