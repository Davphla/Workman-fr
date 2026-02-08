# Workman-FR 🇫🇷

A **French-optimized** variant of the [Workman keyboard layout](https://workmanlayout.org), giving you **direct single-keypress access** to all French accented characters via AltGr — no dead keys, no multi-tap.

Based on the [original Workman layout](https://workmanlayout.org) by OJ Bucao.

## Table of contents

- [Why Workman-FR?](#why-workman-fr)
- [AltGr Layer](#altgr-layer)
- [Installation](#installation)
- [Files](#files)
- [Credits](#credits)


## Why Workman-FR?

Standard Workman (and even `workman-intl`) uses **dead keys** for accents: you press `dead_acute` then `e` to get `é` — two keystrokes every time. [In French](https://www.sttmedia.com/characterfrequency-french), accented characters like **é** (2.13%), **à** (0.54%), **è** (0.35%), **ê** (0.24%) are extremely common. Workman-FR makes them **one keypress** with AltGr.

## AltGr Layer

The accented characters are accessible by holding **AltGr** (Right Alt) and pressing the key. **AltGr+Shift** gives the uppercase version.

```
Base Workman layout:
┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐
│ q │ d │ r │ w │ b │ j │ f │ u │ p │ ; │
├───┼───┼───┼───┼───┼───┼───┼───┼───┼───┤
│ a │ s │ h │ t │ g │ y │ n │ e │ o │ i │  ← home row
├───┼───┼───┼───┼───┼───┼───┼───┼───┼───┤
│ z │ x │ m │ c │ v │ k │ l │ , │ . │ / │
└───┴───┴───┴───┴───┴───┴───┴───┴───┴───┘

AltGr layer (French accents):
┌────┬────┬────┬────┬────┬────┬────┬────┬────┬────┐
│    │    │    │    │    │    │ û  │ ù  │ ü  │ «» │
├────┼────┼────┼────┼────┼────┼────┼────┼────┼────┤
│ à  │ â  │    │    │    │ ë  │ è  │ é  │ ô  │ î  │
├────┼────┼────┼────┼────┼────┼────┼────┼────┼────┤
│    │    │    │ ç  │ æ  │ œ  │ ê  │ €  │ ï  │    │
└────┴────┴────┴────┴────┴────┴────┴────┴────┴────┘
```

## Installation

### Quick install (one-liner)

```bash
sudo curl -fsSL https://raw.githubusercontent.com/Davphla/Workman-fr/master/xorg/workman-fr -o /usr/share/X11/xkb/symbols/workman-fr
```

Then activate it depending on your setup (see below).

### Sway (Wayland)

After installing the symbols file, edit `~/.config/sway/config`:

**Single layout:**
```
input * {
    xkb_layout workman-fr
}
```

**Dual layout with toggle** (keep your current layout + Workman-FR):
```
input * {
    xkb_layout us,workman-fr
    xkb_variant workman-intl,
}

# Toggle between layouts with Super+Shift+F1
bindsym $mod+Shift+F1 input * xkb_switch_layout next
```

Then reload: `swaymsg reload`

### Hyprland (Wayland)

Edit `~/.config/hypr/hyprland.conf`:

**Single layout:**
```
input {
    kb_layout = workman-fr
}
```

**Dual layout with toggle:**
```
input {
    kb_layout = us,workman-fr
    kb_variant = workman-intl,
}

# Toggle between layouts
bind = SUPER SHIFT, F1, exec, hyprctl switchxkblayout all next
```

### GNOME (Wayland / X11)

```bash
# Add workman-fr to your available layouts
gsettings set org.gnome.desktop.input-sources sources "[('xkb', 'workman-fr'), ('xkb', 'us')]"
```

You can also add it via **Settings → Keyboard → Input Sources → +** (search for "Workman-FR" after installing the symbols file).

Toggle layouts with **Super+Space** (default GNOME shortcut).

### KDE Plasma (Wayland / X11)

Go to **System Settings → Keyboard → Layouts**, enable "Configure layouts", click **Add** and search for `workman-fr`.

Or via command line:
```bash
# Temporary activation
setxkbmap workman-fr
```

### X.Org (generic)

```bash
# Activate
setxkbmap workman-fr && xset r 66

# Switch back to US QWERTY
setxkbmap us; xset -r 66
```

To make it permanent, add to `~/.xinitrc` or `/etc/X11/xorg.conf.d/00-keyboard.conf`:
```
Section "InputClass"
    Identifier "keyboard"
    MatchIsKeyboard "yes"
    Option "XkbLayout" "workman-fr"
EndSection
```

### xmodmap (legacy)

```bash
xmodmap xmodmap/xmodmap.workman-fr
```

### Linux console (TTY)

```bash
sudo loadkeys linux_console/workman-fr.iso15.kmap
```

To make it permanent, set in `/etc/vconsole.conf`:
```
KEYMAP=workman-fr.iso15
```
(after copying the kmap to `/usr/share/kbd/keymaps/`)

---

### Uninstall

```bash
sudo rm /usr/share/X11/xkb/symbols/workman-fr
```

Then remove or revert any changes made to your compositor/DE config.

## Files

| File | Description |
|------|-------------|
| `xorg/workman-fr` | XKB symbols for X.Org / Wayland |
| `xmodmap/xmodmap.workman-fr` | xmodmap configuration |
| `linux_console/workman-fr.iso15.kmap` | Linux console keymap (ISO-8859-15) |

## Credits

- Original Workman layout by [OJ Bucao](https://workmanlayout.org)
- Original layout files maintained at [workman-layout/Workman](https://github.com/workman-layout/Workman)
- French frequency data from [sttmedia.com](https://www.sttmedia.com/characterfrequency-french)
