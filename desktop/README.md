# Desktop Environment

My main choice of desktop environment is XFCE.

Sadly, it's currently only X11.\
But I think it makes up for it with its simplicity, stability, and speed.

KDE Plasma fails due to death from a million cuts.\
And GNOME fails due to not having a system tray by default.\
Every other desktop just seems like a lesser version of XFCE.

XFCE isn't without its faults, but most of them can be mitigated fairly easily, and we'll fix and work around some of them here, as well as set up some basic things.

## Mouse Configuration

With a mouse at 1100 DPI, the default XFCE speed is okay.\
However, the "Adaptive pointer acceleration" feels terrible, so that needs to be disabled.

Other than that I don't really have any other mouse-related tweaks.

## Theme

I'm not a huge fan of Dracula, but I like the consistency of it across applications.\
The Vimix icons aren't the best looking ones, but they cover most of the applications, so again, consistency.

### Dracula
---
The various Downloads for Dracula are all pretty outdated, so is the one in the official repositories.\
So we'll grab it from the official GitHub repository and clone it straight into the themes directory:
```bash
sudo git clone https://github.com/dracula/gtk.git /usr/share/themes/Dracula
```
And because GNOME is a pain, we need to symlink some files and directories:
```bash
sudo ln -s /usr/share/themes/Dracula/assets ~/.config
mkdir -p ~/.config/gtk-4.0 && sudo ln -s /usr/share/themes/Dracula/gtk-4.0/gtk*.css ~/.config/gtk-4.0/
```

And to apply it:
```bash
xfconf-query -c xsettings -p /Net/ThemeName -s "Dracula"
xfconf-query -c xfwm4 -p /general/theme -s "Dracula"
gsettings set org.gnome.desktop.interface gtk-theme "Dracula"
gsettings set org.gnome.desktop.wm.preferences theme "Dracula"
```

And to make GNOME prefer dark mode:
```bash
gsettings set org.gnome.desktop.interface color-scheme "prefer-dark"
```

We can update the Dracula at any point now by calling:
```bash
sudo git -C /usr/share/themes/Dracula pull
```

### Vimix Icons
---
Same with Vimix, most sources are outdated, so we'll clone it from the GitHub repo.\
Only downside is that it requires us to use a install script, which isn't as easy to update as the Dracula theme:
```bash
sudo git clone https://github.com/vinceliuice/Vimix-icon-theme.git /tmp/Vimix
```

Now to install it:
```bash
sudo /tmp/Vimix/install.sh -d /usr/share/icons
```

Apply them:
```bash
xfconf-query -c xsettings -p /Net/IconThemeName -s "Vimix-dark"
gsettings set org.gnome.desktop.interface icon-theme "Vimix-dark"
```

## Window Tweaks

### Buttons
---
I don't need to see the application icon, nor the maximize button, so we'll remove those from the title bar:
```bash
xfconf-query -c xfwm4 -p /general/button_layout -s "|HC"
```
