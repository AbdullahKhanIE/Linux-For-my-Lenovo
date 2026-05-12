# Linux-For-my-Lenovo


Alright — we’ll build you a **clean, beginner-safe, “don’t-break-my-system” setup** for:

* 🧠 keyd (Caps = Vim-style control layer)
* 🪟 Hyprland (Vim movement: HJKL)
* 🌐 OpenBangla Keyboard + Fcitx5 (Bangla typing support)
* 🇧🇩 proper language switching (Bangla ↔ English)
* 💻 coding + browser + terminal workflow

No overengineering. Just a solid base.

---

# 🧱 PART 1 — Install everything you need

Run:

```bash
sudo pacman -S keyd fcitx5 fcitx5-configtool fcitx5-gtk fcitx5-qt fcitx5-mozc
```

Now install Bangla engine:

```bash
sudo pacman -S fcitx5-m17n
```

(We will also support OpenBangla Keyboard later)

---

# ⚙️ PART 2 — Enable Fcitx5 (Bangla system support)

## 1. Set environment variables

Edit:

```bash
nano ~/.config/environment.d/env.conf
```

Add:

```ini
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
SDL_IM_MODULE=fcitx
```

---

## 2. Enable fcitx5

```bash
fcitx5 &
```

To autostart in Hyprland:

```ini
exec-once = fcitx5 -d
```

---

## 3. Configure languages

Run:

```bash
fcitx5-configtool
```

Add:

* English (default)
* Bengali (m17n or OpenBangla Keyboard input method)

---

# 🧠 PART 3 — keyd (Caps = Vim brain system)

## 1. Install + enable

```bash
sudo pacman -S keyd
sudo systemctl enable --now keyd
```

---

## 2. Create config

```bash
sudo nano /etc/keyd/default.conf
```

Paste:

```ini
[ids]
*

[main]
capslock = overload(meta, esc)
```

---

## 🧠 What this gives you

| Action    | Result                       |
| --------- | ---------------------------- |
| Tap Caps  | Esc                          |
| Hold Caps | Super (Hyprland control key) |

---

# 🪟 PART 4 — Hyprland Vim-style movement

Edit:

```bash
nano ~/.config/hypr/hyprland.conf
```

---

## 🧭 Focus movement (Vim style)

```ini
bind = $mainMod, H, movefocus, l
bind = $mainMod, J, movefocus, d
bind = $mainMod, K, movefocus, u
bind = $mainMod, L, movefocus, r
```

---

## 🪟 Move windows

```ini
bind = $mainMod SHIFT, H, movewindow, l
bind = $mainMod SHIFT, J, movewindow, d
bind = $mainMod SHIFT, K, movewindow, u
bind = $mainMod SHIFT, L, movewindow, r
```

---

## 📦 Workspaces (fast switching)

```ini
bind = $mainMod, 1, workspace, 1
bind = $mainMod, 2, workspace, 2
bind = $mainMod, 3, workspace, 3
bind = $mainMod, 4, workspace, 4
bind = $mainMod, 5, workspace, 5
```

---

## 📤 Move window to workspace

```ini
bind = $mainMod SHIFT, 1, movetoworkspace, 1
bind = $mainMod SHIFT, 2, movetoworkspace, 2
bind = $mainMod SHIFT, 3, movetoworkspace, 3
```

---

## 💻 Core apps

```ini
bind = $mainMod, RETURN, exec, kitty
bind = $mainMod, B, exec, firefox
bind = $mainMod, D, exec, wofi --show drun
```

---

## ❌ Window control

```ini
bind = $mainMod, Q, killactive
bind = $mainMod, F, fullscreen
bind = $mainMod, V, togglefloating
```

---

## 🧭 Resize mode (optional but powerful)

```ini
bind = $mainMod, R, submap, resize

submap = resize
bind = , H, resizeactive, -20 0
bind = , L, resizeactive, 20 0
bind = , K, resizeactive, 0 -20
bind = , J, resizeactive, 0 20

bind = , ESCAPE, submap, reset
bind = , RETURN, submap, reset
```

---

# 🌐 PART 5 — OpenBangla Keyboard support

## Install (if not already)

```bash
sudo pacman -S openbangla-keyboard
```

---

## Enable inside Fcitx5

Run:

```bash
fcitx5-configtool
```

Add input method:

* OpenBangla Keyboard

---

## Switching language

Default hotkey:

```
Ctrl + Space
```

You can change it in fcitx5 settings.

---

# 🇧🇩 PART 6 — Bangla + English workflow (IMPORTANT)

You will now have:

| Mode    | Use                      |
| ------- | ------------------------ |
| English | coding, terminal, system |
| Bangla  | writing, chat, notes     |

Switch using:

```
Ctrl + Space
```

---

# 🧠 PART 7 — FINAL MENTAL MODEL

You now operate like this:

## 🧠 Keyboard brain

* Caps = command brain (Super + Esc)
* HJKL = movement everywhere
* Shift = move windows
* Numbers = workspaces

---

## 🌐 Language brain

* Ctrl + Space = Bangla ↔ English
* Fcitx5 handles input switching
* OpenBangla gives phonetic typing

---

# 🚀 RESULT (what you just built)

You now have:

### 💻 i3-style power

* instant workspace switching
* zero mouse dependency

### 🧠 Vim-style movement

* HJKL everywhere
* consistent mental model

### 🇧🇩 Bangla support

* proper input system
* fast switching

### ⚡ modern Hyprland workflow

* smooth animations
* dynamic tiling
* fast app launching

---
