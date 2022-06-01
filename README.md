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

## LVM
### Installer le paquet : #apt-get install lvm2
### Créer le volume physique :
o Pvcreate (partition)
### Créer le groupe de volumes :
o Vgcreate (VolumeGroupName) (PhysicalVolume)
### Créer le volume logique :
o lvcreate -n (nom) -L (taille mémoire en gb), -l (mémoire en %) NOM_GROUPE
## 1. Système files
### Mkfs -V -t ext4 /dev/sd.. = formater une partition logique
### Mkfs.ext4 /dev/sd.. = partition physique
## 2. Astuce archives
### ASTUCE : Toujours créer une archive d’un répertoire qu’on veut placer sur notre LVM comme /home
### Télécharger le paquet : #apt-get install bzip2
### Créer l’archive : tar -jcf backup.tar.bz2
### Afficher le contenu de l’archive : tar -jtf backup.tar.bz2
### Extraire le contenu de l’archive : tar -C / -jxf backup.tar.bz2
## Quotas
### Télécharger le fichier : #apt-get install quota
### Allez dans le fichier : #nano /etc/fstab
o À la ligne du « /home » rajouter « usrquota après defaults et reboot
### Créer les fichier quotas :
o #cotacheck -c (chemin du point montage)
### Pour vérifier si c’est bien fait :
o #cotacheck -mv (chemin du point montage)
### Pour initialiser les quotas :
o #quotacheck -vgum (chemin du point)
### Pour modifier le quota d’un user :
o #Edquota <user>
▪ Dans le fichier modifier STRICTE (HARD EN ANGLAIS) ET SOUPLE (SOFTEN ANGLAIS)
▪ 1000 = 1 Mo
### Vérifiez : repquota <point de montage/chemin repertoire>

## NTP
- Télécharger le paquet : #apt-get install ntp
- Démarrer/arrêter le service :
o Service ntp start/stop/restart
- Vérification la synchronisation des serveurs :
o Ntpq -p
- Service ntp status
- Aller dans le Fichier de configuration : /etc/ntp.conf
o Restreindre un réseau :
▪ restrict (réseau) mask (masque) nomodify notrap
▪ OU
▪ Restrict (reseau) mask (masque) ignore
o restreindre tout le monde :
▪ restrict default ignore
## Réseaux
### Fichier de configuration : /etc/network/interfaces
### Allow-hotplug interface : autoriser le branchement à chaud
### Obligatoire si « static » :
o Iface interface inet dhcp/static
o Address X.X.X.X
o Netmask X.X.X.X
o Gateway X.X.X.X
### Afficher les interfaces → ip addr
### Restart le service → service networking restart
### Ifup/down pour shut/start l’inter

  ## SSH
- Télécharger le paquet serveur : #apt-get install ssh
- Télécharger le paquet client : #apt-get install openssh-client
- Génerer une paire de clé ssh : #ssh-keygen -t rsa
- Transférer la clé publique : # scp -p (fichier) (user)@(ip destination) : (les 2 points
sont importants)
- Créer un fichier cacher : #mkdir .ssh (pas oublier le point)
- Pour autoriser une connection sur notre serveur ssh :
o Allez dans le fichier « /etc/.ssh/authorized_keys
▪ Copier la clé public dedans
- Fichier de configuration : /etc/ssh/sshd_config
o PermitRootLogin no → empêche root de se connecter en ssh
o AllowUsers → permet d’autoriser des utilisateurs à se connecter en ssh
o PasswordAuthentication no → bloque l’identification par mdp
o UsePam no → Empeche d’utiliser PAM → à faire après avoir fait l’échange declé
  
## 
