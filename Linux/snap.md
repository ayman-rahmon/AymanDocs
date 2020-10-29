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
## looking for packages:

```
snap find <package-name>

```

## installing a snap image:
```
sudo snap install <package-name>

```
## to run a snap image:

```
snap run <package-name>

```

## manipulating snap images:

```
# list installed packages...
snap list
# check the capacity and usga of packages...
df | grep <package-name>
#get a  describtion of a snap package...
snap info <package-name>



```
