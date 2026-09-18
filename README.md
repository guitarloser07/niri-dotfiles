# niri-dotfiles

Personal user-layer configs for `fedora-niri-atomic`. Managed with [chezmoi](https://www.chezmoi.io).

The image repo (`fedora-niri-atomic`) ships only the system layer: packages,
flatpaks, GDM, `niri.desktop`, and a minimal fallback `/etc/niri/config.kdl`
that boots to a working Niri + Noctalia session. Everything opinionated lives
here and shadows the fallback once applied.

## Layout (chezmoi `dot_` convention)

```
dot_config/niri/config.kdl       -> ~/.config/niri/config.kdl (complete file, shadows /etc)
dot_config/noctalia/config.toml  -> ~/.config/noctalia/config.toml
dot_config/kitty/kitty.conf      -> ~/.config/kitty/kitty.conf
dot_config/gtk-3.0/gtk.css       -> ~/.config/gtk-3.0/gtk.css
dot_config/gtk-4.0/gtk.css       -> ~/.config/gtk-4.0/gtk.css
```

Note: Niri does not merge system + user configs. `~/.config/niri/config.kdl`
fully replaces `/etc/niri/config.kdl`, so keep this copy complete.

## Apply on a fresh rebase

```sh
sh -c "$(curl -fsLS get.chezmoi.io)" -- init --apply guitarloser07/niri-dotfiles
```

## Iterate

```sh
chezmoi edit ~/.config/niri/config.kdl   # or edit dot_config/... directly
chezmoi apply
niri msg action load-config-file          # or restart session
```
