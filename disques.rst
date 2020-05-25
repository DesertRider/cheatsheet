Disques, partitions, multipath, ...
===================================

Quelques commandes pêle-mêle::

   lsblk -o name,uuid,partuuid
   blkid /dev/sda1
   lsscsi
   lsusb
   lsscsi
   lscpu
   lspci
   #--- Voir des informations sur un disque, selon udev
   udevadm info --query=all --name=/dev/sda
   #--- listes des informations sur les disques scsi
   scsi_id --page=0x80-0x83 --whitelisted --device=/dev/sda

   
Reliées aux partitions::

   parted
   fdisk
   cfdisk
   sfdisk
   mkfs.ext4, mkfs.xfs
   e2label
   tune2fs
   mke2fs
   
Reliées aux disques::

   rescan-scsi-bus.sh --forcerescan
   # provient du package sg3_utils
   # si disk remove
   rescan-scsi-bus.sh -d
   # si resize d'un disque au lieu d'un ajout:
   rescan-scsi-bus.sh -s
   
Multipath::

   service multipathd reload
   
   # console multipath
   multipathd -k
   multipathd> list maps
   
   # multipathd avec mots clé
   multipathd -k"keyword"
   pour lister: multipathd -k"help" 


   multipath -ll


   
