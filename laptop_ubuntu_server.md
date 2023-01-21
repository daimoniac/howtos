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

## powerdown HDs when idle - userspace daemon with logging
```
wget https://github.com/adelolmo/hd-idle/releases/download/v1.18/hd-idle_1.18_amd64.deb
dpkg -i hd-idle_1.18_amd64.deb
```
/etc/default/hd-idle:
```
START_HD_IDLE=true
HD_IDLE_OPTS="-i 900 -c ata -l /var/log/hd-idle.log"
```

```
systemctl enable hd-idle
systemctl start hd-idle
```

## disable wifi permanently
```
rfkill block wlan0
```
