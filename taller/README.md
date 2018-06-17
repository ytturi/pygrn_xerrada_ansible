# Taller - Desplegament i actualització de contingut estàtic

## Objectius

- Treballar amb Python
- Desplegar utilitzant Ansible
- Actualitzar "sense por" utilitzant Ansible
- Desplegar i Actualitzar "massivament" utilitzant Ansible

## Requeriments

### Màquines destí

- Durant el taller sería convenient disposar de màquines virtuals per realitzar-hi el desplegament.
- També podeu utilitzar Dockers a inicialitzats amb Bash i amb accés a la xarxa.

El Repositori a clonar és públic, pel que el podreu clonar sense problemes tant mitjançant HTTPS com amb SSH.

```
git clone git@github.com:ytturi/pygrn_xerrada_ansible.git
git clone https://github.com/ytturi/pygrn_xerrada_ansible.git
```

!!! Warning
    Recordeu que si cloneu per SSH, haureu de generar abans les claus SSL.

### Configuració local

Per tal d'utilitzar ansible, necessitem tenir python instalat. Com sempre, és recomanable instalar-lo en un virtualenv.

```bash
mkvirtualenv ansible
pip install ansible
```

## Documentació

### Contingut utilitzat per aquesta documentació

- [MkDocs](https://www.mkdocs.org), tractat en la [xerrada sobre contingut estàtic](https://github.com/pygrn/xerrades/tree/master/xerrades/2018/20180221)
    - Extensió [Admonition](https://python-markdown.github.io/extensions/admonition/), una extensió que ens permet utilitzar "Notes". Originaria de rST, realitza un recuadre de contingut amb un títol.
    - Extensió [Details](https://facelessuser.github.io/pymdown-extensions/extensions/details/), la trobem dins del paquet PyMdown. Ens permet afegir notes com Admonition, però desplegables.
    - Tema [Material](https://squidfunk.github.io/mkdocs-material/), un tema per la documentació MKDOCS i ReadTheDocs, que millora gràficament aquesta pàgina
- [Virtualenv](https://virtualenv.pypa.io/en/stable/), aquesta llibreria que segurament ja coneixeu i ens permet no instalar coses directament al sistema.

### Exemple de fitxer YML per Ansible

### Possibles mòduls de Ansible que us vindràn bé

- [APT](https://docs.ansible.com/ansible/latest/modules/apt_module.html), ens permet realitzar les diferents funcionalitats del APT de Debian.
- [GIT](https://docs.ansible.com/ansible/latest/modules/git_module.html), ens permet fer els desplegaments i actualitzacions corresponents de GIT.
- [PIP](https://docs.ansible.com/ansible/2.4/pip_module.html), ens permet tractar amb llibreries i Virtualenvs
- [SYSTEMD](https://docs.ansible.com/ansible/2.5/modules/systemd_module.html), ens permet gestionar els serveis de la màquina
- Tractament de fitxers:
    - [FILE](https://docs.ansible.com/ansible/latest/modules/file_module.html), actualitzar els atributs dels fitxers i/o realitzar links
    - [COPY](https://docs.ansible.com/ansible/latest/modules/copy_module.html), copiar un fitxer des d'on despleguem a les màquines destí
    - [TEMPLATE](https://docs.ansible.com/ansible/latest/modules/template_module.html), realitzar un fitxer a partir del valor de diferents variables
    - [LineInFile](https://docs.ansible.com/ansible/latest/modules/lineinfile_module.html), assegurar-nos que hi ha (o no) una línia en el fitxer
    - [REPLACE](https://docs.ansible.com/ansible/latest/modules/replace_module.html), reemplaça totes les instàncies de les línies indicades pel valor indicat

## Desplegament

### Tractament de peticions HTTP/S

Posarem un Nginx amb la configuració facilitada en el repositori de la xerrada:

> pygrn_xerrada_ansible/taller/docs_nginx.conf


Per tal de desplegar-ho, hem de pensar les passes que seguiriem en local i adaptar-ho a Ansible.

??? Note "Passes que seguiriem en local"
    1. Instalar Nginx amb `apt-get install nginx` 
    2. (**opcional**) Eliminar la configuració per defecte
    3. Afegir la configuració nova a "_sites-available_"
    4. Realitzar un link simbolic a "_sites-enabled_"

    ??? Note "Codi amb bash"
            sudo apt-get install nginx
            sudo rm /etc/nginx/sites-enabled/default
            sudo cp /.../pygrn_xerrada_ansible/taller/docs_nginx.conf /etc/nginx/sites-available/docs
            sudo ln -s /etc/nginx/sites-available/docs /etc/nginx/sites-enabled/docs 
        
        !!! Warning
            Com que utilitzem fitxers protegits cal utilitzar **sudo**!

!!! Info
    No cal que compilem, utilitzem el mateix que podria venir amb un debian amb els repositoris de APT.

!!! Info
    Podem utilitzar diverses configuracions per pujar el fitxer. 

### Clonar el repositori

Aquesta documentació es troba en el repositori de github de la xerrada: [github:ytturi/pygrn_xerrada_ansible](https://github.com/ytturi/pygrn_xerrada_ansible).

Allà hi tenim el directori "`taller/documentacio_estatica`" on trobarem:

- El fitxer de configuració de mkdocs ("mkdocs.yml"),
- Els requeriments de pyhton ("requirements.txt") 
- La documentació en format Markdown en el directori "docs".

??? Note "Passes que realitzariem en local"
    1. Anar al directori de projectes
    2. Mirar si existeix el repositori
        1. Si no hi és el clonem amb `git clone https://github.com/ytturi/pygrn_xerrada_ansible.git`
        2. Si hi és, l'actualitzem amb `git pull`

