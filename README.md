
# kitty.config

This repository contains the custom configuration for the [kitty terminal emulator](https://sw.kovidgoyal.net/kitty/). It includes:
- **kitty.conf:** The main configuration file.
- **tokyonight.conf:** An optional theme configuration (Tokyo Night).
- **terminal-box-fill-svgrepo-com.svg:** A custom desktop icon for kitty.
- **spaceman.jpg:** An additional image resource (if needed).

## Table of Contents
- [Overview](#overview)
- [Installation](#installation)
- [Set Kitty as Your Default Terminal](#set-kitty-as-your-default-terminal)
- [Update the Desktop Icon](#update-the-desktop-icon)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## Overview
This configuration is designed to enhance your kitty terminal experience. The repository provides a primary configuration file (`kitty.conf`) along with an optional theme file (`tokyonight.conf`). Additionally, a custom desktop icon (`terminal-box-fill-svgrepo-com.svg`) is included to personalize your kitty launcher.

## Installation

### 1. Clone the Repository
Clone the repo to your local machine:
```bash
git clone https://github.com/igorkhalip-KidouSystems/kitty.config.git ~/.config/kitty
cd kitty.config
```

### 2. Set Up the Kitty Configuration
Kitty loads its configuration from `~/.config/kitty/kitty.conf`. To use the configuration provided in this repository, do one of the following:

- **Using a Symbolic Link:**
  ```bash
  mkdir -p ~/.config/kitty
  ln -sf "$(pwd)/kitty.conf" ~/.config/kitty/kitty.conf
  ```

- **Copying the File:**
  ```bash
  mkdir -p ~/.config/kitty
  cp kitty.conf ~/.config/kitty/kitty.conf
  ```

If you want to use the Tokyo Night theme settings, you can merge or include the settings from `tokyonight.conf` into your `kitty.conf`.

## Set Kitty as Your Default Terminal

### For GNOME (or Similar Desktop Environments)
1. Open **Settings** and navigate to **Default Applications**.
2. Under **Terminal Emulator**, select **kitty**.

### For Debian/Ubuntu (Command Line)
1. Run the following command:
   ```bash
   sudo update-alternatives --config x-terminal-emulator
   ```
2. Choose the option corresponding to **kitty**.

*Note:* If you’re using another desktop environment, refer to its documentation for setting the default terminal emulator.

## Update the Desktop Icon

To ensure that kitty uses the custom desktop icon from this repository, follow these steps:

### 1. Copy the Custom Icon
Copy the `terminal-box-fill-svgrepo-com.svg` file to your local icons directory:

- **For User-Specific Installation:**
  ```bash
  mkdir -p ~/.local/share/icons/hicolor/scalable/apps
  cp terminal-box-fill-svgrepo-com.svg ~/.local/share/icons/hicolor/scalable/apps/kitty.svg
  ```

- **For System-Wide Installation (requires sudo):**
  ```bash
  sudo cp terminal-box-fill-svgrepo-com.svg /usr/share/icons/hicolor/scalable/apps/kitty.svg
  ```

### 2. Update the Desktop Entry
Locate your kitty desktop entry file (commonly found at `/usr/share/applications/kitty.desktop` or `~/.local/share/applications/kitty.desktop`). Open the file in a text editor and update the `Icon` field to point to the new icon. For example:

```ini
[Desktop Entry]
Name=Kitty
Comment=Kitty Terminal Emulator
Exec=kitty
Icon=/home/yourusername/.local/share/icons/hicolor/scalable/apps/kitty.svg
Type=Application
Terminal=false
Categories=Utility;TerminalEmulator;
```

Replace `/home/yourusername/` with your actual home directory path.

### 3. Refresh the Icon Cache
After updating the desktop entry, refresh the icon cache:

- **For User Icons:**
  ```bash
  gtk-update-icon-cache ~/.local/share/icons/hicolor
  ```
- **For System Icons:**
  ```bash
  sudo gtk-update-icon-cache /usr/share/icons/hicolor
  ```

## Troubleshooting
- **Configuration Not Loading:** Ensure that `kitty.conf` is correctly linked or copied to `~/.config/kitty/kitty.conf`.
- **Default Terminal Not Changing:** Double-check your system’s default application settings or rerun the `update-alternatives` command.
- **Icon Not Updating:** Verify that the desktop entry points to the correct icon path and that the icon cache has been refreshed.

## Contributing
Contributions, improvements, or bug fixes are welcome! Please open an issue or submit a pull request with your suggestions.

