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

### Configuració local

Per tal d'utilitzar ansible, necessitem tenir python instalat. Com sempre, és recomanable instalar-lo en un virtualenv.

`pip install ansible`

## Documentació

### Contingut utilitzat per aquesta documentació

- [MkDocs](https://www.mkdocs.org), tractat en la [xerrada sobre contingut estàtic](https://github.com/pygrn/xerrades/tree/master/xerrades/2018/20180221)
    - Extensió [Admonition](https://python-markdown.github.io/extensions/admonition/), una extensió que ens permet utilitzar "Notes". Originaria de rST, realitza un recuadre de contingut amb un títol.
    - Tema [Material](https://squidfunk.github.io/mkdocs-material/), un tema per la documentació MKDOCS i ReadTheDocs, que millora gràficament aquesta pàgina
- [Virtualenv](https://virtualenv.pypa.io/en/stable/), aquesta llibreria que segurament ja coneixeu i ens permet no instalar coses directament al sistema.

### Exemple de fitxer YML per Ansible

### Possibles mòduls de Ansible que us vindràn bé

- [APT](https://docs.ansible.com/ansible/latest/modules/apt_module.html), ens permet realitzar les diferents funcionalitats del APT de Debian.
- [GIT](https://docs.ansible.com/ansible/latest/modules/git_module.html), ens permet fer els desplegaments i actualitzacions corresponents de GIT.
- [PIP](https://docs.ansible.com/ansible/2.4/pip_module.html), ens permet tractar amb llibreries i Virtualenvs
- Tractament de fitxers:
    - [FILE](https://docs.ansible.com/ansible/latest/modules/file_module.html), actualitzar els atributs dels fitxers i/o realitzar links
    - [COPY](https://docs.ansible.com/ansible/latest/modules/copy_module.html), copiar un fitxer des d'on despleguem a les màquines destí
    - [TEMPLATE](https://docs.ansible.com/ansible/latest/modules/template_module.html), realitzar un fitxer a partir del valor de diferents variables
    - [LineInFile](https://docs.ansible.com/ansible/latest/modules/lineinfile_module.html), assegurar-nos que hi ha (o no) una línia en el fitxer
    - [REPLACE](https://docs.ansible.com/ansible/latest/modules/replace_module.html), reemplaça totes les instàncies de les línies indicades pel valor indicat

## Desplegament


