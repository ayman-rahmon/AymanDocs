# snap settings...

## installing snap on arch linux:

```
git clone https://aur.archlinux.org/snapd.git
cd snapd
makepkg -si


# enabling the service for snap to work...

sudo systemctl systemctl enable --now snapd.socket


# to enable classic snap support...

sudo ln -s /var/lib/snapd /snap

```
## installing a snap image:
```
sudo snap install <name of image>

```
## to run a snap image:

```
snap run <name of image>

```
