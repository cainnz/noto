#Public/Notta 
## Ubuntu Based Sytems

**.desktop files are store in:**
```bash
~/home/user/.local/share/applications
```
- All files needs to end with ***.desktop*** anything before the ***dot*** can be anything
- Files can be edited with **nano** or any other editor
Follow the following example to create **entries** when using **AppImages**:
```bash
[Desktop Entry]
Type=Application
Name=Application_Name
Comment=Same_as_application_name
Icon=Icon_location_full_path
Exec=AppImage_location_full_path
Terminal=false
Categories=Internet,Utilities,etc #it can be any of these or other options
```
**to unzip AppImages:*
```bash

```
## Apt package manager, well maintained apps

**exa:** A 'ls' replacement, it can show awesome icons as well, ***note: a nerdfont needs to be installed***

**installation:**
```bash
sudo apt install exa
```

__caffeine:__ Prevent screen from going to sleep

**installation:**
```bash
sudo apt install caffeine
```

**wireguard:**
```bash
sudo dnf install wireguard-tools # same package might work on other distros
```

create ***.conf*** file and place it in > ***/etc/wireguard/name.conf*** 

**cheat sheet:**
```bash
wg-quick up name #you only need the name of the .conf file!
wg-quick down name


```
