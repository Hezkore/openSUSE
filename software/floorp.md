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
4. Set Floorp as the default browser:
```bash
xdg-settings set default-web-browser floorp.desktop
```

## prefs.js

Floorp is good and all, but weirdly configured by default.\
Add this to the end of the `prefs.js` file located at `~/.floorp/<profile directory>`:
```javascript
user_pref("general.smoothScroll.currentVelocityWeighting", "0.25");
user_pref("general.smoothScroll.mouseWheel.durationMinMS", 50);
user_pref("general.smoothScroll.msdPhysics.continuousMotionMaxDeltaMS", 120);
user_pref("general.smoothScroll.msdPhysics.enabled", false);
user_pref("general.smoothScroll.msdPhysics.motionBeginSpringConstant", 1250);
user_pref("general.smoothScroll.msdPhysics.regularSpringConstant", 1000);
user_pref("general.smoothScroll.msdPhysics.slowdownMinDeltaMS", 12);
user_pref("general.smoothScroll.msdPhysics.slowdownSpringConstant", 2000);
user_pref("general.smoothScroll.stopDecelerationWeighting", "0.4");
user_pref("mousewheel.default.delta_multiplier_y", 100);
user_pref("floorp.browser.sidebar.is.displayed", false);
```