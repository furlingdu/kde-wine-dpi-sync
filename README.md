# kde-wine-dpi-sync

Automatic Wine scaling script for KDE.

Wine ignores the KDE display scale and renders Windows programs at 96 DPI. This script keeps the Wine DPI in sync with the KDE display scale, so Windows programs match the size of native programs.

## Install

```sh
install -Dm755 wine-dpi-sync ~/.local/bin/wine-dpi-sync
install -Dm644 systemd/wine-dpi-sync.service ~/.config/systemd/user/wine-dpi-sync.service
install -Dm644 systemd/wine-dpi-sync.timer ~/.config/systemd/user/wine-dpi-sync.timer
install -Dm644 systemd/wine-dpi-sync.path ~/.config/systemd/user/wine-dpi-sync.path
systemctl --user daemon-reload
systemctl --user enable --now wine-dpi-sync.timer wine-dpi-sync.path
```

## Usage

```sh
wine-dpi-sync --status
```

Changing the display scale triggers a sync right away. A timer checks every 60 seconds as a fallback. Already running Windows programs need a restart to pick up the new DPI.

## Extra Wine prefixes

Add one prefix path per line to `~/.config/wine-dpi-sync.conf`

## How it works

The script reads `Xft.dpi` from the X server and writes `LogPixels` to the Wine prefix registry at `HKCU\Control Panel\Desktop`

## License

AGPL-3.0
