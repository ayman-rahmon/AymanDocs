# adding languages and keyboards to linux (arch linux and those based on it)




## preperations steps:

the wanted language's lines in the file should be uncommented in the file :
/etc/locale.gen   (usually two lines per language)

after the lines for the languages wanted is uncommented you should run this command:

```
locale-gen
```



##installing necessary packages:
```
# installing fonts for the language you want to add.
sudo pacman -S adobe-source-han-sans-jp-fonts otf-ipafont
yay -S ttf-monapo



#installing a keymap manager (easier than handling the fonts directly)
sudo pacman -S ibus ibus-anthy
```
## adding the keymap manager to work on the start of the user's session:

```
# add the following lines to the file ~/.xprofile (to make them run on user login)

export GTK_IM_MODULE='ibus'
export QT_IM_MODULE='ibus'
export XMODIFIERS=@im='ibus'

#Toolbar for anthy
ibus-daemon -drx
```
## set up your preferences:
```
# you can set up your preferences using a visual tool by typing the following in the terminal

ibus-setup

```
