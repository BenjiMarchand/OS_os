# Full Sheat Sheat
## Montage
### Monter une partition : #mount (partition/disque) (répertoire_de_destination)
o Exemple : mount /dev/sda6 /home/test
o Pour prouver : /proc/mounts
### Pour monter automatiquement au démarrage : #nano /etc/fstab
o Rajouter la commande dans le fichier :
o (partition/disque) (répertoireDeDestination) (Letype) (lesOptions) 0 0
▪ Type = ext4,ext3,ext = si inconnu = auto
▪ Les options par défaut = Defaults
▪ Userquota est une option
### Pour connaître le nom des partitions : #df ou #df -h
## Partitionnement
### Fdisk -l = permet d’afficher les disques présente sur la machine
### Fdisk (partition) = Permet de partitionner un disque
o T = permet de changer le type
o N = permet de créer une nouvelle partition
o P = Afficher les partitions
o W = sauvegarder et quitter
o Q = Quitter en sauvant
### Pour créer une partition :
o Mettre « n », le numéro de la partition, valeur du cylindre par défaut, entrez
la taille si demandez, retourner dans le menu principal puis taper « t » pour
changer le type et « fd »
## RAID
### Télécharger le paquet : #apt-get install mdadm
### Commande mdadm : #mdadm --OPTIONS (partition) --level= --raid-device= (notez
pour finir les noms des partitions
### Option pas mal pour que ça fonctionne :
o --create = création
o --level = Le type de raid de 1 à 5
o --raid-devices = indiquer les disques durs qui vont être utiliser, ils devrontalors tous être marqué après le chiffre en fin de commande
o --spare-devices = indique le spare disque
