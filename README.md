# System Metrics (GNOME Shell extension)

**UUID:** `system-metrics@ubuntu`  
**Version:** 17 (see [system-metrics@ubuntu/metadata.json](system-metrics@ubuntu/metadata.json))

CPU, GPU, RAM, swap, and network metrics in the GNOME top bar, with a detailed dropdown menu. Works on GNOME Shell 45+ (Wayland or X11).

## Features

- **Status bar** — Compact CPU, RAM, swap, upload/download (and optional CPU temperature), with optional monochrome mode and spacing controls.
- **Dropdown menu** — Larger cards for CPU, GPU (NVIDIA/AMD when detected), RAM, swap, and network.
- **External monitor (v17)** — Click the **system-monitor** icon in the menu header to launch htop, btop, `top`, GNOME System Monitor, or a custom command. The **open-menu** icon next to it opens extension settings.

## Requirements

- GNOME Shell 45–50.x (as listed in `metadata.json`)
- For TUI monitors: a terminal launcher (default uses `xdg-terminal-exec`; common on recent Ubuntu/GNOME)
- Optional: `htop`, `btop`, `gnome-system-monitor`, GPU tools as needed for the features you enable

## Install

Paths below assume this repo lives at `/mnt/Storage/Progs/sysmonitor`. Adjust if your mount point differs (e.g. `/run/media/.../Storage/...`).

### From zip (recommended)

```bash
gnome-extensions install --force \
  "/mnt/Storage/Progs/sysmonitor/system-metrics/system-metrics.zip"
gnome-extensions enable system-metrics@ubuntu
```

### Manual

```bash
cp -r /mnt/Storage/Progs/sysmonitor/system-metrics/system-metrics@ubuntu \
  ~/.local/share/gnome-shell/extensions/
glib-compile-schemas \
  ~/.local/share/gnome-shell/extensions/system-metrics@ubuntu/schemas
gnome-extensions enable system-metrics@ubuntu
```

After install, or if the extension does not pick up new settings:

```bash
gnome-extensions disable system-metrics@ubuntu && gnome-extensions enable system-metrics@ubuntu
```

On **Wayland**, log out and back in if the panel icon or settings are missing.

## Settings

Open **Extensions → System Metrics → settings**, or the gear icon in the dropdown header.

| Section | What it controls |
|--------|-------------------|
| **Timing** | Refresh interval (1–10 seconds) |
| **Status bar** | Which metrics appear in the panel; monochrome mode |
| **Status bar spacing** | Gaps, padding, optional `\|` separators |
| **Dropdown menu** | Show/hide GPU card |
| **External monitor** | App launched from the header monitor icon |

### External monitor

| Application | Behavior |
|-------------|----------|
| Htop / Btop / Top | Runs inside your **Terminal launcher** prefix |
| GNOME System Monitor | Launched as a GUI app (no terminal) |
| Custom command | Full command you enter (e.g. `foot -e btop`) |

**Terminal launcher** examples:

| Terminal | Prefix |
|----------|--------|
| Default (Ubuntu/GNOME) | `xdg-terminal-exec --` |
| GNOME Terminal | `gnome-terminal --` |
| Alacritty | `alacritty -e` |
| Konsole | `konsole -e` |

If the configured launcher binary is missing, the extension migrates on enable to the first available standard launcher on your system.

## Layout

```text
sysmonitor/system-metrics/
├── README.md               ← this file
├── system-metrics.zip      ← package for gnome-extensions install
├── backups/                ← older zip backups
└── system-metrics@ubuntu/  ← extension source
    ├── extension.js
    ├── prefs.js
    ├── metadata.json
    ├── stylesheet*.css
    ├── icons/
    └── schemas/
```

Rebuild the zip after editing sources:

```bash
cd /mnt/Storage/Progs/sysmonitor/system-metrics
glib-compile-schemas system-metrics@ubuntu/schemas
rm -f system-metrics.zip
zip -r system-metrics.zip system-metrics@ubuntu
```

## Troubleshooting

**Monitor icon does nothing**

1. Check logs: `journalctl -b --no-pager | grep 'System Metrics' | tail -10`
2. Confirm `htop` (or your choice) is installed: `command -v htop`
3. Set **Terminal launcher** to `xdg-terminal-exec --` if you do not use `gnome-terminal`
4. Reload the extension (disable/enable) or log out on Wayland

**Metrics missing or stale**

- Increase refresh interval if CPU use from the extension itself is a concern
- GPU card appears only when a supported GPU is detected

## Changelog (recent)

- **v17** — Clickable header monitor icon; external monitor preferences; `xdg-terminal-exec` default and auto-migration when the configured terminal is missing

## License

Personal/local copy unless otherwise noted. Update `metadata.json` `url` if you publish the extension elsewhere.
# system-metrics
# system-metrics
