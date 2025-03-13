## Using the theme's built-in status modules

To use the theme's built in status modules, set the `status-left` and
`status-right` tmux options _after_ the plugin has been loaded with `run`.

The tmux status line modules are set as variables and prefixed with `@catppuccin_status_<module>`.

To use the `application` and `session` modules on the right and have nothing on
the left:

```sh
set -g status-right-length 100

set -g status-right "#{E:@catppuccin_status_application}#{E:@catppuccin_status_session}"
set -g status-left ""
```

## Customizing modules

Every module supports the following overrides:

### Override the specific module icon

```sh
set -g @catppuccin_[module_name]_icon "icon"
```

### Override the specific module color

```sh
set -g @catppuccin_[module_name]_color "color"
```

### Override the specific module text

```sh
set -g @catppuccin_[module_name]_text "text"
```

### Override the specific module's background color

```sh
set -g @catppuccin_status_[module_name]_bg_color "#{@thm_surface_0}"
```

### Removing a specific module option

```sh
set -g @catppuccin_[module_name]_[option] ""
```

This is for the situation where you want to remove the icon from a module.
For example:

```sh
set -g @catppuccin_date_time_icon ""
```

### Notes for TPM users

Make sure you load the catppuccin theme prior to setting the status-left and/or
status-left options. This ensures the catppuccin options (such as colors and
status modules) are defined so they can then be used.

After status-left and/or status-left have been set, make sure to run TPM to load
the modules. This runs any plugins that may replace text in the status line.

```bash
# load catppuccin theme ...
run '~/.config/tmux/plugins/tmux/catppuccin.tmux' # or where this file is located on your machine

# ... and then set status-left & status-right ...
set -g status-left "#{E:@catppuccin_status_session}"

set -g status-right "#{E:@catppuccin_status_[module_name]}"
set -ag status-right "#{E:@catppuccin_status_[module_name]}"
set -agF status-right "#{E:@catppuccin_status_[module_name]}"

# ... and finally start TPM
set -g @plugin 'tmux-plugins/tpm'
run '~/.tmux/plugins/tpm/tpm'
```
