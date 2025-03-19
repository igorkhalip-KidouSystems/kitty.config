# Kitty Configuration

This repository contains a minimal kitty configuration with a custom prompt and desktop integration setup.

## 1. Cloning the Repository

Clone this repo directly into your kitty configuration directory:

```sh
git clone https://github.com/ikhalip/kitty.config.git ~/.config/kitty
```

## 2. Desktop Integration

To integrate kitty with your desktop environment, follow these steps:

1. **Create symbolic links for kitty and kitten**  
   (Ensure `~/.local/bin` is in your PATH.)
   ```sh
   ln -sf "$(readlink -f ~)/.local/kitty.app/bin/kitty" "$(readlink -f ~)/.local/kitty.app/bin/kitten" "$(readlink -f ~)/.local/bin/"
   ```

2. **Copy the Desktop Entry Files**  
   Copy the default desktop entry files from your kitty installation:
   ```sh
   cp "$(readlink -f ~)/.local/kitty.app/share/applications/kitty.desktop" ~/.local/share/applications/
   cp "$(readlink -f ~)/.local/kitty.app/share/applications/kitty-open.desktop" ~/.local/share/applications/
   ```

3. **Update the Desktop Entry Paths**  
   Replace the default icon and executable paths with the ones from your installation and use your custom icon from this repo. For example, if your custom icon is stored at:
   ```
   $HOME/.config/kitty/terminal-box-fill-svgrepo-com.svg
   ```
   run:
   ```sh
   sed -i "s|^Icon=.*$|Icon=$(readlink -f ~)/.config/kitty/terminal-box-fill-svgrepo-com.svg|g" ~/.local/share/applications/kitty*.desktop
   sed -i "s|^Exec=.*$|Exec=$(readlink -f ~)/.local/kitty.app/bin/kitty|g" ~/.local/share/applications/kitty*.desktop
   ```

4. **Update the Desktop Database & Terminal Registration**  
   ```sh
   update-desktop-database ~/.local/share/applications/
   mkdir -p ~/.config
   echo 'kitty.desktop' > ~/.config/xdg-terminals.list
   ```

## 3. Making Kitty Your Main Terminal

To set kitty as your default terminal emulator:

- **Using update-alternatives (Ubuntu/Debian):**
  ```sh
  sudo update-alternatives --config x-terminal-emulator
  ```
- **For GNOME users, set it via gsettings:**
  ```sh
  gsettings set org.gnome.desktop.default-applications.terminal exec "$(readlink -f ~/.local/kitty.app/bin/kitty)"
  ```
Adjust these commands as needed for your desktop environment.

## 4. Custom Prompt Configuration

This configuration repo uses a custom prompt for kitty. The prompt is defined as follows:

```sh
\[\e]133;k;start_kitty\a\]\[\e]133;D;$?\a\e]133;A\a\]\[\e]133;k;end_kitty\a\]\[\e[1;32m\]\u@\h\[\e[0m\]:\[\e[1;34m\]\w\[\e[0m\]\$ \[\e]133;k;start_suffix_kitty\a\]\[\e]2;\w\a\]\[\e]133;k;end_suffix_kitty\a\]
```

You can define this prompt in one of two ways:

- **Option A: In your shell’s startup file (e.g., `~/.bashrc` or `~/.zshrc`):**
  ```sh
  export PS1="\[\e]133;k;start_kitty\a\]\[\e]133;D;$?\a\e]133;A\a\]\[\e]133;k;end_kitty\a\]\[\e[1;32m\]\u@\h\[\e[0m\]:\[\e[1;34m\]\w\[\e[0m\]\$ \[\e]133;k;start_suffix_kitty\a\]\[\e]2;\w\a\]\[\e]133;k;end_suffix_kitty\a\]"
  ```

- **Option B: In your kitty configuration file (`~/.config/kitty/kitty.conf`):**
  ```sh
  env PS1="\[\e]133;k;start_kitty\a\]\[\e]133;D;$?\a\e]133;A\a\]\[\e]133;k;end_kitty\a\]\[\e[1;32m\]\u@\h\[\e[0m\]:\[\e[1;34m\]\w\[\e[0m\]\$ \[\e]133;k;start_suffix_kitty\a\]\[\e]2;\w\a\]\[\e]133;k;end_suffix_kitty\a\]"
  ```

Choose the method that best fits your workflow. If your shell’s startup file already sets PS1, you might need to modify it there to avoid overriding.

---

Feel free to update or expand this README as needed for your setup!

