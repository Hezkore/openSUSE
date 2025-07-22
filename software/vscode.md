# Visual Studio Code

There's Codium and all that, but if you're succumbing to a big heavy IDE, you might as well get all it has to offer.\
And since Microsoft is giving out instructions specifically for openSUSE, we'll just use those.

Import the key and add the repository:
```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\nautorefresh=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" |sudo tee /etc/zypp/repos.d/vscode.repo > /dev/null
```

Install VSCode:
```bash
sudo zypper install code
```
