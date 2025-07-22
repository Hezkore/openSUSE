# Floorp Browser

Floorp is just a modified version of Firefox, with additional features and customizations.\
I mainly use it because it syncs with Firefox Sync and launches *a lot* faster than Firefox itself.

Please see the "prefs.js" section below for some configuration changes that make it more usable.

Floorp is not available in the package repositories, so we have two options.

The simplest is via `opi`.\
However, I'm not sure how well auto-updates work that version:
```bash
sudo opi -n floorp-browser
```

A method that I know works, and will auto-update itself is:

1. Download Linux (x86_64) from the [Floorp releases page](https://floorp.app/download)
2. Extract to `/opt/`
```bash
sudo tar -xjf ~/Downloads/floorp-*.tar.bz2 -C /opt/
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

No matter how we installed Floorp, it is weirdly configured by default.\
You can go through Floorp and try and find all of the things to change.\
Or we can simply add some things to `prefs.js` to instantly fix some of the things.


First, start Floorp once, then close it and make sure Floorp isn't running somewhere else.\
Then navigate to `~/.floorp/<profile directory>`.\
`<profile directory>` is usually a bunch of numbers ending with `default-release`.\
Find the `prefs.js` file in that directory.

Add this to the end of the `prefs.js` file:
```javascript
// Disable all sidebars
user_pref("floorp.browser.sidebar.enable", false);
user_pref("floorp.browser.sidebar.is.displayed", false);
// Disable the sponsored site suggestions
user_pref("browser.newtabpage.activity-stream.showSponsoredTopSites", false);
// Disable password saving
user_pref("signon.rememberSignons", false);
// Fix the wonky mouse scrolling
user_pref("mousewheel.default.delta_multiplier_y", 100);
user_pref("general.smoothScroll.currentVelocityWeighting", "0.25");
user_pref("general.smoothScroll.mouseWheel.durationMinMS", 50);
user_pref("general.smoothScroll.msdPhysics.continuousMotionMaxDeltaMS", 120);
user_pref("general.smoothScroll.msdPhysics.enabled", false);
user_pref("general.smoothScroll.msdPhysics.motionBeginSpringConstant", 1250);
user_pref("general.smoothScroll.msdPhysics.regularSpringConstant", 1000);
user_pref("general.smoothScroll.msdPhysics.slowdownMinDeltaMS", 12);
user_pref("general.smoothScroll.msdPhysics.slowdownSpringConstant", 2000);
user_pref("general.smoothScroll.stopDecelerationWeighting", "0.4");
```