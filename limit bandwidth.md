# Limit bandwidth with wondershaper

## 1. Install tools

`sudo apt install wondershaper ifupdown isc-dhcp-client`

## 2. Backup network interfaces config

`sudo cp /etc/network/interfaces /root/backup.interfaces`

Now if anything goes wrong, you can restore your config with `sudo cp /root/backup.interfaces /etc/network/interfaces`.

## 3. Set bandwidth limitations

> Note: You can list your network devices with `ip addr`.

`sudo nano /etc/network/interfaces`

Paste the following lines:

```bash
auto end1
iface end1 inet dhcp
    up /sbin/wondershaper end1 1024 512
    down /sbin/wondershaper remove end1
```

Save changes and exit nano.

## 4. Apply changes

`sudo ifdown end1 && sudo ifup end1`

> Note: May give the message "ifdown: interface end1 not configured". This does not mean something went wrong.

## 5. Test changes

`pipx install speedtest-cli`

`speedtest`

> Note: If you get "ERROR: HTTP Error 403: Forbidden", try running `speedtest --secure`.

Results should be around 1024 Kb up and 512 Kb down.
