# Kode standarder for Ansible
Denne kodestandard skal fungere som et grundlag og kan tilpasses efter behov.
Det er vigtigt at opretholde konsistens på tværs af projekter og samarbejde for at sikre en klar og læsbar kode.

## Formatering af Kode
Brug 2 mellemrum for indrykning.  
Hold en tomt linjeskift mellem forskellige sektioner for bedre læsbarhed.  
Brug funktioners fulde navn, så man kan se hvad modul det kommer fra.

```yaml
# Good
- name: Load variables from YAML file
  ansible.builtin.include_vars:
  ...

- name: Update variables with web results
  ansible.builtin.set_fact:
  ...

# Bad
- name: Load variables from YAML file
  include_vars:
  ...

- name: Update variables with web results
  set_fact:
  ...

```

## Navngivning af Tasks
Anvend klare, beskrivende navne til tasks.  
Undgå brug af specialtegn i navngivningen.

```yaml


- name: Install Apache
  ...

- name: Configure Firewall
  ...

```

## Variable
Brug snake_case til variabelnavne.  
Brug præcise og deskriptive navne.

```yaml

apache_version: 2.4
web_servers:
  - server1
  - server2

```

### Brug af YAML lists og Dictionaries
Brug lister for at repræsentere en række værdier.  
Brug dictionaries til at repræsentere nøgle-værdi-par.  
Hold variable i separate filer og indlæs dem, for at reducerer kompleksitet og øge genanveldelse.

```yaml

websites:
  - name: example
    domain: example.com
  - name: test
    domain: test.com

```


## Quotes forskellig brug af ' og "
Brug enkelt citater (' ') for strengværdier.  
Brug dobbelt citater (" ") for variabelværdier.

```yaml

message: "Hello, {{ user_name }}!"
path: '/var/www/html'

```

## Playbook struktur
Opdel playbooks i sektioner: vars, tasks, handlers, roles, osv.

```yaml

---
- name: Web Server Configuration
  hosts: web_servers
  become: true
  vars:
    apache_version: 2.4

  tasks:
    - name: Install Apache
      ...
      notify:
      - Restart Apache

  handlers:
    - name: Restart Apache
      ...

```

## Brug af kommentar
Tilføj kommentarer for at forklare komplekse eller vigtige dele af koden.

```yaml

# Installerer Apache-webserver
- name: Install Apache
  ...

# Genstarter Apache, hvis konfigurationen ændres
- name: Restart Apache
  ...

```

## Brug af Tags
Anvend tags til at gruppere og køre specifikke dele af playbooks.

```yaml

- name: Install and configure web server
  hosts: web_servers
  become: true
  tags: web
  ...

```

Dette er et grundlæggende udkast, og du kan tilpasse det efter behov og organisationens præferencer. Det er altid en god idé at konsultere Ansibles officielle dokumentation og tage hensyn til teamets egne erfaringer og præferencer.
