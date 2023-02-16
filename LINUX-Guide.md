# ADMINISTRATION LINUX

## SOMMAIRE

1. [Commandes de bases](#commandes-de-bases)
2. [Grub](#grub)
3. [SystemD](#systemd)
4. [Password](#password)
5. [Maintenance via Grub](#maintenance-via-grub)
6. [Gestion Réseaux](#gestion-reseaux)
7. [Gestion des paquets logiciels](#gestion-des-paquets-logiciels)
8. [Gestion des espaces de stockage](#gestion-des-espaces-de-stockage)
9. [Gestion Avancées des espaces de stockage](#gestion-avancee-des-espaces-de-stockages---lvm)
10. [File System](#gestion-des-espaces-de-stockages---file-system)
11. [Gestion des utilisateurs](#gestion-des-utilisateurs)
12. [Droits sur les fichiers et répertoires](#droits-sur-les-fichiers-et-repertoires)
13. [Maintenance d'un système en production](#maintenance-dun-systeme-en-production)
14. [Gestion de la taille des logs](#gestion-de-la-taille-des-logs)
15. [Outils d'analyse](#outils-danalyse-du-systeme)
16. [Performances et Processus](#performances-et-processus)
    
## COMMANDES DE BASES

Liste de commandes basiques

- `passwd`

  Changer de mot de passe:
  - >``passwd username``
- `who`
    
    Permet de connaître les utilisateurs connectés sur le serveur
  - >``who``
  - >``who -uH`` (Affiche le temps d'inativité des utilisateurs)
- ``date``
  
    Afficher la date
    >``date +%X`` (Affiche uniquement l'heure)
    >
    >``date "+%A %d %B %Y"`` (Affiche date au format: jour 00 mois AAAA)
- `cal` (Calendrier)
- `pwd` (Position dans l'arborescence)
- `find`
  - >`find /etc -type f -name "ho*"` (Recherche tous les fichiers commençant par ho à partir de /etc)
  - >`find ~ -type d` (Recherche tous les répertoires à partir du répertoire personnel)
  - >`find ~ -type f -name "*txt" -exec cp {} {}.save \;` (Recherche tous les fichiers terminant par txt dans et en faire une copie .save)
  - >`find / -mount -type f -name "*.conf" 2>/dev/null` (Recherche à la racine tous les fichiers .conf en filtrant les erreurs)
- `cat`
  - > `cat fichier` (Lire le contenu d'un fichier)
  - > `cat > fichier` (Création d'un fichier et de son édition)
  - > `cat fichier fichier2 > fichier1+2` (Concaténation de deux fichiers en un)
- `echo`
  - >`echo Hello` (Renvoi Hello en texte)
  - >`echo 'text' > Fichier` (Renvoi la saisie dans un fichier)
  - >`echo 'text2' >> Fichier` (Concaténation de text2 dans Fichier)
- `ls`
  - >`ls -A` (Affiche **TOUS** les fichiers et répertoires)
  - >`ls -l`  (Affiche la liste des fichiers ainsi que les permissions et propriétaires)
  - >`ls -la` (Affiche la liste de **TOUS** les fichiers et répertoires)
  - >`ls -la *.txt` (Affiche la liste de **TOUS** les fichiers ayant pour extension .txt)
  - >`ls -ld /tmp` (Affiche les caractéristiques détaillées du répertoire /tmp pas son contenu)
  - >`ls -d /etc/[a-d]*` (Affiche les fichiers ou répertoires commençant par a,b,c ou d)
  - >`ls -ld /etc/[!aeiouy][a-zA-Z][a-zA-Z][a-zA-Z][a-zA-Z][f-s].conf` (Exemple)
  - >`ls -l fichier* Fichier /tmp/fichier.txt` (Liste détaillée de plusieurs fichier)
- `mkdir` (Création d'un répertoire)
  - >`mkdir dossier` (Création du répertoire *dossier*)
  - >`mkdir -p bin Tp/{Dossier,dossier1,dossier2/{sous-dossier,sous-dossier1}}` (Création de plusieurs répertoire avec sous-dossier et sous-sous-dossier dans *dossier2*)
- `touch` (création de fichier)
  - >`touch fichier`
- `rm` (Commande de supression)
  - >`rm -r fichier` (Suppression d'un fichier)
- `rmdir` (Commande de suppression de dossier)
  - > `rmdir -r repertoire` (Supression d'un répertoire)
- `sudo` (Elevation de privilège)
- `less` (Lire un fichier au fur et à mesure)
- `wc`
  - > `wc -l /etc/passwd` (Affiche le contenu et le nombre de ligne présent dans le document)
- `tee` (Lit les entrées standard et les renvois dans un fichier)
- `grep`
  - >`grep mot Fichier` (Recherche toutes les occurences de 'mot' dans Fichier)
  - >`grep -i mot Fichier` (Recherche toutes les occurences quelque soit la casse)
  - >`grep -v "^$" Edition` (Recherche toutes les lignes non vide dans le fichier Edition)
  - >`grep -sl localhost /etc/*` (Lister les fichiers localhost dans /etc sans inclure les sous-répertoires)
- `tail`
  - >`tail -n2 /etc/hosts` (Affiche les deux dernières lignes d'un fichier)
- `head`
  - > `head -n2 /etc/hosts` (Affiche les deux premières lignes d'un fichier)
Création de lien symbolique et physique:
- `ln`
  - >`ln Source Destinaire` (Lien physique entre le fichier source et destinaire)
  - >`ln -s Source Destinaire` (Lien symbolique entre deux fichiers)
- `ps`
  - `ps -ef` (Enumération des processus en fonction)

## GRUB

Modification de la configuration de GRUB à partir de :

- `/etc/default/grub`
- `/etc/grub.d/`

Regénérer le fichier GRUB à l'aide de `grub-mkconfig` et `update-grub`

*ex:*

> `grub-mkconfig -o /boot/grub/grub.cfg` ou `update-grub`

### Fichiers de démarrage

Fichier indispensables pour le démarrage minimum de Debian:
>`ls -l /boot/`  => vmlinuz-x.x.x & initrd.img-x.x.x

Ligne pouvant être modifier (au démarrage, touche 'e')

>`linux /vm-linuz-4.x.x.x-x-amd64 root=/dev/mapper/debian--vg-root ro quiet`

## SystemD

SystemD est le gestionnaire système, PID 1.

Pour gouverner tous les services:
>`systemctl <action> [cible/service/unit]`

-Afficher la cible par défaut

-Changer de cible par défaut

-Changer de cible directement

-Gérer les services


------ Lister les cibles, services et autres éléments de SystemD ------

Connaître la cible par défaut
>`systemctl get-default`

Changer la cible par défaut

>`systemctl set-default multi-user.target`

Changer de cible

>`systemctl isolate rescue-target`

Lister les divers éléments (units) de SystemD

>`systemctl list-units`


Lister tous les units

>`systemctl list-units --all`

Voir le statut d'un service

>`systemctl status cron.service`

Démarrer un service

>`systemctl start cron.service`

Stopper un service

>`systemctl stop cron.service`

Redémarrer un service

>`systemctl restart cron.service`

Activer un service

>`systemctl enable networking`

Désactiver un service

>`systemctl disable networking`


## PASSWORD

Change user's password:

>`sudo passwd user`


## MAINTENANCE VIA GRUB

### AVEC MOT DE PASSE ROOT
Passer par le boot manager GRUB pour passer en mode Maintenance
Utiliser les flèches pour choisir la ligne du noyau voulu puis appuyez sur [e]

Ligne à modifier:

>`linux /vm-linuz-4.x.x.x-x-amd64 root=/dev/mapper/debian--vg-root ro quiet`

en

>`linux /vm-linuz-4.x.x.x-x-amd64 root=/dev/mapper/debian--vg-root ro single`

Valider avec CTRL+X ou [F10] Saisir le mot de passe ROOT.
Après les actions en mode maintenance, CTRL+D > rescue.target


### ***SANS MOT DE PASSE ROOT***

Mêmes étapes que #AVEC MOT DE PASSE ROOT

>`linux /vm-linuz-4.x.x.x-x-amd64 root=/dev/mapper/debian--vg-root ro init=/bin/bash`

// Connexion en root sans mot de passe

Système est démarré mais système de fichier racine est en lecture seule:

>`mount -o remount, rw /` > Permet d'ajouter l'écriture

Après actions, synchro écriture de données en RAM vers DISK avec command:

> `sync`

/!\ Reboot impossible, extinction par POWEROFF matériel /!\

## GESTION RESEAUX

> `ip a`  Connaître IP ADDRESS
> 
> `ip r`  r = Route  Connaître la passerelle par défaut

Informations DNS:

> `/etc/resolv.conf`
(Possibilité de le modifier pour mettre  un DNS statique)

### CONFIGURATION IP EN DHCP

Fichier pour gérer la partie IP:

 >`/etc/network/interfaces`

Edition du fichier (ne jamais commenter ou effacer les ligne loopback):

>`vim /etc/network/interfaces`

Configuration statique:
>- Modification de la ligne:

`iface ens33 inet dhcp` en:
>`iface ens33 inet static`
> 
>>>address: 10.1.1.10
>>>netmask: 255.255.0.0
>>>gateway: 10.1.255.251

(Possibilité de renseigner l'address avec CIDR /16 dans cette exemple sans renseigner le netmask)

Si l'IP statique n'est pas prise en compte ajouter la ligne suivante au-dessus:

>`auto ens33`

Gérer le service networking

>`systemctl stop/start/restart networking.service`

### CONFIGURATION IP VIA INTERFACE GRAPHIQUE

Network Manager  Clic droit sur l'icone en haut à droite

Paramètres Filaire

>`systemctl restart NetworkManager` ou via interface graphique


## GESTION DES PAQUETS LOGICIELS

### GESTION DES DEPÔTS

Fichier de configuration des dépôts:

>`/etc/apt/sources.list`

Modification du fichier avec toutes les sources à disposition:
>`deb http://ftp.fr.debian.org/ buster main contrib non-free`
> 
>`deb-src http://ftp.fr.debian.org/ buster main contrib non-free`


Lancement mise à jour des paquets (root)

>`apt update` > relecture des paquets (vérification des versions)

>`apt upgrade`  met à jour les nouveaux paquets

>`apt full-upgrade`  Supprimes les paquets obsolètes et installe les nouveaux

Installation des VMWARE TOOLS:

>`apt install open-vm-tools-desktop`

Resélectionner les utilitaires comme à l'installation:

>`tasksel`

Rechercher un paquet en particulier (ftp par exemple):

>`apt search ftp`

## GESTION DES ESPACES DE STOCKAGE

La commande `fdisk`

>`fdisk <option> [périphérique de stockage]`

Afficher la table de partion du périphérique

>`fdisk -l /dev/sdb`

Modifier les partitions du périphérique sélectionné

>`fdisk /dev/sdb`

Obtenir une info d'un disque lorsqu'il n'est pas encore monté: (hôte)

>`udevadm info --query=path --name=sda`

>`echo "- - -" > /sys/class/scsi_host/host#/scan`

>`fdisk -l`

## GESTION AVANCEE DES ESPACES DE STOCKAGES - LVM
Création de volume physique

>pvcreate
>pvcreate /dev/sdb1 /dev/sdb2 /dev/sdc1 /dev/sdd

Création des groupes de volumes

>vgcreate
>vgcreate NomDuGroupe /dev/sdb1 /dev/sdb2 /dev/sdc1

Création des volumes logiques

>lvcreate
>lvcreate -n lv1 -L 10G NomDuGroupe

Les options `-n` et `-L` sont respectivement le nom et la taille.

Deux chemins pour manipuler les Volumes Logiques:

>/dev/vgsystem/lvhome
ou

>/dev/mapper/vgsystem-lvhome

Ajouter des volumes physiques au VG

>vgextend NomDuGroupe /dev/LABEL

Agrandir un Volume Logique: (`-r` = invoque resize2fs / `-L` = Taille)

>lvextend -r -L +512M /dev/NomDuGroupe/LABEL
>lvextend -r -L 1G /dev/NomDuGroupe/LABEL2

Réduire un Volume Logique

>lvreduce -r -L +512M /dev/NomDuGroupe/LABEL

Etendre un volume en prenant tout l'espace libre

>lvextend -l +100%FREE /dev/NomDuGroup/HDD-LABEL

### INFORMATIONS LVM

Toutes les commandes LVM sont disponibles dans un shell dédié, accessible via la commande `lvm`

| Informations Résumées avec `s` | Infos Détaillés avec `display` |  Designation |
| ------------------------------ | ------------------------------ | ---------------------- |
| `pvs` | `pvdisplay` | Volume Physique
| `vgs` | `vgdisplay` | Groupe de volume
| `lvs` | `lvdisplay` | Volume Logique

Exemples:

>vgdisplay vggroup2

>lvdisplay /dev/vggroup2/lv1

>pvdisplay /dev/sdb1

## GESTION DES ESPACES DE STOCKAGES - FILE SYSTEM

**Création de systèmes de fichiers:**

>mkfs.[fstype] <option> [périphérique de stockage]

Exemples:
- Création d'un système de fichiers ext4 sur partition /dev/sda2
>-  `mkfs.ext4 /dev/sda2`
- Création d'un système de fichiers ext4 sur volume logique lv1
>- `mkfs.ext4 /dev/vggroup1/lv1`
- Création d'un système de fichiers NTFS (nécessite le paquet `ntfs-3g`)
>- `mkfs.ntfs /dev/sde1`

**Modification d'un système de fichiers:**

>tune2fs <options> [périphérique de stockage]

Options usuelles:
  - `-L` permet de modifier l'étiquette du système de fichiers
  - `-l` permet d'afficher les informations du superbloc
  - `-i` permet de modifier l'intervalle entre deux vérifications
  - `-c` permet de modifier le nombre maximum de montages déclenchant une vérification

Commande de changement de taille d'un système de fichier:

>resize2fs <options> [périphériques de stockage]

**Vérification d'un système de fichiers**

>fsck.<fstype> <options> [périphérique de stockage]

**Prise d'information**

>blkid <options> [périphérique de stockage]

Cette commande permet d'afficher les informations relatives à un périphériques particulier. Sans argument, elle affichera les informations relatives à tous les périphériques formatés.

>lsblk <options> [périphérique de stockage]

La commande `lsblk` permet d'afficher sous forme arborescente les informations relatives aux périphériques et systèmes de fichiers

### MONTAGE D'UN SYSTEME DE FICHIERS

>mount <options> [périphérique source] [/point/de/montage]

Options possibles:
  - `-t [fstype] `Détermine le type de système de fichier à monter
  - `-o [option]` Permet de définir différentes options séparées par une virgule
  - `sync/async` Active ou non l'utilisation de la mise en tampon RAM des données avant écriture dans le système de fichiers. Par défaut: `async`
  - `exec/noexec` Active la possibilité d'exécuter des fichiers exécutables présents sur le systèmes de fichiers
  - `ro/rw` Monte le système de fichiers en lecture seule ou en lecture/écriture
  - `suid/nosuid` Active la possibilité d'exécuter les binaires avec l'interprétation du SUID positionné au dessus
  - `remount` Permet de changer une ou des options de montage sans démonter le système de fichiers

Exemple:

>ls /mnt
>mount -t ext4 /dev/sdc1 /mnt

**Informations sur les montages**

>mount
>findmnt [/chemin/du/volume]

**Démonter un volume**

>unmount /mnt


### MONTAGE AUTOMATIQUE

Le montage automatique est géré par `systemd` au démarrage.
La déclaration des montages automatiques est présente dans le fichier `/etc/fstab`

**Informations sur les systèmes de fichiers**

>df <options> [/point/de/montage]

Commande permettant d'obtenir des informations utiles sur les systèmes de fichiers montés

Options usuelles:

>-h : affiche la taille en puissance de 1024
>
>-i : affiche les informations sur les inodes

Pour connaître la taille d'un répertoire

>du <options> [/point/de/montage]

Options usuelles:

>-h : affiche la taille en puissance de 1024
>
>-s : n'affiche pas les sous-répertoires mais uniquement le répertoire en argument

Exemple: `du -hs /etc`

## GESTION DES UTILISATEURS

### GESTIONS DES GROUPES

Les informations concernant les groupes d'un système Linux sont contenus dans les fichiers: `/etc/group` et `/etc/gshadow`.

**Nous ne pouvons pas les modifier !**

Analyse de colonnes du fichier `/etc/group`

>nomgroupe:passechiffré:GID:membres,de,ce,groupe,secondaire

exemple:

>informatique:x:1500:jmartin,abenabel,sdia

Dans l'exemple ci-dessus le `x` dans la colonne du mot de passe, indique que le mot de passe est dans le fichier: `/etc/gshadow`

### COMMANDES DE GESTIONS DES GROUPES

Ajouter un groupe:

>groupadd <options> [NomDuGroupe]

Option usuelle:
- `-g [GID]`: valeur numérique de l'identifiant du groupe. Valeur unique.
  
Modifier un groupe existant:

>groudmod <options> [NomDuGroupe]

Option usuelle:
- `-g [GID]` change le GID d'un groupe. Attention aux orphelins des fichiers créés préalablement
- `-n [nouveau nom]` change le nom du groupe

 Supprimer un groupe:

>groupdel <options> [NomDuGroupe]

Administration des groupes:

>gpasswd <options> [NomDuGroupe]

Options usuelles:
- `-a [Utilisateur]` ajoute "Utilisateur" au groupe
- `-d [Utilisateur]` supprime "Utilisateur" au groupe

### GESTION DES UTILISATEURS

Les informations concernant les utilisateurs d'un système Linux sont contenus dans les fichiers `/etc/passwd` et `/etc/shadow`

>passwd <options> [utilisateurs]

Options usuelles:
- `-e [utilisateur]` annuler immédiatement la validité du mot de passe d'un utilisateur. Celui-ci sera obligé de changer son mot de passe à sa prochaine connexion
- `-l [utilisateur]` verrouille le mot de passe en ajoutant "!" devant le hash du mot de passe dans `/etc/shadow`
- `-u [utilisateur]` dévérouille le mot de passe en supprimant "!" devant le hash du mot de passe dans `/etc/shadow`
  
**Ajouter un utilisateur:**

>useradd <options> [utilisateur]

Options usuelles:
- ``-m ``useradd crée le répertoire d'accueil de l'utilisateur
- ``-d [/chemin/rep/accueil]`` répertoire d'accueil de l'utilisateur. Si non indiqué, useradd utilisera le nom de l'utilisateur et la valeur de la variable HOME du fichier /etc/default/useradd
- ``-u [UID]`` indique l'UID de l'utilisateur. Si non renseigné, useradd utilisera le plus petit UID
- `-g [GID]` indique le GID du groupe principal de l'utilisateur
- `-G [groupe1,groupe2,groupen]` indique la liste des groupes secondaires de l'utilisateur séparés par des ","
- `-s` indique le shell de l'utilisateur sous forme du chemin absolu du binaire
- `-r` indique la création d'un utilisateur système
  
Si l'option `-m` est passée à `useradd` alors ce dernier copiera le contenu du répertoire `/etc/skel`dans le répertoire d'accueil de l'utilisateur.

**Modification d'un utilisateur**

>usermod <options> [Utilisateur]

Option usuelles:
- `-d [/home/DIR]` indique le nouveau répertoire d'accueil de l'utilisateur. Si l'option `-m` est fournie, le contenu du répertoire actuel sera déplacé dans le nouveau répertoire d'accueil
- `-e [DATE DE FIN DE VALIDITE]` date à laquelle le compte utilisateur sera désactivé. (Format: AAAA-MM-JJ) Un format vide désactivera l'expiration.
- `-f [DUREE INACTIVITE]` nombre de jours suivant la fin de validité d'un mot de passe après lequel le compte est définivement désactivé. (valeur 0 désactive le compte dès que le mot de passe à dépasser sa fin de validité, -1 désactive cette fonctionnalité)
- `-g [GID]` nom du nouveau groupe principal de l'utilisateur. Tout fichier du répertoire personnel appartiendra désormais au nouveau groupe
- `-G [groupe1,groupe2,groupe*n*]` liste des groupes secondaires de l'utilisateur.
- `-a` ajouter les groupes supplémentaires à l'utilisateur. A n'utiliser qu'avec l'option `-G`
- `-s [shell]` chemin du nouveau shell de l'utilisateur (peut être configurer à l'aide de la commandde `chsh`)
- `-L` verrouille le mot de passe de l'utilisateur. Cette option ajoute un '!' devant le hash du mot de passe dans `/etc/shadow`

Remarque: pour verrouiller le compte (et pas seulement l'accès par mot de passe), il est également nécessaire de placer `DATE_FIN_VALIDITE` à 1

- `-U` déverouille le mot de passe de l'utilisateur
- `-c "COMMENTAIRE"` permet d'ajouter un commentaire
**Suppression d'un utilisateur**

>userdel <options> [Utilisateur]

Option usuelle:
- `-r` les fichiers présents dans le répertoire d'accueil de l'utilisateur seront également supprimés. Les fichiers de l'utilisateur présents dans d'autres répertoires ne seront pas supprimés
 
### CHANGEMENT D'IDENTITE et PRIVESC

>su <options> [utilisateur]

`su` permet de changer d'utilisateur ou d'exécuter une commande sous l'indentité d'un autre user.

`su` peut aussi permettre de devenir **root**

Options usuelles:
- `s [shell]` préciser le shell à utiliser pour l'ouverture de session
- `-` ou `-l [utilisateur]` faire un changement complet d'identité (charges les variables d'environnement de l'utilisateur cible)
- `-c [cmd]`exécuter la commande, il est conseillé de mettre la commande entre simples quote

>
>`sudo <options> [commande]`

La commande `sudo`permet de déléguer des tâches précises d'administration à certains utilisateurs. Par exemple, il sera possible d'accorder les privilèges de gestion des utilisateurs à un groupe d'utilisateurs.

Afin qu'un utilisateur puisse utiliser la commande `sudo`, il faut qu'il soit renseigné dans le fichier de configuration `/etc/sudoers`et renseigner les commandes qu'il pourra utiliser.

## DROITS SUR LES FICHIERS ET REPERTOIRES

### LES DROITS UNIX/LINUX

rwx rwx r-x => Utilisateur Groupe Other

| Droit | Octal | Fichier | Répertoire |
|-------|-------|---------|------------|
|`r` read| 4 | Permet de lire, ouvrir le fichier ex: `cat` | Permet de lister le contenu d'un dossier |
|`w` write | 2 | Permet d'écrire dans le fichier (`r` doit être présent) | Permet de modifier le contenu du dossier (créer, copier, renommer, supprimer) ex: `mkdir cp rm`|
|`x` execution | 1 | Permet d'exécuter un fichier binaire ou script shell (le droit de lecture doit être présent) | Permet à un utilisateur de traverser ou d'accéder à un fichier dans le dossier. Ex: `cd` |

Calculer les droits en octal, il faut additionner les valeurs des droits présents pour les trois groupes.

- rwx = 4+2+1 = 7
- rw- = 4+2 = 6
- r-x = 4+1 = 5
- r-- = 4

Exemples: rwxrwxr-x = 775 | rwxr-x--- = 750 | rw-rw-r-- = 664

Pour afficher les droits d'un fichier ou répertoire, la commande `ls` sera utilisée.

>user@debian:~$ ls -l
>total 2
>drwxr-xr-x 2 user user 4096 16:30 Dossier
>-rw-r--r-- 1 user user 33   17:35 Fichier

### MODIFICATION DES DROITS

>chmod <-R> [ugoa] [+ - =] [rwxX] fichier ou dossier

`chmod` permet la modification des droits, à utiliser de deux façons
- Absolue: en octal ou symbolique avec le signe "="
- Relative: en symbolique avec les signes "+" ou "-"

Attention à l'option `-R`, le fait de réaliser un `chmod`de façon récursive doit être effectué de façon réfléchie et ne doit pas être généralisé à tous les usages.

Modifier les permissions d'un répertoire en notation symbolique

>chmod g+w,o-rx /data/common

Modifier les permissions d'un répertoire en notation octal

>chmod 770 /data/common

Modifier les permissions d'un répertoire ET son contenu:

>chmod -R g+w,o-rx /data/common

### Modification du propriétaire et/ou du groupe propriétaire

>chown <-R> [user]:[group] fichier(dossier)

La commande `chown` permet de modifier l'utilisateur propriétaire et groupe propriétaire 

Modifier l'utilisateur et le groupe propriétaire:

Exemple:
> 
> chown penthium:users /data


Modifier seulement le groupe propriétaire de /data/common ET son contenu

>chown -R :users /data/common


### Gestion du modèle de droit "umask"

L'`umask` est utilisé pour déterminer les droits des fichiers et des répertoires.

La valeur de l'`umask` sera "soustraite" à la valeur des droits maximaux à la création: `0666` pour un fichier, `0777` pour un répertoire.

Sur Debian, l'`umask` par défaut des utilisateurs est `0022`. Il est important que cette valeur reste appliquer à root et aux services dont le UID < 1000.

Pour calculer l'`umask` en droit lecture-écriture-exécution pour l'user et le groupe propriétaire:
- La somme total en octal: 770
- Ensuite je vais soustraire la valeur cible à la valeur maximal: 777
- Le résultat est: 007
- Ou 0007 en prenant compte du premier chiffre représentant les droits spéciaux.

Il est possible pour chaque utilisateur de modifier son `umask` avec la commande du même nom.

>umask [mode]

Afficher le masque courant:

>umask

Modifier le masque courant:

>umask 0007

Pour avoir un `umask` spécifique lors de la connexion, il est possible d'ajouter une entrée avec la commande `umask` dans son fichier de chargement de son shell (le fichier `~/.bashrc` pour le shell `bash`)

### DROIT SPECIAUX UNIX

| Droit | Octal | Fichier | Répertoire
|-------|-------|---------|-----------|
|**SetUID** Symbolique sur colonne user, champ x: s=SetUID + droit x positionné S=Set UID positionné seul | 4--- |Exécution avec les droits du propriétaire du fichier | Non utilisé pour les dossiers
| **SetGID** Symbolique sur colonne group, champ x: s=SetGID + droit x positionné S=SetGID positionné seul | 2--- | Exécution avec les droits du groupe Ex:`/usr/bin/crontab` s'exécute avec les droits du groupe `crontab` | Tout fichier créé dans ce dossier héritera du groupe du dossier parent. Les sous-dossiers créés hériteront quant à eux du droit SGID |
| **Sticky Bit** Symbolique sur colonne other,champ x: t=Sticky Bit + droit x positionné T=Sticky Bit positionné seul | 1--- | Mise en zone de swap. Le but est que le fichier  puisse être stocké en mémoire pour être relancer plus rapidement | Tout fichier créé ne pourra être supprimer que par son propriétaire ou root. Ex `/tmp` |

>chmod -R [ugoa][+ - =][st] fichier ou dossier

## MAINTENANCE D'UN SYSTEME EN PRODUCTION

### JOURNALD AU TRAVERS DE SYSTEMD

Tous les services, programmes, tâches gérées par `systemd` ont leurs comportements remontés dans `journald`.

Le fait d'exécuter la commande `systemctl status [daemon] affiche le statut du service mais aussi les logs de l'application.

### LA COMMANDE JOURNALD

Afficher les logs complet de chaque service:

>journalctl

Le fichier de configuration de `journald` est `/etc/systemd/journald`

Visualiser les logs en temps réel:

>journalctl -f

Avoir des informations sur un service en particulier:

>journalctl -u [service]

Filtrer avec PID:

   journalctl _PID=[n° pid]

Obtenir les logs d'un binaire:

>journalctl /usr/bin/sshd

Voir les logs par niveaux de priorité:

>journalctl -p <level>

Les niveaux de priorité sont du plus critique au plus informatif:
- emerg
- alert
- crit
- err
- warning
- notice
- info
- debug

Il est possible de cumuler les options, par exemple:

>journalctl -f /usr/bin/sshd -p info

### RSYSLOG AU TRAVERS DE JOURNALD

Pour conserver les logs Debian utilise `rsyslog`

`rsyslog` travaille sur des "facilities" et des niveaux de priorités qui déclenchent une action.

Les "facilities" les plus courantes sont:
- ``auth``: utilisée pour des évènements concernant la sécurité ou l'authentification à travers des applications (type SSH)
- ``authpriv``: utilisée pour des messages relatifs au contrôle d'accès
- ``daemon``: utilisée par les différents processus systèmes et d'applications
- ``kern``: utilisée pour les messages concernant le noyau
- ``mail``: utilisée pour les évènements des services mail
- ``user``: facility par défaut quand aucune n'est spécifiée
- ``local0`` à ``local7``: utilisées pour les messages de différents programmes
- ``*``: désigne toutes les facilities
- ``none``: désigne aucune facility

Les niveaux de priorités sont:
- ``emerg``: urgence, système inutilisable
- ``alert``: alerte, intervention immédiate nécessaire
- ``crit``: erreur système critique
- ``err``: erreur de fonctionnement
- ``warning``: avertissement
- ``notice``: évènements normaux devant être signalés
- ``info``: pour information
- ``debug``: message de débogage

Les règles sont configurées dans le fichier:

>/etc/rsyslog.conf

Le "-" devant certains chemin indique que l'enregistrement des logs est asynchrone.

La commande `logger` permet de faire des tests ou de créer des scripts qui intéragissent avec `journald` et `rsyslog`.

Par exemple pour envoyer un message cron de niveau info:

>logger -p cron.info Message de test

### PLANIFICATION DES TACHES

Pour éditer la planification des tâches, on lance la commande:

>crontab -e 

Ce qui nous permet de choisir l'éditeur de texte qu'on souhaite utiliser.

Pour afficher la liste des tâches:

>crontab -l

Le fichier `crontab` est composé de 6 colonnes:
- Minute: 0 à 59
- Heure: 0 à 23
- Jour: 1 à 31
- Mois: 1 à 12
- Jour de la semaine: 0 à 7 (sachant que 0 et 7 représentent dimanche)
- Commande: la commande à exécuter suivant la planification (il est conseillé d'utiliser un script pour des raisons de simplification de suivi des actions)

Il est possible de formater les cinq premières colonnes:
- Avec des listes, en utilisant le caractère ",":
  - Ex: 1,3,5 dans la colonne des jours de la semaine génèrent une tâche tous les lundis, mercredi et vendredis
- Avec des intervalles, en utilisant "-":
  - Ex: 10-20 dans la colonne jours du mois génère une tâche exécutée du 10 au 20
- Avec un joker, en utilisant "*":
  - Ex: * dans la colonne des heures indique toutes les heures
- Mettre un répétiteur, en utilisant "/":
  - Ex: */2 dans la colonne des mois génère une tâche exécutée en janvier, mars, mai, juillet, septembre, novembre

Exemple de configuration:

>0   5   *   *   1   /opt/bin/backup.sh

Cet exemple est une tâche exécutée chaque lundi matin à 5h00 durant toute l'année, quel que soit le mois.

### PLANIFICATION SYSTEME

Cron utilise une table spéciale pour les tâches de planification du système.
Ces tâches sont déclarées dans le fichier `/etc/crontab`

## GESTION DE LA TAILLE DES LOGS

### TAILLE DES LOGS AVEC JOURNALD

Nativement `journald` stocke ses logs dans une base de données volatile dans `/run/log/journal`
Mais il est possible de demander à `journald` de garder les logs de façon durable. Dans le fichier de configuration: `/etc/systemd/journald.conf`, le paramètre ``#Storage=auto`` est commenté donc journald utilise sa par défaut aui est **auto**

Le fait de créer un répertoire `/var/log/journal`rendra la conservation des logs durable. La taille de la base de données peut par contre devenir conséquente sur un système fortement utilisé.

Par défaut, `journald` utilisera un maximum de 10% du système de fichier hébergeant `/var/log/journald`

Il est possible de définir la taille maximum utilisée sur le système de fichier de la base de données avec le paramètre `SystemMaxUse=`. De plus, il est possible de dire que la base de données sera subdivisée en plusieurs fichiers de taille fixe avec le paramètre `SystemMaxFileSize=`.

Bien évidemment si la décision est prise de garder les logs de journald de façon définitive, il sera peut être intéressant de stopper `rsyslog` afin d'éviter les doublons d'informations.

>systemctl disable rsyslog

### TAILLE DES LOGS AVEC LOGROTATE

`logrotate` est un programme exécuté par une tâche cron système tous les jours présente dans `/etc/cron.daily/logrotate`

Le fichier de configuration principal `/etc/logrotate.conf` définit des valeurs de comportement par défaut.

## OUTILS D'ANALYSE DU SYSTEME

Connaître la version du système:

>cat /etc/debian_version

Connaître la version du noyau Linux actif et son architecture

>uname -a

Connaître le type de CPU

>lscpu

Lister les informations des matériels PCI:

>lspci

Lister les périphériques USB:

>lsusb

Lister les informations sur stockage et système de fichiers

>fdisk; pvs,vgs,lvs ; lsblk,blkid,findmnt,df

Lister les informations sur répertoire et fichiers:
- La commande `du` permet de prendre des informations sur la taille utilise d'un répertoire.

>>du -sh /root
- La commande `ls` permet de prendre des informations sur les fichiers

>>ls -lh fichier
- La commande `file` permet de connaître la nature d'un fichier
  
>>file /bin/path

- La commande `lsof` permet de connaître l'activité des fichiers ouverts dans un répertoire donné

>>lsof /root

## PERFORMANCES ET PROCESSUS

Information en temps réel avec `top` (native)
- Touche L : Coloration syntaxique
- Touche M : Passer d'un affichage à l'autre
- Touche H : Aide Interne
- Touche Q : Quitter

Information en temps réel avec `htop` (à installer)

Information en temps réel avec `glances` (à installer)
  - https://github.com/nicolargo/glances 

Liste des processus avec `ps`

>ps -ef

Informations sur la ram avec `free`

>free -h

