```
https://www.youtube.com/watch?v=MFMYs1O1yCY
i3 Migration guide swaywm

Core utils and alternatives:
https://wiki.archlinux.org/title/Core_utilities
https://wiki.archlinux.org/title/List_of_applications

system:
sys audit		: lynis [cmd]
permissions		: opendoas [cmd] sudo replacement which is smaller and more secure
fuzzy finder	: broot [cmd] searches is layers is faster
				: fzf [cmd]
search tool 	: fd [cmd] # filename search
				: ag [cmd]
				: ripgrep[cmd] # grep re
file manager	: lf [tui] no actions defined these will need to be scripted
				: fff [tui] shrinked down version of nnn (bash)
				: zzfm [gui] shrunked down version of spacefm
				: dragon [cmd+gui] utility to connect terminal file managers with gui apps
fs navigation	: zoxide [cmd] # smart cd alternative
				: exa [cmd] # ls alternative
				: rip [cmd] # rm replacement
file copy		: rsync [cmd] # Robocopy on windows
				: rclone [cmd] # cloud-could copy / mount
trash mgmt		: trash-cli [cmd] # freedesktop standard cli trash bin (python3)
launcher		: dmenu / rofi / wofi [gui]
statusbar		: polybar [gui] works well with i3
				: waybar [gui] for hyperland
wm				: sway [gui] # i3 config compatible for wayland
				: hyprland [gui] fast gpu accelerated compositor (wm term in wayland) for wayland
				: i3-gaps-rounded [gui] rounded windows
lock screen		: i3lock-color [gui] colorful lockscreen should not be installed with i3lock
				: swaylock [gui] lockscreen
				: swaylock-effects [gui] swaylock with sfx
				: swayidle [cmd] monitors keyboard mouse to run scripts
logout screen	: wlogout [gui] logout screen for wayland
login manager	: sddm [gui] lightweight login manager fom kde with no dependencies]
				: sx [cmd] lightweight startx alternative bash script
				: wlogout [gui]
hotkey			: sxhkd (simple hotkey daemon) [cmd]
system info		: pstree [cmd]
				: procs [cmd] # ps replacement in rust
				: btop [tui] in python
				: btop++ [tui] in C++
				: glances [tui]
				: mission center [gui] similar to win taskmgr
				: radeontop [tui] gpu monitor
				: bomn [tui] netwok monitor
				: wavemon [tui] wireless monitor
network info	: bandwhich [tui]
power info		: powertop [tui]
power management: tlp [cmd]
				: tlp-gui [gui]
				: cpufreq [cmd]
				: auto-cpufreq [cmd]
media conversion: ffmpeg [cmd]
				: imagemagick [cmd]
media info		: exiftool [cmd]
media player	: cmus [cmd]
wallpaper		: feh [cmd]
				: xwallpaper [???]
				: nitrogen [cmd+gui]
wallpcoloextract: pywal [cmd]
screenshot		: grim [cmd]
				: scrot [cmd]
system tray		: trayer [gui]
notifications	: notify [???]
				: dunst [gui]
				: ntfy [cmd] # deployable server for notificatons
bluetooth		: bluez [???] bluetooth stack
shell			: zsh [cmd] bash compatible / configurable / addons
				: xonsh [cmd] # Python shell
prompt			: starship [cmd]
terminal		: xterm [cmd] default option for many tools
				: kitty [gui]
				: alacritty [gui] # Rust
				: ghostty [gui]
				: urxvt [gui] has a deamon to make it run faster than any other
				: st [gui] fast but no scrollback history etc multiple patches require manual adjustment
terminal muxer	: tmux [tui]
				: screen [tui] GNU non-open
history and run : atuin [cmd]
				: navi [cmd]
command runner	: just [cmd] # make alternative in rust
piping			: pypyp [cmd] # Command piping with python syntax
command helper	: xargs [cmd]
				: xsel [cmd]
display config 	: xrandr [cmd]
ftp server		: uftpd [cmd] # simple tftp and ftp server
file opener		: xdg-open [cmd] # freedesktop standard
				: mimeo
file info		: file [cmd]
pager			: bat [cmd]
wireless switch : rfkill [cmd]
bluetooth mgmt	: bluez [cmd]
wireless		: wpa_supplicant / iwd (smaller, faster, modern replacement) [cmd]
				: networkmanager [cmd] convenience features such as network autoconnect and notifications etc
				: conmanctl [cmd] wifi connection
efi configurator: efibootmgr [cmd] # cat ls sys/firmware/efi/efivars
bootmanager		: systemd-boot [cmd]
downloader		: aria2 [cmd]
				: curl [cmd]
				: httpie [cmd] # postman alternative
JSON Query		: jq / yq / jc / jello
RDP				: xrdp [cmd] # RDP client for Linux
calendar		: khal [tui]
email			: mutt [tui]

Optional:
polkit			: lxsession [goi] permission monitoring
automouting		: udiskie> udisks2 [gui] automouting disks on access
window info		: xprop [gui]
				: sprox [gui]
disk usage		: ncdu [tui]
				: gdu [tui]
				: duf [tui]
				: dua-cli [tui]
disk format		: cfdisk [tui]
watch folder	: entr [cmd]

applications:
duplicate finder: rmlint [cmd] creates scripts to delete duplicate
				: fdupes / jdupes [cmd]
ssh client		: mosh [cmd] better ssh connections which doesn't easily disconnect like openssh
backups			: restic [cmd]
				: borg [cmd]
				: syncthing [webgui]
bookmarks		: buku [cli]
```
