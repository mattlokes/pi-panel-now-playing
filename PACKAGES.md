# System packages

Measured on a fresh Raspberry Pi OS Lite (trixie, arm64) on a Pi 5, with
pi-panel-core already installed and `--no-install-recommends`. They match
`[system]` in `pi-panel.toml`.

```
python3-gi              # PyGObject: must match the system GTK, so the venv sees system site-packages
gir1.2-gtk-4.0          # GTK 4 (pulls in the Gdk, Gsk, Graphene, Pango and PangoCairo typelibs)
```

These pull in about 55 packages (GTK 4, cairo, pango, fontconfig, adwaita-icon-theme).
GL comes from Mesa, which pi-panel-core's wlroots already brings in.

GTK's Recommends are not needed: `libgtk-4-bin`, `librsvg2-common`,
`libgtk-4-media-gstreamer` and `iso-codes`. The app uses no icons, and its
font (Inter) is bundled and loaded through PangoCairo. `fonts-dejavu-core`
arrives as a Depends and is the fallback.

## Not from apt

- `uv` (from the core), for `[build]`. The venv is made from `/usr/bin/python3` with `--system-site-packages`.
