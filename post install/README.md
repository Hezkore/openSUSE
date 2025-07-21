# After Initial Install

These are some of the things I think are objectively a good idea to do after installing openSUSE Tumbleweed as a regular desktop user.

## Root Password

If you ever run into issues with some applications not accepting your password (YaST, for example) it's because they are asking for the Root password, which can be skipped during installation.

So if the root password was not set during the install, you can set it now:
```bash
sudo passwd root
```

## Auto Agree With Licenses

It's not like we have a choice anyway, so let's just agree to all licenses automatically.

```bash
sudo vim /etc/zypp/zypp.conf
```
(or `nano` if `vim` is too confusing)

Find the line:
```bash
#autoAgreeWithLicenses = no
```

Uncomment it and change it to:
```bash
autoAgreeWithLicenses = yes
```

## Ignore RPM Integrity Checks

99% of all the RPM packages out there will fail the integrity checks.\
So let's just disable the damn thing by adding `gpgcheck=0` to `/etc/zypp/zypp.conf`:
```bash
echo "gpgcheck=0" | sudo tee -a /etc/zypp/zypp.conf
```

## NVidia Kernel Module

You can always check which GPU module (driver) is in use by running the command:
```bash
inxi -G
```
After install, the `nouveau` kernel module will be loaded.\
Fine for some cards, but with newer NVidia GPUs you will want to install the proprietary NVidia driver.

Did you select the "non-free repos" during install?\
If you are unsure, run:
```bash
zypper repos --details
```
And if any of listed repos starts with the URI `https://download.nvidia.com/opensuse/` then we're good.\
Otherwise, we add the repository:
```bash
sudo zypper install openSUSE-repos-Tumbleweed-NVIDIA
```

Then we install the driver based on what's recommended:
```bash
sudo zypper install-new-recommends --repo repo-non-free
```
Then reboot.

Make sure `inxi -G` says something like "gpu: nvidia".\
If it doesn't, you can try to manually install everything we need.
```bash
sudo zypper install nvidia-common-G06 nvidia-compute-G06 nvidia-compute-G06-32bit nvidia-compute-utils-G06 nvidia-gl-G06 nvidia-gl-G06-32bit nvidia-libXNVCtrl nvidia-modprobe nvidia-open-driver-G06-signed-kmp-default nvidia-persistenced nvidia-userspace-meta-G06 nvidia-video-G06 nvidia-video-G06-32bit
```

## Media Codec Support

The default ones are open-source and don't quite handle H.264 and H.265 all that well.\
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

## Wine

A lot of times Wine itself is good enough for Windows applications, and you won't need Proton or anything fancy:
```bash
sudo zypper install wine
```

Make sure we have a prefix ready:
```bash
wine start cmd /c exit
```

Associate Wine with `.exe` files:
```bash
xdg-mime default wine.desktop application/x-ms-dos-executable
```

## Universal Linux Packaging Formats

While the preferred way of installing application is via the software repositories, sometimes I want to install applications that are not available there.\
Adding a third-party repository is my main way of doing this, but sometimes the only option is to use a universal packaging format like Snap, Flatpak, or AppImage.

The preferred order of packing formats is:

1. **AppImage** - It's a self-contained executable that doesn't require any additional dependencies and starts quickly.
2. **Flatpak** - It's a containerized format that requires the Flatpak runtime, and is generally slower than AppImage.
3. **Snap** - It's the slowest of the three and has a lot of issues with permissions and sandboxing.\
I don't even bother installing it.

### AppImage
---
To setup AppImage support we don't really have to do anything, but AppImageLauncher makes things a lot easier by moving them to a designated directory and creating desktop entries for them.

Install the x86_64.rpm from their [GitHub releases page](https://github.com/TheAssassin/AppImageLauncher/releases).

Once installed, I start the application and set the path for where the AppImage files are stored to:
```bash
~/.applications
```

### Flatpak
---
Flatpak requires the Flatpak runtime to be installed, which is available in the software repositories.

Install it with:
```bash
sudo zypper install flatpak
```

## Node.js NPM

Unfortunately, a lot of things require Node.js and NPM to be installed, so we might as well install them.

```bash
sudo zypper install npm
```
Do note that `npm` is an alias for the latest npm version in the repositories, and will also install `nodejs`.

## Development Essentials

Even if you don't plan on doing any development, it's a good idea to have the development essentials installed so that you can grab the source code of any application and compile it if needed.

```bash
sudo zypper install -t pattern devel_basis
sudo zypper install dkms kernel-default-devel
```
