LVM
===

Création d'un disque en LVM
...........................

Créer une partition unique de type 8e::

   fdisk /dev/sdc
   ...

Créer un volume physique LVM utilisant la partition créée::

   pvcreate /dev/sdc1

Création d'un volume group LVM::

   vgcreate volgrp_03 /dev/sdc1

Affichage du volume physique LVM et du volume group créés::

   pvdisplay

Créer volume LVM "lv_data" sur le volume group créé, utiliser 100% de son espace::

   lvcreate --name lv_data -l 100%FREE volgrp_03

Créer le filesystem sur ce volume::

   mkfs.ext4 /dev/volgrp_03/lv_data

Créer le mount point, ajuster fstab et monter::

   mkdir /DATA
   vim /etc/fstab
   cat >> /etc/fstab <<EOD
   /dev/mapper/volgrp_03-lv_data /DATA                ext4     defaults        0 0
   EOD
   
MONTER LE VOLUME::

   mount -a


Extension d'une partition LVM existante
.......................................

Agrandir le disque virtuel, puis rescan du disque::

   echo 1 > /sys/block/sdX/device/rescan # where X is b/c/d/whatever your disk is
   
Créer partition primaire de type 8e (ex: sdf)::

   fdisk /dev/sdf
   partprobe

Créer le volume physique::

   pvs
   pvcreate /dev/sdf1
   pvs

Ajouter le nouveau LVM Physical Volume au Volume Group::

   vgs
   vgextend reload-data /dev/sdf1
   vgs

Expansion du Logical Volume à 100% de l'espace free::

   lvs
   lvdisplay
   # noter le path du volume logique à étendre: /dev/... (ligne LV Path)
   lvextend -l +100%FREE /dev/reload-data/lvdata
   lvs

Resize du file system EXT3 du volume linux::

   # déterminer le type de file system à extensionner
   cat /etc/fstab
   # si ext3 ou ext4:
   df -h
   resize2fs -p /dev/reload-data/lvdata
   df -h
   # ou si XFS:
   xfs_growfs /var


AJOUT d'un disque et d'une partition LVM
........................................

Ajouter disque physique ou virtuel, puis rescan du disque::

   for HOST in /sys/class/scsi_host/host* ; do echo "- - -" > $HOST/scan ; done
   # fdisk partition, créer partition primaire de type 8e (ex: sdf)
   fdisk /dev/sdc
   partprobe

Créer le volume physique::

   pvs
   pvcreate /dev/sdc1
   pvs

Ajouter le nouveau LVM Physical Volume au Volume Group::

   vgs
   vgcreate volgrp_03 /dev/sdc1
   vgs

Expansion du Logical Volume à 100% de l'espace free::

   lvs
   lvdisplay
   lvcreate -n lv_bkp -l 100%FREE volgrp_03
   lvdisplay volgrp_03/lv_bkp

Créer le file system XFS du volume linux::

   mkfs.xfs /dev/volgrp_03/lv_bkp
   mkdir /backup
   mount /dev/sdc1
   # ou ajuster /etc/fstab et mount -a




Autres commandes LVM
....................

o pvscan - scan all disks for physical volumes
o lvscan - scan all disks for logical volumes


