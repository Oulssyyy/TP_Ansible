
## Challenge — Atelier 10 : Un serveur web simple

#### Crée les 3 playbooks

```bash
cd playbooks/
```

#### Playbook 1 — Debian

```yaml
---  # apache-debian.yml

- hosts: debian
	tasks:
		- name: Update package cache
			apt:
				update_cache: true
				cache_valid_time: 3600

		- name: Install Apache
			apt:
				name: apache2
				state: present

		- name: Start & enable Apache service
			service:
				name: apache2
				state: started
				enabled: true

		- name: Install custom web page
			copy:
				dest: /var/www/html/index.html
				mode: 0644
				content: |
					<!doctype html>
					<html>
						<head>
							<meta charset="utf-8">
							<title>Debian Apache</title>
						</head>
						<body>
							<h1>Apache web server running on Debian Linux</h1>
						</body>
					</html>
```

#### Playbook 2 — Rocky Linux

```yaml
---  # apache-rocky.yml

- hosts: rocky
	tasks:
		- name: Install Apache package
			dnf:
				name: httpd
				state: present

		- name: Start & enable Apache service
			service:
				name: httpd
				state: started
				enabled: true

		- name: Install custom web page
			copy:
				dest: /var/www/html/index.html
				mode: 0644
				content: |
					<!doctype html>
					<html>
						<head>
							<meta charset="utf-8">
							<title>Rocky Apache</title>
						</head>
						<body>
							<h1>Apache web server running on Rocky Linux</h1>
						</body>
					</html>
```

#### Playbook 3 — SUSE Linux

```yaml
---  # apache-suse.yml

- hosts: suse
	tasks:
		- name: Install Apache package
			zypper:
				name: apache2
				state: present

		- name: Start & enable Apache service
			service:
				name: apache2
				state: started
				enabled: true

		- name: Install custom web page
			copy:
				dest: /srv/www/htdocs/index.html
				mode: 0644
				content: |
					<!doctype html>
					<html>
						<head>
							<meta charset="utf-8">
							<title>SUSE Apache</title>
						</head>
						<body>
							<h1>Apache web server running on SUSE Linux</h1>
						</body>
					</html>
```

#### Vérifier la syntaxe de chaque playbook

```bash
yamllint apache-debian.yml
yamllint apache-rocky.yml
yamllint apache-suse.yml
```

#### Exécuter les playbooks

```bash
ansible-playbook apache-debian.yml
ansible-playbook apache-rocky.yml
ansible-playbook apache-suse.yml
```

#### Vérifier le résultat

```bash
curl debian
curl rocky
curl suse
```

Par page HTML servie par chaque hôte on a :

- Apache web server running on Debian Linux
- Apache web server running on Rocky Linux
- Apache web server running on SUSE Linux
