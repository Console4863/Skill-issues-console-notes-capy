|Category|Requirements, Conventions or Software Version Used|
|---|---|
|System|Any [Linux distro](https://linuxconfig.org/linux-download)|
|Software|GNOME, KDE, XFCE, MATE, LXQT, Cinnamon|
|Other|Privileged access to your Linux system as root or via the `sudo` command.|
|Conventions|**#** – requires given [linux commands](https://linuxconfig.org/linux-commands) to be executed with root privileges either directly as a root user or by use of `sudo` command  <br>**$** – requires given [linux commands](https://linuxconfig.org/linux-commands) to be executed as a regular non-privileged user|

## How to open file explorer from terminal on Linux

---

---

  
The basic process for opening the file explorer from your terminal is to execute the command that relates to your file explorer application. The caveat here is that each desktop environment tends to name their file explorer differently, so it is never the same command. We will cover the default file explorers for some of the most popular Linux desktop environments below.

**NOTE**  
In the commands below, we append a `.` which tells the file explorer to open the current directory in which your terminal resides. This is not strictly necessary, and you can provide a different path if you wish.

### GNOME

GNOME is the default desktop environment for [Ubuntu Linux](https://linuxconfig.org/ubuntu-linux-download) and names their file explorer Nautilus. To open the file explorer in GNOME, enter:

$ nautilus .

[![Opening the file explorer in the current directory where our terminal resides](https://linuxconfig.org/wp-content/uploads/2023/04/01-how-to-open-file-explorer-from-terminal-on-linux.png)](https://linuxconfig.org/wp-content/uploads/2023/04/01-how-to-open-file-explorer-from-terminal-on-linux.png)

Opening the file explorer in the current directory where our terminal resides

### KDE

KDE uses the Dolphin file manager. To open the file explorer in KDE Plasma, enter:

$ dolphin .

---

---

### Xfce

Xfce uses the Thunar file manager. To open the file explorer in Xfce, enter:

$ thunar .

### MATE

MATE utilizes the Caja file manager. To open the file explorer in MATE, enter:

$ caja .

### LXQt

LXQt has the pcmanfm file manager. To open the file explorer in LXQt, enter:

$ pcmanfm-qt .

### Cinnamon

Cinnamon is the default desktop environment for [Linux Mint](https://linuxconfig.org/linux-mint-download) and uses the Nemo file manager. To open the file explorer in Nemo, enter:

$ nemo .