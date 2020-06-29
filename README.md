# emptty
Dead simple Display Manager running in CLI as TTY login, that starts Xorg or Wayland.

![](screenshot.png)

## Configuration

#### /etc/emptty/conf
Default startup configuration. On each change it requires to restart emptty.

`TTY_NUMBER` TTY, where emptty will start.

`SWITCH_TTY` Enables switching to defined TTY number. Default is true.

`PRINT_ISSUE` Enables printing of /etc/issue in daemon mode.

`DEFAULT_USER` Preselected user, if AUTOLOGIN is enabled, this user is logged in.

`AUTOLOGIN` Enables Autologin, if DEFAULT_USER is defined. Possible values are "true" or "false". Default value is false.
__NOTE:__ to enable autologin DEFAULT_USER must be in group nopasswdlogin, otherwise user will NOT be authorized.

`LANG` defines locale for all users. Default value is "en_US.UTF-8"

`DBUS_LAUNCH` Prepends "dbus-launch" before desktop command. Default value is true. If `.emptty` is handled as script, this config is overriden to false.

#### /etc/emptty/motd
Custom file, that prints your own MOTD. Reading this file supports colors (e.g. `\x1b[31m` or `\033[32m`).

#### ${HOME}/.emptty
Optional configuration file, that could be also handled as shell script. If is not presented, emptty shows selection of installed desktops.

`ENVIRONMENT` Selects, which environment should be defined for following command. Possible values are "xorg" and "wayland", "xorg" is default.

`COMMAND` Defines command to start Desktop Environment/Window Manager. This value does not need to be defined, if .emptty file is presented as shell script (with shebang at the start and execution permissions).

`LANG` Defines locale for logged user, has higher priority than LANG from global configuration

#### /etc/emptty/custom-sessions/
Optional folder for custom sessions, that could be available system-wide, but do not have .desktop file stored on standard paths for Xorg or Wayland sessions. Expected suffix of each file is ".desktop".

`Name` Defines name of Desktop Environment/Window Manager.

`Exec` Defines command to start Desktop Environment/Window Manager.

`Environment` Selects, which environment should be defined for following command. Possible values are "xorg" and "wayland", "xorg" is default.

## Build & install

### Build dependencies
- go
- gcc
- pam-devel

### Dependencies
- pam
- xorg / xorg-server (optional)
- xauth / xorg-xauth (required for xorg)
- mcookie (required for xorg)
- wayland (optional)

---
- `make clean` to cleanup already built binary.
- `make build` to build binary and gzip man page.
---
- `make install` to install binary.
- `make install-pam` to install pam module.
- `make install-manual` to install man page.
- `make install-all` to install binary, pam module and man page.
---
- `make install-config` to create default conf file in /etc/emptty/.
- `make install-runit` to install runit service
- `make install-openrc` to install openrc service
- `make install-systemd` to install systemd service.
---
- `make uninstall` to remove emptty from your system
---

ArchLinux users can install `emptty` using `yay -S emptty-git` or any other AUR helper
