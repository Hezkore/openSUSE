# Floorp Browser

Floorp is just a modified version of Firefox with additional features and customizations.\
I mainly use it because it syncs with Firefox Sync and launches a lot faster than Firefox itself.

Floorp is not available in the package repositories, so I do the following:

1. Download Linux (x86_64) from the [Floorp releases page](https://floorp.app/download)
2. Extract to `/opt/`
```bash
sudo tar -xjf /home/hezkore/Downloads/floorp-*.tar.bz2 -C /opt/
```
3. Create `~/.local/share/applications/floorp.desktop` and add the following content:
```ini
[Desktop Entry]
Name=Floorp
GenericName=Web Browser
Comment=Browse the Web
Exec=/opt/floorp/floorp %u
StartupWMClass=firefox-aurora
Icon=/opt/floorp/browser/chrome/icons/default/default64.png
Terminal=false
Type=Application
Categories=Network;WebBrowser;GTK;
MimeType=text/html;text/xml;application/xhtml+xml;application/vnd.mozilla.xul+xml;text/mml;application/x-xpinstall;x-scheme-handler/http;x-scheme-handler/https;
StartupNotify=true
Keywords=web;browser;internet;
Actions=new-window;new-private-window;profile-manager-window;

[Desktop Action new-window]
Name=Open a New Window
Exec=/opt/floorp/floorp --new-window %u

[Desktop Action new-private-window]
Name=Open a New Private Window
Exec=/opt/floorp/floorp --private-window %u

[Desktop Action profile-manager-window]
Name=Open the Profile Manager
Exec=/opt/floorp/floorp --ProfileManager
```