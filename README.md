# Домашнее задание к занятию "08.05 Тестирование Roles"

----------------------------------------------------------


----------------------------------------------------------
## Подготовка к выполнению

#### 1. Установите molecule: `pip3 install "molecule==3.4.0"`
#### 2. Соберите локальный образ на основе [Dockerfile](Dockerfile)
```shell
$ docker build -t redhat_ansible:latest .
...
Step 14/14 : RUN rm -rf Python-*
 ---> Running in e561dcab2a1b
Removing intermediate container e561dcab2a1b
 ---> 2e0f274b5164
Successfully built 2e0f274b5164
Successfully tagged redhat_ansible:latest

$ docker images
REPOSITORY                        TAG       IMAGE ID       CREATED          SIZE
redhat_ansible                    latest    2e0f274b5164   48 seconds ago   2.48GB
```
* В дальнейшем я отказалась от использования контейнера с образом RHEL, т.к. возникали сложности с настройками, падения "иксов".  
* Работа по этой домашке, без учета личных проблем, заняла огромное количество времени. Мне пришлось переустанавливать 5 раз ОС =) Первое тестирование проводилось на `ubuntu 20.04`, и систему я дестабилизировала. Искала другие варианты, с которыми можно было бы работать успешно (семейство Linux). В итоге пришла к тому, что лучше развернуть ВМ на той же, знакомой `ubuntu 20.04`. Поэтому работать я буду с `Virtual Box`. 
* Моя система - `ubuntu 20.04` на Virtual Box, работать буду с ней и с `docker`.
* Весь необходимый ансанбль у `ansible` я устанавливала по следующим версиям, т.к. версии из задания не приносили никаких плодов:

```shell
$ molecule --version
molecule 3.5.3.dev61 using python 3.8 
    ansible:2.12.1
    delegated:3.5.3.dev61 from molecule
    docker:1.1.0 from molecule_docker requiring collections: community.docker>=1.9.1
    podman:1.0.1 from molecule_podman requiring collections: containers.podman>=1.7.0 ansible.posix>=1.3.0
```
##### P.S. У меня было полтора месяца на борьбу с `ansible`, некоторые изменения в файлах объяснить уже не смогу. 

----------------------------------------------------------
## Основная часть

----------------------------------------------------------
### Molecule

#### 1. Запустите molecule test внутри корневой директории elasticsearch-role, посмотрите на вывод команды.

* Ошибки были, в основном, следующие:
```shell
TASK [elasticsearch-role : Configure Elasticsearch Deb] ************************
skipping: [centos7]
changed: [ubuntu]

RUNNING HANDLER [elasticsearch-role : restart Elasticsearch] *******************
fatal: [centos7]: FAILED! => {"changed": false, "msg": "Service is in unknown state", "status": {}}
changed: [ubuntu]
```
```shell
TASK [elasticsearch-role : Configure Elasticsearch Deb] ************************
skipping: [centos7]
changed: [ubuntu]

RUNNING HANDLER [elasticsearch-role : restart Elasticsearch] *******************
fatal: [centos7]: FAILED! => {"changed": false, "msg": "Unable to start service elasticsearch: Job for elasticsearch.service failed because a fatal signal was delivered to the control process. See \"systemctl status elasticsearch.service\" and \"journalctl -xe\" for details.\n"}
changed: [ubuntu]
```
* А также ошибка с неправильно сформированным `meta`-файлом. Он был скорректирован (добавлен `namespace`):
```yaml
galaxy_info:
  author: Alexey Metlyakov
  description: your role description
  company: netology
  role_name: elasticsearch_role
  namespace: elk
```

* Изменились и следующие файлы:
* `molecule.yml`
```yaml
---
dependency:
  name: galaxy
driver:
  name: docker
lint: |
  ansible-lint .
  yamllint .
platforms:
  - name: instance-1
    image: docker.io/pycontribs/centos:7
    command: /sbin/init
    volumes:
      - /sys/fs/cgroup:/sys/fs/cgroup:ro
    privileged: True
    published_ports:
      - 0.0.0.0:5003:5003/udp
      - 0.0.0.0:5003:5003/tcp
    pre_build_image: true
  - name: instance-2
    image: docker.io/pycontribs/ubuntu:latest
    privileged: True
    published_ports:
      - 0.0.0.0:5004:5004/udp
      - 0.0.0.0:5004:5004/tcp
    environment:
      - ES_JAVA_OPTS: "-Xms256m -Xmx256m"
      - ES_MIN_MEM: "256m"
      - ES_MAX_MEM: "1g"
      - discovery.type: "single-node"
    pre_build_image: true
provisioner:
  name: ansible
  log: true
  options:
    vvv: true
    diff: true
verifier:
  name: ansible
```
* `tasks/install_apt.yml`:
```yaml
---
- name: Update repositories cache and install "python" package
  apt:
    update_cache: yes
- name: Install Java using Ansible
  apt:
    name: openjdk-8-jdk
    state: present
- name: Install Elasticsearch
  apt:
    deb: "/tmp/elasticsearch-{{ elasticsearch_version }}-amd64.deb"
    state: present
  notify: restart Elasticsearch Deb
```
* `tasks/install_yum.yml`:
```yaml
---
- name: Update APT package manager repositories cache
  become: true
  yum:
    update_cache: yes
- name: Install Elasticsearch
  yum:
    name: "/tmp/elasticsearch-{{ elasticsearch_version }}-x86_64.rpm"
    state: present
  notify: restart Elasticsearch
```
* `tasks/configure.yml`:
```yaml
---
- name: Configure Elasticsearch
  become: true
  template:
    src: elasticsearch.yml.j2
    mode: 0644
    dest: /etc/elasticsearch/elasticsearch.yml
  notify: restart Elasticsearch
  when: ansible_facts.pkg_mgr == "yum"
- name: Configure Elasticsearch
  template:
    src: elasticsearch.yml.j2
    mode: 0644
    dest: /etc/elasticsearch/elasticsearch.yml
  notify: restart Elasticsearch Deb
  when: ansible_facts.pkg_mgr == "apt"
```
* `handlers/main.yml`:
```yaml
---
- name: restart Elasticsearch
  become: true
  service:
    name: elasticsearch
    state: restarted
  when: ansible_facts.pkg_mgr == "yum"
- name: restart Elasticsearch Deb
  service:
    name: elasticsearch
    state: restarted
  when: ansible_facts.pkg_mgr == "apt"
```
* `templates/elasticsearch.yml.j2`:
```yaml
path.data: /var/lib/elasticsearch
path.logs: /var/log/elasticsearch
network.host: 0.0.0.0
discovery.seed_hosts: ["{{ ansible_facts['default_ipv4']['address'] | default('0.0.0.0') }}"]
node.name: node-a
cluster.initial_master_nodes: 
   - node-a
http.cors.enabled: true
http.cors.allow-origin: "*"
http.cors.allow-headers: Authorization
xpack.security.enabled: true
xpack.security.transport.ssl.enabled: true
```

* Лог тестирования `elasticsearch-role` вынесла в отдельный [файл](logs/elasticsearch_test_01.md)
* Лог запуска с `molecule converge` также в отдельном [файле](logs/elasticsearch_converge_01.md)

```shell
$ docker ps
CONTAINER ID   IMAGE                      COMMAND                  CREATED          STATUS          PORTS                                            NAMES
077146124aec   pycontribs/ubuntu:latest   "bash -c 'while true…"   1 minutes ago   Up 1 minutes   0.0.0.0:5004->5004/tcp, 0.0.0.0:5004->5004/udp   instance-2
e90ff25cc618   pycontribs/centos:7        "/sbin/init"             1 minutes ago   Up 1 minutes   0.0.0.0:5003->5003/tcp, 0.0.0.0:5003->5003/udp   instance-1
```
* Проверка статуса сервиса в `centos`:
```shell
$ docker exec -ti instance-2 /bin/bash
root@instance-2:/# service elasticsearch status
 * elasticsearch is running
```

* Проверка статуса сервиса в `ubuntu`:
```shell
$ docker exec -ti instance-2 /bin/bash
root@instance-2:/# service elasticsearch status
 * elasticsearch is running
```
----------------------------------------------------------
#### 2. Перейдите в каталог с ролью `kibana-role` и создайте сценарий тестирования по умолчанию при помощи `molecule init scenario --driver-name docker`.

* Учитывая, что работаю с `podman`, создавать сценарий буду с `--driver-name podman`
```shell
$ molecule init scenario --driver-name podman
INFO     Initializing new scenario default...
INFO     Initialized scenario in /home/lerekler/Learning/gitProjects/ansible_test_roles/playbook/roles/kibana-role/molecule/default successfully.
```

#### 3. Добавьте несколько разных дистрибутивов (centos:8, ubuntu:latest) для инстансов и протестируйте роль, исправьте найденные ошибки, если они есть.

* `molecule.yml`:
```yaml
---
dependency:
  name: galaxy
driver:
  name: podman
  managed: false
  login_cmd_template: sleep 5000000
lint: |
  ansible-lint .
  yamllint .
platforms:
  - name: instance-3
    image: docker.io/pycontribs/centos:7
    command: /sbin/init && sleep 5000000
    privileged: True
    published_ports:
      - 0.0.0.0:5005:5005/udp
      - 0.0.0.0:5005:5005/tcp
    pre_build_image: true
  - name: instance-4
    image: docker.io/pycontribs/ubuntu:latest
    command: sleep 5000000
    published_ports:
      - 0.0.0.0:5004:5004/udp
      - 0.0.0.0:5004:5004/tcp
    pre_build_image: true
    provisioner:
provisioner:
  name: ansible
verifier:
  name: ansible
```
* `install_yum.yml`:
```yaml
---
- name: Update cache
  become: true
  yum:
    update_cache: yes
- name: Install Kibana
  become: true
  yum:
    name: "/tmp/kibana-{{ kibana_version }}-x86_64.rpm"
    state: present
  notify: restart Kibana Centos
```
* `install_apt.yml`:
```yaml
---
- name: Update repositories cache
  apt:
    update_cache: yes
- name: Install Kibana
  apt:
    deb: "/tmp/kibana-{{ kibana_version }}-amd64.deb"
    state: present
  notify: restart Kibana Deb
```
* `configure.yml`:
```yaml
---
- name: Configure Kibana
  become: true
  template:
    src: kibana.yml.j2
    dest: /etc/kibana/kibana.yml
    mode: 0644
  notify: restart Kibana Centos
  when: ansible_facts.pkg_mgr == "yum"
- name: Configure Kibana
  template:
    src: kibana.yml.j2
    dest: /etc/kibana/kibana.yml
    mode: 0644
  notify: restart Kibana Deb
  when: ansible_facts.pkg_mgr == "apt"
```
* `handlers/main.yml`:
```yaml
---
- name: restart Kibana Centos
  become: true
  service:
    name: kibana
    state: restarted
  when: ansible_facts.pkg_mgr == "yum"
- name: restart Kibana Deb
  service:
    name: kibana
    state: restarted
  when: ansible_facts.pkg_mgr == "apt"
```
* [Лог](logs/kibana_test_01.md) тестирования
* [`molecule converge`](logs/kibana_converge_01.md)


#### 4. Добавьте несколько assert'ов в verify.yml файл, для проверки работоспособности kibana-role (проверка, что web отвечает, проверка логов, etc). Запустите тестирование роли повторно и проверьте, что оно прошло успешно.