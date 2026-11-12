# Flameshot for Ubuntu

Build a `.deb` from the `v15.0.0.0` tag and install it with `apt`.

1. Install the build tools and dependencies:

```shell
sudo apt update
sudo apt install git cmake build-essential debhelper devscripts \
    qt6-base-dev qt6-tools-dev qt6-tools-dev-tools qt6-l10n-tools libqt6svg6-dev \
    qt6-wayland-dev libgl-dev libxkbcommon-dev libvulkan-dev \
    libkdsingleapplication-qt6-dev
```

2. Download the tag:

```shell
git clone --branch v15.0.0.0 --depth 1 https://github.com/leocostaba/flameshot-wayland.git
cd flameshot-wayland
```

3. Build the package (the Debian files live in `packaging/debian`, so link them to the repo root first):

```shell
ln -s packaging/debian debian
dpkg-buildpackage -us -uc -b
```

4. Install it. The `.deb` is created one directory above the repo:

```shell
sudo apt install ../flameshot_15.0.0.0-1_amd64.deb
```

5. Check it and start it:

```shell
flameshot --version
flameshot gui
```

For Wayland, the package recommends `xdg-desktop-portal-gtk` (GNOME), `xdg-desktop-portal-kde` (KDE) or `xdg-desktop-portal-wlr` and `grim` (Sway/Hyprland). `apt` installs the recommended packages by default.

To remove it: `sudo apt remove flameshot`.
