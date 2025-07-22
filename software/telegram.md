# Telegram

One of the few applications I actually install manually.\
And this is mostly because I really like how Telegram updates itself.

We'll basically do the Windows thing, where we download it ourselves and extract it to a directory we want.\
I like to place it in `/opt`, then create a symlink to our local bin directory.
```bash
curl -L https://telegram.org/dl/desktop/linux -o telegram.tar.xz && sudo tar -xf telegram.tar.xz -C /opt && rm telegram.tar.xz && ln -fs /opt/Telegram/Telegram ~/.local/bin/telegram && ( ~/.local/bin/telegram &> /dev/null &)
```
