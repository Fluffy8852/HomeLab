# Proxmox - Removing local-lvm from config
## Remove local-lvm from Proxmox config
``pvesm remove local-lvm``

## Remove the thin pool
``lvremove /dev/pve/data``

## Extend the root logical volume
``lvextend -l +100%FREE /dev/pve/root``

## Resize the filesystem
``resize2fs /dev/pve/root``
