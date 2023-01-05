# power management
## automatic tuning
https://rhea.dev/articles/2017-07/Home-server-Power-saving
```
powertop --calibrate
```

`/lib/systemd/system/powertop.service`:
```
[Unit]
Description=PowerTOP autotuner

[Service]
Type=oneshot
ExecStart=/usr/sbin/powertop --auto-tune

[Install]
WantedBy=multi-user.target
```

## keep laptop running when lid is closed
`/etc/systemd/logind.conf`:
```
HandleLidSwitch=ignore
HandleLidSwitchExternalPower=ignore
LidSwitchIgnoreInhibited=no
```

## switch off display when lid is closed and after timeout
`/etc/default/grub`:
add to cmdline
```
consoleblank=60
```

`/etc/systemd/system/blank.service`:
```
[Unit]
Description=Enable virtual console blanking and poweroff

[Service] 
Type=oneshot 
Environment=TERM=linux 
StandardOutput=tty 
TTYPath=/dev/console 
ExecStart=/usr/bin/setterm --powerdown=1 --powersave on

[Install] 
WantedBy=multi-user.target
```

