## Atelier 04 — Authentification

#### Éditer le fichier `/etc/hosts`

```bash
sudo nano /etc/hosts
```

Ajouter les noms des target hosts

```bash
192.168.56.10  control
192.168.56.20  target01
192.168.56.30  target02
192.168.56.40  target03
```

#### Tester la connectivité réseau basique (ping ICMP)

```bash
for HOST in target01 target02 target03; do ping -c 1 -q $HOST; done
```

#### Générer une clé SSH sur le Control Host

```bash
ssh-keygen
```

#### Distribuer la clé publique vers chaque Target Host

```bash
ssh-copy-id vagrant@target01
ssh-copy-id vagrant@target02
ssh-copy-id vagrant@target03
```
Ces commandes vont copier la clé publique du Control Host dans le fichier `~/.ssh/authorized_keys` des cibles.

### Tester un ping Ansible avec l’inventaire ad hoc

```bash
ansible all -i target01,target02,target03 -m ping
```

Chaque hôte nous réponds : 
```bash 
"ping": "pong"
```

