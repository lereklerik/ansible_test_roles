```shell
netology@netology:~/Projects/ansible_test_roles/playbook/roles/elasticsearch-role$ molecule test
INFO     default scenario test matrix: dependency, lint, cleanup, destroy, syntax, create, prepare, converge, idempotence, side_effect, verify, cleanup, destroy
INFO     Performing prerun...
INFO     Added ANSIBLE_LIBRARY=/home/netology/.cache/ansible-compat/c19495/modules:/home/netology/.ansible/plugins/modules:/usr/share/ansible/plugins/modules
INFO     Added ANSIBLE_COLLECTIONS_PATH=/home/netology/.cache/ansible-compat/c19495/collections:/home/netology/.ansible/collections:/usr/share/ansible/collections
INFO     Added ANSIBLE_ROLES_PATH=/home/netology/.cache/ansible-compat/c19495/roles:/home/netology/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles
INFO     Using /home/netology/.ansible/roles/elk.elasticsearch_role symlink to current repository in order to enable Ansible to find the role using its expected full name.
INFO     Running default > dependency
WARNING  Skipping, missing the requirements file.
WARNING  Skipping, missing the requirements file.
INFO     Running default > lint
COMMAND: ansible-lint .
yamllint .

WARNING  Loading custom .yamllint config file, this extends our internal yamllint config.
INFO     Running default > cleanup
WARNING  Skipping, cleanup playbook not configured.
INFO     Running default > destroy
INFO     Sanity checks: 'podman'

PLAY [Destroy] *****************************************************************

TASK [Destroy molecule instance(s)] ********************************************
changed: [localhost] => (item={'command': '/sbin/init', 'image': 'docker.io/pycontribs/centos:7', 'name': 'instance-1', 'networks': ['elk-centos'], 'pre_build_image': True, 'published_ports': ['0.0.0.0:5003:5003/udp', '0.0.0.0:5003:5003/tcp'], 'volumes': ['/sys/fs/cgroup:/sys/fs/cgroup:ro']})
changed: [localhost] => (item={'image': 'docker.io/pycontribs/ubuntu:latest', 'name': 'instance-2', 'networks': ['elk-ubuntu'], 'pre_build_image': True, 'published_ports': ['0.0.0.0:5004:5004/udp', '0.0.0.0:5004:5004/tcp']})

TASK [Wait for instance(s) deletion to complete] *******************************
changed: [localhost] => (item={'failed': 0, 'started': 1, 'finished': 0, 'ansible_job_id': '308608670985.21399', 'results_file': '/home/netology/.ansible_async/308608670985.21399', 'changed': True, 'item': {'command': '/sbin/init', 'image': 'docker.io/pycontribs/centos:7', 'name': 'instance-1', 'networks': ['elk-centos'], 'pre_build_image': True, 'published_ports': ['0.0.0.0:5003:5003/udp', '0.0.0.0:5003:5003/tcp'], 'volumes': ['/sys/fs/cgroup:/sys/fs/cgroup:ro']}, 'ansible_loop_var': 'item'})
changed: [localhost] => (item={'failed': 0, 'started': 1, 'finished': 0, 'ansible_job_id': '315527353367.21427', 'results_file': '/home/netology/.ansible_async/315527353367.21427', 'changed': True, 'item': {'image': 'docker.io/pycontribs/ubuntu:latest', 'name': 'instance-2', 'networks': ['elk-ubuntu'], 'pre_build_image': True, 'published_ports': ['0.0.0.0:5004:5004/udp', '0.0.0.0:5004:5004/tcp']}, 'ansible_loop_var': 'item'})

PLAY RECAP *********************************************************************
localhost                  : ok=2    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

INFO     Running default > syntax

playbook: /home/netology/Projects/ansible_test_roles/playbook/roles/elasticsearch-role/molecule/default/converge.yml
INFO     Running default > create

PLAY [Create] ******************************************************************

TASK [get podman executable path] **********************************************
ok: [localhost]

TASK [save path to executable as fact] *****************************************
ok: [localhost]

TASK [Log into a container registry] *******************************************
skipping: [localhost] => (item="instance-1 registry username: None specified") 
skipping: [localhost] => (item="instance-2 registry username: None specified") 

TASK [Check presence of custom Dockerfiles] ************************************
ok: [localhost] => (item=Dockerfile: None specified)
ok: [localhost] => (item=Dockerfile: None specified)

TASK [Create Dockerfiles from image names] *************************************
skipping: [localhost] => (item="Dockerfile: None specified; Image: docker.io/pycontribs/centos:7") 
skipping: [localhost] => (item="Dockerfile: None specified; Image: docker.io/pycontribs/ubuntu:latest") 

TASK [Discover local Podman images] ********************************************
ok: [localhost] => (item=instance-1)
ok: [localhost] => (item=instance-2)

TASK [Build an Ansible compatible image] ***************************************
skipping: [localhost] => (item=docker.io/pycontribs/centos:7) 
skipping: [localhost] => (item=docker.io/pycontribs/ubuntu:latest) 

TASK [Determine the CMD directives] ********************************************
ok: [localhost] => (item="instance-1 command: /sbin/init")
ok: [localhost] => (item="instance-2 command: None specified")

TASK [Remove possible pre-existing containers] *********************************
changed: [localhost]

TASK [Discover local podman networks] ******************************************
skipping: [localhost] => (item=instance-1: None specified) 
skipping: [localhost] => (item=instance-2: None specified) 

TASK [Create podman network dedicated to this scenario] ************************
skipping: [localhost]

TASK [Create molecule instance(s)] *********************************************
changed: [localhost] => (item=instance-1)
changed: [localhost] => (item=instance-2)

TASK [Wait for instance(s) creation to complete] *******************************
changed: [localhost] => (item=instance-1)
changed: [localhost] => (item=instance-2)

PLAY RECAP *********************************************************************
localhost                  : ok=8    changed=3    unreachable=0    failed=0    skipped=5    rescued=0    ignored=0

INFO     Running default > prepare
WARNING  Skipping, prepare playbook not configured.
INFO     Running default > converge

PLAY [Converge] ****************************************************************

TASK [Gathering Facts] *********************************************************
ok: [instance-2]
ok: [instance-1]

TASK [Include elasticsearch-role] **********************************************

TASK [elasticsearch-role : Fail if unsupported system detected] ****************
skipping: [instance-1]
skipping: [instance-2]

TASK [elasticsearch-role : include_tasks] **************************************
included: /home/netology/Projects/ansible_test_roles/playbook/roles/elasticsearch-role/tasks/download_yum.yml for instance-1
included: /home/netology/Projects/ansible_test_roles/playbook/roles/elasticsearch-role/tasks/download_apt.yml for instance-2

TASK [elasticsearch-role : Download Elasticsearch's rpm] ***********************
ok: [instance-1 -> localhost]

TASK [elasticsearch-role : Copy Elasticsearch to managed node] *****************
diff skipped: source file size is greater than 104448
changed: [instance-1]

TASK [elasticsearch-role : Download Elasticsearch's deb] ***********************
ok: [instance-2 -> localhost]

TASK [elasticsearch-role : Copy Elasticsearch to manage host] ******************
diff skipped: source file size is greater than 104448
changed: [instance-2]

TASK [elasticsearch-role : include_tasks] **************************************
included: /home/netology/Projects/ansible_test_roles/playbook/roles/elasticsearch-role/tasks/install_yum.yml for instance-1
included: /home/netology/Projects/ansible_test_roles/playbook/roles/elasticsearch-role/tasks/install_apt.yml for instance-2

TASK [elasticsearch-role : Update yum package manager repositories cache] ******
ok: [instance-1]

TASK [elasticsearch-role : install EPEL repo] **********************************
ok: [instance-1]

TASK [elasticsearch-role : install python] *************************************
changed: [instance-1]

TASK [elasticsearch-role : Install Java using Ansible] *************************
changed: [instance-1]

TASK [elasticsearch-role : Install Elasticsearch] ******************************
changed: [instance-1]

TASK [elasticsearch-role : Update repositories cache and install "python" package] ***
changed: [instance-2]

TASK [elasticsearch-role : Install Java using Ansible] *************************
The following additional packages will be installed:
  adwaita-icon-theme at-spi2-core ca-certificates-java fontconfig
  fontconfig-config fonts-dejavu-core fonts-dejavu-extra gtk-update-icon-cache
  hicolor-icon-theme humanity-icon-theme java-common libasound2
  libasound2-data libasyncns0 libatk-bridge2.0-0 libatk-wrapper-java
  libatk-wrapper-java-jni libatk1.0-0 libatk1.0-data libatspi2.0-0
  libavahi-client3 libavahi-common-data libavahi-common3 libcairo2 libcroco3
  libcups2 libdatrie1 libdrm-amdgpu1 libdrm-common libdrm-intel1
  libdrm-nouveau2 libdrm-radeon1 libdrm2 libelf1 libflac8 libfontconfig1
  libfontenc1 libfreetype6 libgail-common libgail18 libgdk-pixbuf2.0-0
  libgdk-pixbuf2.0-bin libgdk-pixbuf2.0-common libgif7 libgl1 libgl1-mesa-dri
  libgl1-mesa-glx libglapi-mesa libglvnd0 libglx-mesa0 libglx0 libgraphite2-3
  libgtk2.0-0 libgtk2.0-bin libgtk2.0-common libharfbuzz0b libice-dev libice6
  libjbig0 libjpeg-turbo8 libjpeg8 liblcms2-2 libllvm10 libnspr4 libnss3
  libogg0 libpango-1.0-0 libpangocairo-1.0-0 libpangoft2-1.0-0 libpciaccess0
  libpcsclite1 libpixman-1-0 libpng16-16 libpthread-stubs0-dev libpulse0
  librsvg2-2 librsvg2-common libsensors4 libsm-dev libsm6 libsndfile1
  libthai-data libthai0 libtiff5 libvorbis0a libvorbisenc2 libwrap0 libx11-6
  libx11-dev libx11-doc libx11-xcb1 libxau-dev libxau6 libxaw7 libxcb-dri2-0
  libxcb-dri3-0 libxcb-glx0 libxcb-present0 libxcb-render0 libxcb-shape0
  libxcb-shm0 libxcb-sync1 libxcb1-dev libxcomposite1 libxcursor1 libxdamage1
  libxdmcp-dev libxfixes3 libxft2 libxi6 libxinerama1 libxmu6 libxpm4
  libxrandr2 libxrender1 libxshmfence1 libxt-dev libxt6 libxtst6 libxv1
  libxxf86dga1 libxxf86vm1 openjdk-8-jdk-headless openjdk-8-jre
  openjdk-8-jre-headless ubuntu-mono ucf x11-common x11-utils
  x11proto-core-dev x11proto-dev xorg-sgml-doctools xtrans-dev
Suggested packages:
  default-jre libasound2-plugins alsa-utils cups-common gvfs libice-doc
  liblcms2-utils pciutils pcscd pulseaudio librsvg2-bin lm-sensors libsm-doc
  libxcb-doc libxt-doc openjdk-8-demo openjdk-8-source visualvm
  icedtea-8-plugin libnss-mdns fonts-ipafont-gothic fonts-ipafont-mincho
  fonts-wqy-microhei fonts-wqy-zenhei fonts-indic mesa-utils
The following NEW packages will be installed:
  adwaita-icon-theme at-spi2-core ca-certificates-java fontconfig
  fontconfig-config fonts-dejavu-core fonts-dejavu-extra gtk-update-icon-cache
  hicolor-icon-theme humanity-icon-theme java-common libasound2
  libasound2-data libasyncns0 libatk-bridge2.0-0 libatk-wrapper-java
  libatk-wrapper-java-jni libatk1.0-0 libatk1.0-data libatspi2.0-0
  libavahi-client3 libavahi-common-data libavahi-common3 libcairo2 libcroco3
  libcups2 libdatrie1 libdrm-amdgpu1 libdrm-common libdrm-intel1
  libdrm-nouveau2 libdrm-radeon1 libdrm2 libelf1 libflac8 libfontconfig1
  libfontenc1 libfreetype6 libgail-common libgail18 libgdk-pixbuf2.0-0
  libgdk-pixbuf2.0-bin libgdk-pixbuf2.0-common libgif7 libgl1 libgl1-mesa-dri
  libgl1-mesa-glx libglapi-mesa libglvnd0 libglx-mesa0 libglx0 libgraphite2-3
  libgtk2.0-0 libgtk2.0-bin libgtk2.0-common libharfbuzz0b libice-dev libice6
  libjbig0 libjpeg-turbo8 libjpeg8 liblcms2-2 libllvm10 libnspr4 libnss3
  libogg0 libpango-1.0-0 libpangocairo-1.0-0 libpangoft2-1.0-0 libpciaccess0
  libpcsclite1 libpixman-1-0 libpng16-16 libpthread-stubs0-dev libpulse0
  librsvg2-2 librsvg2-common libsensors4 libsm-dev libsm6 libsndfile1
  libthai-data libthai0 libtiff5 libvorbis0a libvorbisenc2 libwrap0 libx11-dev
  libx11-doc libx11-xcb1 libxau-dev libxaw7 libxcb-dri2-0 libxcb-dri3-0
  libxcb-glx0 libxcb-present0 libxcb-render0 libxcb-shape0 libxcb-shm0
  libxcb-sync1 libxcb1-dev libxcomposite1 libxcursor1 libxdamage1 libxdmcp-dev
  libxfixes3 libxft2 libxi6 libxinerama1 libxmu6 libxpm4 libxrandr2
  libxrender1 libxshmfence1 libxt-dev libxt6 libxtst6 libxv1 libxxf86dga1
  libxxf86vm1 openjdk-8-jdk openjdk-8-jdk-headless openjdk-8-jre
  openjdk-8-jre-headless ubuntu-mono ucf x11-common x11-utils
  x11proto-core-dev x11proto-dev xorg-sgml-doctools xtrans-dev
The following packages will be upgraded:
  libx11-6 libxau6
2 upgraded, 132 newly installed, 0 to remove and 127 not upgraded.
changed: [instance-2]

TASK [elasticsearch-role : Install Elasticsearch] ******************************
Selecting previously unselected package elasticsearch.
(Reading database ... 41443 files and directories currently installed.)
Preparing to unpack .../elasticsearch-7.14.0-amd64.deb ...
Creating elasticsearch group... OK
Creating elasticsearch user... OK
Unpacking elasticsearch (7.14.0) ...
Setting up elasticsearch (7.14.0) ...
### NOT starting on installation, please execute the following statements to configure elasticsearch service to start automatically using chkconfig
 sudo update-rc.d elasticsearch defaults 95 10
### You can start elasticsearch service by executing
 sudo /etc/init.d/elasticsearch start
Created elasticsearch keystore in /etc/elasticsearch/elasticsearch.keystore
changed: [instance-2]

TASK [elasticsearch-role : Configure Elasticsearch] ****************************
skipping: [instance-2]
--- before: /etc/elasticsearch/elasticsearch.yml
+++ after: /home/netology/.ansible/tmp/ansible-local-22149n7dxrn6z/tmpspjjiabw/elasticsearch.yml.j2
@@ -1,82 +1,6 @@
-# ======================== Elasticsearch Configuration =========================
-#
-# NOTE: Elasticsearch comes with reasonable defaults for most settings.
-#       Before you set out to tweak and tune the configuration, make sure you
-#       understand what are you trying to accomplish and the consequences.
-#
-# The primary way of configuring a node is via this file. This template lists
-# the most important settings you may want to configure for a production cluster.
-#
-# Please consult the documentation for further information on configuration options:
-# https://www.elastic.co/guide/en/elasticsearch/reference/index.html
-#
-# ---------------------------------- Cluster -----------------------------------
-#
-# Use a descriptive name for your cluster:
-#
-#cluster.name: my-application
-#
-# ------------------------------------ Node ------------------------------------
-#
-# Use a descriptive name for the node:
-#
-#node.name: node-1
-#
-# Add custom attributes to the node:
-#
-#node.attr.rack: r1
-#
-# ----------------------------------- Paths ------------------------------------
-#
-# Path to directory where to store the data (separate multiple locations by comma):
-#
 path.data: /var/lib/elasticsearch
-#
-# Path to log files:
-#
 path.logs: /var/log/elasticsearch
-#
-# ----------------------------------- Memory -----------------------------------
-#
-# Lock the memory on startup:
-#
-#bootstrap.memory_lock: true
-#
-# Make sure that the heap size is set to about half the memory available
-# on the system and that the owner of the process is allowed to use this
-# limit.
-#
-# Elasticsearch performs poorly when the system is swapping the memory.
-#
-# ---------------------------------- Network -----------------------------------
-#
-# By default Elasticsearch is only accessible on localhost. Set a different
-# address here to expose this node on the network:
-#
-#network.host: 192.168.0.1
-#
-# By default Elasticsearch listens for HTTP traffic on the first free port it
-# finds starting at 9200. Set a specific HTTP port here:
-#
-#http.port: 9200
-#
-# For more information, consult the network module documentation.
-#
-# --------------------------------- Discovery ----------------------------------
-#
-# Pass an initial list of hosts to perform discovery when this node is started:
-# The default list of hosts is ["127.0.0.1", "[::1]"]
-#
-#discovery.seed_hosts: ["host1", "host2"]
-#
-# Bootstrap the cluster using an initial set of master-eligible nodes:
-#
-#cluster.initial_master_nodes: ["node-1", "node-2"]
-#
-# For more information, consult the discovery and cluster formation module documentation.
-#
-# ---------------------------------- Various -----------------------------------
-#
-# Require explicit names when deleting indices:
-#
-#action.destructive_requires_name: true
+discovery.seed_hosts: ["10.0.2.100"]
+node.name: node-a
+bootstrap.memory_lock: true
+cluster.name: es-docker-cluster
\ No newline at end of file

changed: [instance-1]

TASK [elasticsearch-role : Configure Elasticsearch] ****************************
skipping: [instance-1]
--- before: /etc/elasticsearch/elasticsearch.yml
+++ after: /home/netology/.ansible/tmp/ansible-local-22149n7dxrn6z/tmpyrizccs4/elasticsearch.yml.j2
@@ -1,82 +1,6 @@
-# ======================== Elasticsearch Configuration =========================
-#
-# NOTE: Elasticsearch comes with reasonable defaults for most settings.
-#       Before you set out to tweak and tune the configuration, make sure you
-#       understand what are you trying to accomplish and the consequences.
-#
-# The primary way of configuring a node is via this file. This template lists
-# the most important settings you may want to configure for a production cluster.
-#
-# Please consult the documentation for further information on configuration options:
-# https://www.elastic.co/guide/en/elasticsearch/reference/index.html
-#
-# ---------------------------------- Cluster -----------------------------------
-#
-# Use a descriptive name for your cluster:
-#
-#cluster.name: my-application
-#
-# ------------------------------------ Node ------------------------------------
-#
-# Use a descriptive name for the node:
-#
-#node.name: node-1
-#
-# Add custom attributes to the node:
-#
-#node.attr.rack: r1
-#
-# ----------------------------------- Paths ------------------------------------
-#
-# Path to directory where to store the data (separate multiple locations by comma):
-#
 path.data: /var/lib/elasticsearch
-#
-# Path to log files:
-#
 path.logs: /var/log/elasticsearch
-#
-# ----------------------------------- Memory -----------------------------------
-#
-# Lock the memory on startup:
-#
-#bootstrap.memory_lock: true
-#
-# Make sure that the heap size is set to about half the memory available
-# on the system and that the owner of the process is allowed to use this
-# limit.
-#
-# Elasticsearch performs poorly when the system is swapping the memory.
-#
-# ---------------------------------- Network -----------------------------------
-#
-# By default Elasticsearch is only accessible on localhost. Set a different
-# address here to expose this node on the network:
-#
-#network.host: 192.168.0.1
-#
-# By default Elasticsearch listens for HTTP traffic on the first free port it
-# finds starting at 9200. Set a specific HTTP port here:
-#
-#http.port: 9200
-#
-# For more information, consult the network module documentation.
-#
-# --------------------------------- Discovery ----------------------------------
-#
-# Pass an initial list of hosts to perform discovery when this node is started:
-# The default list of hosts is ["127.0.0.1", "[::1]"]
-#
-#discovery.seed_hosts: ["host1", "host2"]
-#
-# Bootstrap the cluster using an initial set of master-eligible nodes:
-#
-#cluster.initial_master_nodes: ["node-1", "node-2"]
-#
-# For more information, consult the discovery and cluster formation module documentation.
-#
-# ---------------------------------- Various -----------------------------------
-#
-# Require explicit names when deleting indices:
-#
-#action.destructive_requires_name: true
+discovery.seed_hosts: ["0.0.0.0"]
+node.name: node-a
+bootstrap.memory_lock: true
+cluster.name: es-docker-cluster
\ No newline at end of file

changed: [instance-2]

RUNNING HANDLER [elasticsearch-role : restart Elasticsearch] *******************
changed: [instance-1]

RUNNING HANDLER [elasticsearch-role : restart Elasticsearch Deb] ***************
changed: [instance-2]

PLAY RECAP *********************************************************************
instance-1                 : ok=12   changed=6    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0
instance-2                 : ok=10   changed=6    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0

INFO     Running default > idempotence

PLAY [Converge] ****************************************************************

TASK [Gathering Facts] *********************************************************
ok: [instance-1]
ok: [instance-2]

TASK [Include elasticsearch-role] **********************************************

TASK [elasticsearch-role : Fail if unsupported system detected] ****************
skipping: [instance-2]
skipping: [instance-1]

TASK [elasticsearch-role : include_tasks] **************************************
included: /home/netology/Projects/ansible_test_roles/playbook/roles/elasticsearch-role/tasks/download_yum.yml for instance-1
included: /home/netology/Projects/ansible_test_roles/playbook/roles/elasticsearch-role/tasks/download_apt.yml for instance-2

TASK [elasticsearch-role : Download Elasticsearch's rpm] ***********************
ok: [instance-1 -> localhost]

TASK [elasticsearch-role : Copy Elasticsearch to managed node] *****************
ok: [instance-1]

TASK [elasticsearch-role : Download Elasticsearch's deb] ***********************
ok: [instance-2 -> localhost]

TASK [elasticsearch-role : Copy Elasticsearch to manage host] ******************
ok: [instance-2]

TASK [elasticsearch-role : include_tasks] **************************************
included: /home/netology/Projects/ansible_test_roles/playbook/roles/elasticsearch-role/tasks/install_yum.yml for instance-1
included: /home/netology/Projects/ansible_test_roles/playbook/roles/elasticsearch-role/tasks/install_apt.yml for instance-2

TASK [elasticsearch-role : Update yum package manager repositories cache] ******
ok: [instance-1]

TASK [elasticsearch-role : install EPEL repo] **********************************
ok: [instance-1]

TASK [elasticsearch-role : install python] *************************************
ok: [instance-1]

TASK [elasticsearch-role : Install Java using Ansible] *************************
ok: [instance-1]

TASK [elasticsearch-role : Install Elasticsearch] ******************************
ok: [instance-1]

TASK [elasticsearch-role : Update repositories cache and install "python" package] ***
ok: [instance-2]

TASK [elasticsearch-role : Install Java using Ansible] *************************
ok: [instance-2]

TASK [elasticsearch-role : Install Elasticsearch] ******************************
ok: [instance-2]

TASK [elasticsearch-role : Configure Elasticsearch] ****************************
skipping: [instance-2]
ok: [instance-1]

TASK [elasticsearch-role : Configure Elasticsearch] ****************************
skipping: [instance-1]
ok: [instance-2]

PLAY RECAP *********************************************************************
instance-1                 : ok=11   changed=0    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0
instance-2                 : ok=9    changed=0    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0

INFO     Idempotence completed successfully.
INFO     Running default > side_effect
WARNING  Skipping, side effect playbook not configured.
INFO     Running default > verify
INFO     Running Ansible Verifier

PLAY [Verify] ******************************************************************

TASK [Example assertion] *******************************************************
ok: [instance-1] => {
    "changed": false,
    "msg": "All assertions passed"
}
ok: [instance-2] => {
    "changed": false,
    "msg": "All assertions passed"
}

PLAY RECAP *********************************************************************
instance-1                 : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
instance-2                 : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

INFO     Verifier completed successfully.
INFO     Running default > cleanup
WARNING  Skipping, cleanup playbook not configured.
INFO     Running default > destroy

PLAY [Destroy] *****************************************************************

TASK [Destroy molecule instance(s)] ********************************************
changed: [localhost] => (item={'command': '/sbin/init', 'image': 'docker.io/pycontribs/centos:7', 'name': 'instance-1', 'networks': ['elk-centos'], 'pre_build_image': True, 'published_ports': ['0.0.0.0:5003:5003/udp', '0.0.0.0:5003:5003/tcp'], 'volumes': ['/sys/fs/cgroup:/sys/fs/cgroup:ro']})
changed: [localhost] => (item={'image': 'docker.io/pycontribs/ubuntu:latest', 'name': 'instance-2', 'networks': ['elk-ubuntu'], 'pre_build_image': True, 'published_ports': ['0.0.0.0:5004:5004/udp', '0.0.0.0:5004:5004/tcp']})

TASK [Wait for instance(s) deletion to complete] *******************************
FAILED - RETRYING: [localhost]: Wait for instance(s) deletion to complete (300 retries left).
changed: [localhost] => (item={'failed': 0, 'started': 1, 'finished': 0, 'ansible_job_id': '633620542142.46639', 'results_file': '/home/netology/.ansible_async/633620542142.46639', 'changed': True, 'item': {'command': '/sbin/init', 'image': 'docker.io/pycontribs/centos:7', 'name': 'instance-1', 'networks': ['elk-centos'], 'pre_build_image': True, 'published_ports': ['0.0.0.0:5003:5003/udp', '0.0.0.0:5003:5003/tcp'], 'volumes': ['/sys/fs/cgroup:/sys/fs/cgroup:ro']}, 'ansible_loop_var': 'item'})
FAILED - RETRYING: [localhost]: Wait for instance(s) deletion to complete (300 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) deletion to complete (299 retries left).
changed: [localhost] => (item={'failed': 0, 'started': 1, 'finished': 0, 'ansible_job_id': '798599428662.46667', 'results_file': '/home/netology/.ansible_async/798599428662.46667', 'changed': True, 'item': {'image': 'docker.io/pycontribs/ubuntu:latest', 'name': 'instance-2', 'networks': ['elk-ubuntu'], 'pre_build_image': True, 'published_ports': ['0.0.0.0:5004:5004/udp', '0.0.0.0:5004:5004/tcp']}, 'ansible_loop_var': 'item'})

PLAY RECAP *********************************************************************
localhost                  : ok=2    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

INFO     Pruning extra files from scenario ephemeral directory
```
