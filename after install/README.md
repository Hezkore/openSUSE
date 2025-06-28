# After Initial Install

## Root Password

If the root password was not set during the install, you can set it now:
```bash
sudo passwd root
```


## Auto Agree With Licenses

It's not like we have a choice anyway, so let's just agree to all licenses automatically.

```bash
sudo vim /etc/zypp/zypp.conf
```

Find the line:
```bash
#autoAgreeWithLicenses = no
```

Uncomment it and change it to:
```bash
autoAgreeWithLicenses = yes
```

## NVidia Kernel Module

After install, the `nouveau` kernel module will be loaded, which is fine for AMD GPUs, but for NVidia GPUs you will want to install the proprietary NVidia driver.

First we add the repository:
```bash
sudo zypper install openSUSE-repos-Tumbleweed-NVIDIA
```

Then we install the driver based on what's recommended:

```bash
sudo zypper install-new-recommends --repo repo-non-free
```

## Media Codec Support

The default ones are open-source and don't quite handle H.264 and H.265 all that well.
The proprietary ones are available in the `packman` repository, which is not enabled by default for legal reasons.

Add the Tumbleweed `packman` repository:
```bash
sudo zypper addrepo -cfp 90 'https://ftp.gwdg.de/pub/linux/misc/packman/suse/openSUSE_Tumbleweed/' packman
```

Then refresh, upgrade and install the codecs:
```bash
sudo zypper refresh
sudo zypper dist-upgrade --from packman --allow-vendor-change
sudo zypper install --from packman ffmpeg gstreamer-plugins-{good,bad,ugly,libav} libavcodec vlc-codecs
```
