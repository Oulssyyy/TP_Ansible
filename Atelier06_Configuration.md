
## Challenge — Atelier 6 : Configuration de base

#### Modifier `/etc/hosts` pour la résolution des noms
Éditer le fichier hosts sur le Control Host :

```bash
sudo nano /etc/hosts
```

Ajouter ces lignes à la fin du fichier :

```
192.168.56.20 target01
192.168.56.30 target02
192.168.56.40 target03
```

Cela permet au Control Host de joindre les Target Hosts par leur nom (sans utiliser l'adresse IP).

#### Configurer l’authentification SSH sans mot de passe

Générer une clé SSH (si elle n'existe pas encore) :

```bash
ssh-keygen -t ed25519
```

Copier la clé publique vers chaque Target Host :

```bash
ssh-copy-id vagrant@target01
ssh-copy-id vagrant@target02
ssh-copy-id vagrant@target03
```

Vérifier la connexion SSH :

```bash
ssh vagrant@target01 hostname
ssh vagrant@target02 hostname
ssh vagrant@target03 hostname
```

#### Installer Ansible

```bash
sudo apt update
sudo apt install -y ansible
```

#### Tester Ansible rapidement sans configuration

```bash
ansible all -i target01,target02,target03 -m ping
```

## Création du projet Ansible

#### Créer le répertoire du projet

```bash
mkdir -pv ~/monprojet
cd ~/monprojet
```

#### Créer un fichier de configuration vide

```bash
touch ansible.cfg
```

Vérifier que ce fichier est bien pris en compte :

```bash
ansible --version | head -n 2
```

Résultat :

```
config file = /home/vagrant/monprojet/ansible.cfg
```

#### Spécifier l’inventaire et le journal dans `ansible.cfg`

Éditer le fichier :

```bash
nano ansible.cfg
```

Ajouter le contenu suivant :

```
[defaults]
inventory = ./hosts
log_path = ~/journal/ansible.log
```

- `inventory` : indique le fichier contenant la liste des hôtes gérés.
- `log_path` : définit où Ansible enregistre les logs de ses actions.

#### Créer le répertoire de logs

```bash
mkdir -pv ~/journal
```

#### Créer le fichier d’inventaire (hosts)

```bash
nano hosts
```

Ajouter le contenu suivant :

```
[testlab]
target01
target02
target03

[testlab:vars]
ansible_python_interpreter=/usr/bin/python3
ansible_user=vagrant
```

#### Tester la journalisation

```bash
ansible all -m ping
cat ~/journal/ansible.log
```

#### Tester un ping du groupe `[all]`

```bash
ansible all -m ping
```

#### Configurer l’élévation des privilèges (sudo)

Modifier le fichier `hosts` pour ajouter `ansible_become=yes` :

```
[testlab]
target01
target02
target03

[testlab:vars]
ansible_python_interpreter=/usr/bin/python3
ansible_user=vagrant
ansible_become=yes
```

#### Vérifier l’élévation des privilèges

```bash
ansible all -a "head -n 1 /etc/shadow"
```