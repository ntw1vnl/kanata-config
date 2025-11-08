# Kanata

This repo contains the my kbd configuration file for my laptop as well as modified build rules for kanata in order to enabled  the [cmd feature](https://jtroo.github.io/config.html#cmd) used to send a notification when changing base layers.

The original AUR repo can be found here : https://aur.archlinux.org/kanata.git

## How to use

### Clone this repo

```bash
mkdir ~/aur
cd aur
git clone git@github.com:ntw1vnl/kanata-config.git 
```

### Build and install

```bash
cd ~/aur/kanata-config
makepkg -sic
```

### Verify user input group belonging

Make sure the user belongs to the `input` group.

```bash
groups
```

If `input` is not one of the user groups, add it like so :

```bash
sudo usermod -aG input $USER
```

### Copy configuration file 

```bash
cp kanata.kbd ~/.config/
```

### Create systemd service

```bash
cp kanata.service ~/.config/systemd/user/
sudo systemctl --user enable kanata.service
sudo systemctl --user start kanata.service
```
