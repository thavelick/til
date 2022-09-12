# Using ctrl-z to toggle between a program and the terminal

In almost any terminal program you can hit `ctrl-z` to pause it, then run `fg`
to bring it back. With some zsh configuration you can make `ctrl-z` bring back
the program too:

```zsh
# .zshrc
# use ctrl-z to toggle in and out of bg
if [[ $- == *i* ]]; then
  stty susp undef
  bind '"\C-z":" fg\015"'
fi
```

This didn't work in nvim for me. It turns out this is because I'm using Doom
vim which disables `crtrl-z` in `lua/doom/extras/keybindings/core.lua`:

```lua
mappings.map("n", "<c-z>", "<Nop>", opts, "Editor", "disable_suspending", "Disable suspending")
```

Commenting out the offending line fixed me up nicely.

From: https://social.linux.pizza/web/@solene@bsd.network/108973783539676780
