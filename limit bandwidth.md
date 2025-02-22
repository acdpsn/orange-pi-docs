# Limit bandwidth with wondershaper

## 1. Uninstall Debian Wondershaper

This version of Wondershaper is outdated and will not work properly.

`sudo apt remove wondershaper`

## 2. Install Wondershaper from GitHub

`git clone https://github.com/magnific0/wondershaper.git`

`cd wondershaper`

`sudo make install`

`sudo which wondershaper`  
This should return `/usr/bin/wondershaper` if it installed correctly.

## 3. Configure wondershaper

> Note: You can list your network devices with `ip addr`.

`sudo nano /etc/systemd/wondershaper.conf`

- change adaptor from `eth0` to `end1`
- set download and upload speeds

## 4. Enable wondershaper as a systemd service

`sudo systemctl enable --now wondershaper.service`

> Note: If you run into this error:
>
> ```
> Job for wondershaper.service failed because the control > process exited with error code.
> See "systemctl status wondershaper.service" and "journalctl > -xeu wondershaper.service" for details.
> ```
>
> Then you need to change the service executable file location.
>
> `sudo nano /usr/local/lib/systemd/system/wondershaper.service`
>
> Change `/usr/sbin/wondershaper` to `/usr/local/sbin/wondershaper` in ExecStart and ExecStop
>
> Save the file and try to enable the service again.

Wondershaper should now be activated upon reboot.

## 5. Test changes

`pipx install speedtest-cli`

`speedtest`

> Note: If you get "ERROR: HTTP Error 403: Forbidden", try running `speedtest --secure`.
