## Challenge — Installer Ansible depuis les dépôts officiels sur Ubuntu

#### Démarrer la VM Ubuntu
```bash
vagrant up ubuntu
```

#### Se connecter à la VM
```bash
vagrant ssh ubuntu
```

#### Mettre à jour la base des paquets
```bash
sudo apt update
```

#### Rechercher le paquet Ansible
```bash
apt-cache search --names-only ansible
```
Affiche les paquets dont le nom contient "ansible" pour vérifier sa disponibilité dans les dépôts officiels.

#### Installer Ansible
```bash
sudo apt install -y ansible
```

#### Vérifier l'installation
```bash
ansible --version
```

#### Quitter et supprimer la VM
```bash
exit
vagrant destroy -f ubuntu
```

# Challenge — Installer Ansible via le dépôt PPA officiel

#### Relancer une nouvelle VM Ubuntu
```bash
vagrant up ubuntu
```

#### S'y connecter
```bash
vagrant ssh ubuntu
```

#### Mettre à jour les paquets
```bash
sudo apt update
```

#### Ajouter le dépôt PPA Ansible
```bash
sudo apt-add-repository ppa:ansible/ansible
```
Ajoute le dépôt personnel maintenu par l'équipe officielle Ansible sur Launchpad.

#### Rafraîchir la base des paquets après ajout du PPA
```bash
sudo apt update
```

#### Installer Ansible depuis le PPA
```bash
sudo apt install -y ansible
```

#### Vérifier la version installée
```bash
ansible --version
```

#### Quitter et supprimer la VM
```bash
exit
vagrant destroy -f ubuntu
```

## Challenge — Installer Ansible sur Rocky Linux via pip + virtualenv

#### Démarrer la VM Rocky Linux
```bash
vagrant up rocky
```

#### Se connecter à la VM
```bash
vagrant ssh rocky
```

#### Mettre à jour les paquets
```bash
sudo dnf update -y
```

#### Installer Python, pip et virtualenv
```bash
sudo dnf install -y python3 python3-pip python3-virtualenv
```

#### Créer un virtualenv pour Ansible
```bash
python3 -m venv ~/.venv/ansible
```
Crée un environnement virtuel isolé nommé `ansible` dans `~/.venv`.

#### Activer l'environnement virtuel
```bash
source ~/.venv/ansible/bin/activate
```

#### Mettre à jour pip
```bash
pip install --upgrade pip
```

#### Installer Ansible via pip
```bash
pip install ansible
```

#### Vérifier la version d'Ansible
```bash
ansible --version
```

#### Quitter l'environnement virtuel
```bash
deactivate
```

#### Quitter et supprimer la VM
```bash
exit
vagrant destroy -f rocky
```
