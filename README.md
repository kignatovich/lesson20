# lesson20



## Домашнее задание 20
- Проделать то что делали с playbook на уроĸе, можно мой взять можно любой свой.
Не все отсупы в методичĸе в yaml файлах учтены, в своей работе исправляйте это.
- Написать ĸаĸ минимум 3 разные роли
## Подготовка виртуального окружения (env)
```shell
front@front:~/lesson20$ virtualenv env
front@front:~/lesson20$ source env/bin/activate
front@front:~/lesson20$ pip install ansible
front@front:~/lesson20$ pip freeze > requirements.txt
```

### Проверка работы ansible (для изначального файла inventory.ini содержащего только 2 сервера redhat-servers и debian-servers)
```shell
(env) front@front:~/lesson20$ ansible all -i inventory.ini -m ping
Enter passphrase for key '/home/front/.ssh/id_rsa': 

192.168.0.139 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    }, 
    "changed": false, 
    "ping": "pong"
}
192.168.0.141 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    }, 
    "changed": false, 
    "ping": "pong"
}
```
### запуск playbook
```shell
ansible-playbook -i inventory.ini playbookname.yml -K
```
- Ключ "К" - из за того, что я использую не root юзера, а пользователя который требует повышения прав и ввода пароля. Так же можно ansible_sudo_pass = 1

 Grafana, prometeus, update_certs были получены командами 

```shell
cd .roles
ansible-galaxy init Prometheus
ansible-galaxy init Grafana
ansible-galaxy init Update_Certs
```
### roles
![roles](https://i.ibb.co/kHb3KFx/01.jpg)

### grafana
![grafana](https://i.ibb.co/z2BDpbQ/02.jpg)

## prometheus
![prometheus](https://i.ibb.co/tzHfX3D/03.jpg)

### Update_Certs
![Update_Certs](https://i.ibb.co/sRnqbst/04.jpg)


### Вывод команды tree

```shell
./roles/
├── epel
│   └── tasks
│       └── main.yml
├── Grafana
│   ├── defaults
│   │   └── main.yml
│   ├── files
│   ├── handlers
│   │   └── main.yml
│   ├── meta
│   │   └── main.yml
│   ├── README.md
│   ├── tasks
│   │   └── main.yml
│   ├── templates
│   ├── tests
│   │   ├── inventory
│   │   └── test.yml
│   └── vars
│       └── main.yml
├── nginx
│   ├── handlers
│   │   └── main.yml
│   ├── tasks
│   │   └── main.yml
│   ├── templates
│   │   ├── nginx.conf.tpl
│   │   └── nginx_vhosts.conf
│   └── vars
│       └── main.yml
├── Prometheus
│   ├── defaults
│   │   └── main.yml
│   ├── files
│   ├── handlers
│   │   └── main.yml
│   ├── meta
│   │   └── main.yml
│   ├── README.md
│   ├── tasks
│   │   ├── install_alertmanager.yml
│   │   ├── install_prometheus.yml
│   │   ├── main.yml
│   │   └── prepare.yml
│   ├── templates
│   │   ├── alertmanager.service
│   │   └── prometheus.service
│   ├── tests
│   │   ├── inventory
│   │   └── test.yml
│   └── vars
│       └── main.yml
└── Update_Certs
    ├── defaults
    │   └── main.yml
    ├── files
    ├── handlers
    │   └── main.yml
    ├── meta
    │   └── main.yml
    ├── README.md
    ├── tasks
    │   └── main.yml
    ├── templates
    ├── tests
    │   ├── inventory
    │   └── test.yml
    └── vars
        └── main.yml

34 directories, 35 files
```

### Список источников
- [Источник1](https://www.dmosk.ru/miniinstruktions.php?mini=ansible-roles-example#prometheus)
- [Источник2](https://www.dmosk.ru/instruktions.php?object=ansible-nginx-install)