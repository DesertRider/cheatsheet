LVM
---

Création d'un disque en LVM

# Création d'une partition unique de type 8e

``
   Fdisk /dev/sdc <<FIN
   n
   p
   1


   t
   8e
   w
   FIN
   ``

# Création d'un volume physique LVM utilisant la partition créée

``pvcreate /dev/sdc1``

# création d'un volume group LVM

``vgcreate volgrp_03 /dev/sdc1``

# affichage du volume physique LVM et du volume group créés

``pvdisplay``

# Créer volume LVM "lv_data" sur le volume group créé, utiliser 100% de son espace

``lvcreate --name lv_data -l 100%FREE volgrp_03``

# Créer le filesystem sur ce volume

``mkfs.ext4 /dev/volgrp_03/lv_data``

# Créer le mount point, ajuster fstab et monter

``
   mkdir /DATA
   vim /etc/fstab
   # ajouter cette ligne
   /dev/mapper/volgrp_03-lv_data /DATACMS                  ext4     defaults        0 0
``

# MONTER LE VOLUME

``mount -a``

# --- EXTENSION d'une partition LVM existante ---

# 1) ajouter expace disque par VMware
# rescan du disque...
echo 1 > /sys/block/sdX/device/rescan # where X is b/c/d/whatever your disk is
# fdisk partition, créer partition primaire de type 8e (ex: sdf)
fdisk /dev/sdf
# si erreur à l'écriture de la table de partition (le kernel indique que le device is busy, new table will be use on next reboot)
partprobe

# 2) créer le volume physique
pvs
pvcreate /dev/sdf1
pvs

# 3) Ajouter le nouveau LVM Physical Volume au Volume Group
vgs
vgextend reload-data /dev/sdf1
vgs

# 4) Expansion du Logical Volume à 100% de l'espace free
lvs
lvdisplay
# noter le path du volume logique à étendre: /dev/... (ligne LV Path)
lvextend -l +100%FREE /dev/reload-data/lvdata
lvs

# 5) Resize du file system EXT3 du volume linux
# 5.1) déterminer le type de file system à extensionner
cat /etc/fstab
# 5.2) ext3 ou ext4:
df -h
resize2fs -p /dev/reload-data/lvdata
df -h
# ou si XFS:
xfs_growfs /var

# --- AJOUT d'un disque et d'une partition LVM ---

# 1) ajouter expace disque par VMware
# rescan du disque...
for HOST in /sys/class/scsi_host/host* ; do echo "- - -" > $HOST/scan ; done
# fdisk partition, créer partition primaire de type 8e (ex: sdf)
fdisk /dev/sdc
# si erreur à l'écriture de la table de partition (le kernel indique que le device is busy, new table will be use on next reboot)
partprobe

# 2) créer le volume physique
pvs
pvcreate /dev/sdc1
pvs

# 3) Ajouter le nouveau LVM Physical Volume au Volume Group
vgs
vgcreate volgrp_03 /dev/sdc1
vgs

# 4) Expansion du Logical Volume à 100% de l'espace free
lvs
lvdisplay
lvcreate -n lv_bkp -l 100%FREE volgrp_03
lvdisplay volgrp_03/lv_bkp

# 5) Création du file system XFS du volume linux
mkfs.xfs /dev/volgrp_03/lv_bkp
mkdir /backup
mount /dev
# ou ajuster /etc/fstab et mount -a




# --- autres commandes LVM ---
pvscan
lvscan
pvdisplay
lvdisplay

