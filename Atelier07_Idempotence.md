
## Challenge — Atelier 7 : Idempotence

#### Installer tree, git, nmap :

```bash
ansible all -m package -a "name=tree state=present" -b
ansible all -m package -a "name=git state=present" -b
ansible all -m package -a "name=nmap state=present" -b
```

#### Désinstaller les mêmes paquets :

```bash
ansible all -m package -a "name=tree state=absent" -b
ansible all -m package -a "name=git state=absent" -b
ansible all -m package -a "name=nmap state=absent" -b
```

#### Copier `/etc/fstab` du Control Host vers chaque Target sous `/tmp/test3.txt` :

```bash
ansible all -m copy -a "src=/etc/fstab dest=/tmp/test3.txt mode=0644 owner=root group=root" -b
```

#### Supprimer `/tmp/test3.txt` sur les cibles (module `file` state=absent) :

```bash
ansible all -m file -a "path=/tmp/test3.txt state=absent" -b
```

#### Afficher l’espace utilisé par la partition principale (commande informative) :

```bash
ansible all -m command -a "df -h /"
```

#### Remarque de ce challenge :

Pour toutes les opérations de configuration (install, uninstall, copy, delete) on a comme résultat :

- 1ère exécution → changed: true (Ansible a effectué une modification).
- 2ème exécution → changed: false (Ansible détecte que l’état désiré est déjà atteint) — idempotence
