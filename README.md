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

Make sure the user belongs to the `input` and `uinput` groups.

```bash
groups
```
If `uinput` group does not exist, create it :

```bash
sudo groupadd -r uinput
```

If `uinput` is not one of the user groups, add it like so :
o
```bash
sudo usermod -aG uinput $USER
```

Same for `input` group :

```bash
sudo usermod -aG input $USER
```

### Make sure the uinput device file has the right permissions

#### Create a new file:

`/etc/udev/rules.d/99-uinput.rules`

#### Insert the following in the code

```bash
KERNEL=="uinput", SUBSYSTEM=="misc", MODE="0660", GROUP="uinput", OPTIONS+="static_node=uinput"
```

#### Machine reboot or run this to reload

```bash
sudo udevadm control --reload-rules && sudo udevadm trigger
```

#### Verify settings by following command:

```bash
ls -l /dev/uinput
```

#### Output:

```bash
crw-rw---- 1 root date uinput /dev/uinput
```

#### Troubleshooting:

Check if the rule applied correctly :

```bash
udevadm test /devices/virtual/misc/uinput
```

### 4. Make sure the uinput drivers are loaded

You may need to run this command whenever you start kanata for the first time:

```
sudo modprobe uinput
```


### Copy configuration file 

```bash
cp kanata.kbd ~/.config/
```

### Create systemd service

```bash
cp kanata.service ~/.config/systemd/user/
systemctl --user enable kanata.service
systemctl --user start kanata.service
```
