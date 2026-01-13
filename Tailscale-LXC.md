# Tailscale LXC setup
**Install-** `curl -fsSL https://tailscale.com/install.sh | sh`
**start-** `sudo tailscale up`
**On the Proxmox host, edit the container config:** 
`nano /etc/pve/lxc/<CTID>.conf`

**Add all of these lines at bottom:**
```
lxc.cgroup2.devices.allow: c 10:200 rwm
lxc.mount.entry: /dev/net/tun dev/net/tun none bind,create=file
features: keyctl=1,nesting=1
```

**Then restart the container**

**Inside the container:**
```
sudo systemctl restart tailscaled
sudo tailscale up
```
**If no response:**
`journalctl -u tailscaled --no-pager -n 50`
*(In logs the **LOGIN** will be there)*


#### ADDITIONAL
**Exit-node + subnet router:**
sudo tailscale set --advertise-routes=10.0.0.0/24 --advertise-exit-node
