[34mINFO    [0m default scenario test matrix: dependency, lint, cleanup, destroy, syntax, create, prepare, converge, idempotence, side_effect, verify, cleanup, destroy
[34mINFO    [0m Performing prerun[33m...[0m
[34mINFO    [0m Added [33mANSIBLE_LIBRARY[0m=[35m/home/netology/.cache/ansible-compat/c19495/[0m[95mmodules[0m:[35m/home/netology/.ansible/plugins/[0m[95mmodules[0m:[35m/usr/share/ansible/plugins/[0m[95mmodules[0m
[34mINFO    [0m Added [33mANSIBLE_COLLECTIONS_PATH[0m=[35m/home/netology/.cache/ansible-compat/c19495/[0m[95mcollections[0m:[35m/home/netology/.ansible/[0m[95mcollections[0m:[35m/usr/share/ansible/[0m[95mcollections[0m
[34mINFO    [0m Added [33mANSIBLE_ROLES_PATH[0m=[35m/home/netology/.cache/ansible-compat/c19495/[0m[95mroles[0m:[35m/home/netology/.ansible/[0m[95mroles[0m:[35m/usr/share/ansible/[0m[95mroles[0m:[35m/etc/ansible/[0m[95mroles[0m
[34mINFO    [0m Using [35m/home/netology/.ansible/roles/[0m[95melk.elasticsearch_role[0m symlink to current repository in order to enable Ansible to find the role using its expected full name.
[34mINFO    [0m [2;36mRunning [0m[2;32mdefault[0m[2;36m > [0m[2;32mdependency[0m
[31mWARNING [0m Skipping, missing the requirements file.
[31mWARNING [0m Skipping, missing the requirements file.
[34mINFO    [0m [2;36mRunning [0m[2;32mdefault[0m[2;36m > [0m[2;32mlint[0m
COMMAND: ansible-lint .
yamllint .

WARNING  Loading custom .yamllint config file, this extends our internal yamllint config.
[34mINFO    [0m [2;36mRunning [0m[2;32mdefault[0m[2;36m > [0m[2;32mcleanup[0m
[31mWARNING [0m Skipping, cleanup playbook not configured.
[34mINFO    [0m [2;36mRunning [0m[2;32mdefault[0m[2;36m > [0m[2;32mdestroy[0m
[34mINFO    [0m Sanity checks: [32m'docker'[0m

PLAY [Destroy] *****************************************************************

TASK [Destroy molecule instance(s)] ********************************************
[33mchanged: [localhost] => (item=instance-1)[0m
[33mchanged: [localhost] => (item=instance-2)[0m

TASK [Wait for instance(s) deletion to complete] *******************************
[1;30mFAILED - RETRYING: [localhost]: Wait for instance(s) deletion to complete (300 retries left).[0m
[33mchanged: [localhost] => (item=instance-1)[0m
[33mchanged: [localhost] => (item=instance-2)[0m

TASK [Delete docker networks(s)] ***********************************************

PLAY RECAP *********************************************************************
[33mlocalhost[0m                  : [32mok=2   [0m [33mchanged=2   [0m unreachable=0    failed=0    [36mskipped=1   [0m rescued=0    ignored=0

[34mINFO    [0m [2;36mRunning [0m[2;32mdefault[0m[2;36m > [0m[2;32msyntax[0m

playbook: /home/netology/Projects/ansible_test_roles/playbook/roles/elasticsearch-role/molecule/default/converge.yml
[34mINFO    [0m [2;36mRunning [0m[2;32mdefault[0m[2;36m > [0m[2;32mcreate[0m

PLAY [Create] ******************************************************************

TASK [Log into a Docker registry] **********************************************
[36mskipping: [localhost] => (item=None) [0m
[36mskipping: [localhost] => (item=None) [0m
[36mskipping: [localhost][0m

TASK [Check presence of custom Dockerfiles] ************************************
[32mok: [localhost] => (item={'command': '/sbin/init', 'image': 'docker.io/pycontribs/centos:7', 'name': 'instance-1', 'pre_build_image': True, 'privileged': True, 'published_ports': ['0.0.0.0:5003:5003/udp', '0.0.0.0:5003:5003/tcp'], 'volumes': ['/sys/fs/cgroup:/sys/fs/cgroup:ro']})[0m
[32mok: [localhost] => (item={'environment': [{'ES_JAVA_OPTS': '-Xms256m -Xmx256m'}, {'ES_MIN_MEM': '256m'}, {'ES_MAX_MEM': '1g'}, {'discovery.type': 'single-node'}], 'image': 'docker.io/pycontribs/ubuntu:latest', 'name': 'instance-2', 'pre_build_image': True, 'privileged': True, 'published_ports': ['0.0.0.0:5004:5004/udp', '0.0.0.0:5004:5004/tcp']})[0m

TASK [Create Dockerfiles from image names] *************************************
[36mskipping: [localhost] => (item={'command': '/sbin/init', 'image': 'docker.io/pycontribs/centos:7', 'name': 'instance-1', 'pre_build_image': True, 'privileged': True, 'published_ports': ['0.0.0.0:5003:5003/udp', '0.0.0.0:5003:5003/tcp'], 'volumes': ['/sys/fs/cgroup:/sys/fs/cgroup:ro']})[0m
[36mskipping: [localhost] => (item={'environment': [{'ES_JAVA_OPTS': '-Xms256m -Xmx256m'}, {'ES_MIN_MEM': '256m'}, {'ES_MAX_MEM': '1g'}, {'discovery.type': 'single-node'}], 'image': 'docker.io/pycontribs/ubuntu:latest', 'name': 'instance-2', 'pre_build_image': True, 'privileged': True, 'published_ports': ['0.0.0.0:5004:5004/udp', '0.0.0.0:5004:5004/tcp']})[0m

TASK [Discover local Docker images] ********************************************
[32mok: [localhost] => (item={'changed': False, 'skipped': True, 'skip_reason': 'Conditional result was False', 'item': {'command': '/sbin/init', 'image': 'docker.io/pycontribs/centos:7', 'name': 'instance-1', 'pre_build_image': True, 'privileged': True, 'published_ports': ['0.0.0.0:5003:5003/udp', '0.0.0.0:5003:5003/tcp'], 'volumes': ['/sys/fs/cgroup:/sys/fs/cgroup:ro']}, 'ansible_loop_var': 'item', 'i': 0, 'ansible_index_var': 'i'})[0m
[32mok: [localhost] => (item={'changed': False, 'skipped': True, 'skip_reason': 'Conditional result was False', 'item': {'environment': [{'ES_JAVA_OPTS': '-Xms256m -Xmx256m'}, {'ES_MIN_MEM': '256m'}, {'ES_MAX_MEM': '1g'}, {'discovery.type': 'single-node'}], 'image': 'docker.io/pycontribs/ubuntu:latest', 'name': 'instance-2', 'pre_build_image': True, 'privileged': True, 'published_ports': ['0.0.0.0:5004:5004/udp', '0.0.0.0:5004:5004/tcp']}, 'ansible_loop_var': 'item', 'i': 1, 'ansible_index_var': 'i'})[0m

TASK [Build an Ansible compatible image (new)] *********************************
[36mskipping: [localhost] => (item=molecule_local/docker.io/pycontribs/centos:7) [0m
[36mskipping: [localhost] => (item=molecule_local/docker.io/pycontribs/ubuntu:latest) [0m

TASK [Create docker network(s)] ************************************************

TASK [Determine the CMD directives] ********************************************
[32mok: [localhost] => (item={'command': '/sbin/init', 'image': 'docker.io/pycontribs/centos:7', 'name': 'instance-1', 'pre_build_image': True, 'privileged': True, 'published_ports': ['0.0.0.0:5003:5003/udp', '0.0.0.0:5003:5003/tcp'], 'volumes': ['/sys/fs/cgroup:/sys/fs/cgroup:ro']})[0m
[32mok: [localhost] => (item={'environment': [{'ES_JAVA_OPTS': '-Xms256m -Xmx256m'}, {'ES_MIN_MEM': '256m'}, {'ES_MAX_MEM': '1g'}, {'discovery.type': 'single-node'}], 'image': 'docker.io/pycontribs/ubuntu:latest', 'name': 'instance-2', 'pre_build_image': True, 'privileged': True, 'published_ports': ['0.0.0.0:5004:5004/udp', '0.0.0.0:5004:5004/tcp']})[0m

TASK [Create molecule instance(s)] *********************************************
[33mchanged: [localhost] => (item=instance-1)[0m
[33mchanged: [localhost] => (item=instance-2)[0m

TASK [Wait for instance(s) creation to complete] *******************************
[1;30mFAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (300 retries left).[0m
[33mchanged: [localhost] => (item={'failed': 0, 'started': 1, 'finished': 0, 'ansible_job_id': '820322386630.52422', 'results_file': '/home/netology/.ansible_async/820322386630.52422', 'changed': True, 'item': {'command': '/sbin/init', 'image': 'docker.io/pycontribs/centos:7', 'name': 'instance-1', 'pre_build_image': True, 'privileged': True, 'published_ports': ['0.0.0.0:5003:5003/udp', '0.0.0.0:5003:5003/tcp'], 'volumes': ['/sys/fs/cgroup:/sys/fs/cgroup:ro']}, 'ansible_loop_var': 'item'})[0m
[33mchanged: [localhost] => (item={'failed': 0, 'started': 1, 'finished': 0, 'ansible_job_id': '348090485282.52450', 'results_file': '/home/netology/.ansible_async/348090485282.52450', 'changed': True, 'item': {'environment': [{'ES_JAVA_OPTS': '-Xms256m -Xmx256m'}, {'ES_MIN_MEM': '256m'}, {'ES_MAX_MEM': '1g'}, {'discovery.type': 'single-node'}], 'image': 'docker.io/pycontribs/ubuntu:latest', 'name': 'instance-2', 'pre_build_image': True, 'privileged': True, 'published_ports': ['0.0.0.0:5004:5004/udp', '0.0.0.0:5004:5004/tcp']}, 'ansible_loop_var': 'item'})[0m

PLAY RECAP *********************************************************************
[33mlocalhost[0m                  : [32mok=5   [0m [33mchanged=2   [0m unreachable=0    failed=0    [36mskipped=4   [0m rescued=0    ignored=0

[34mINFO    [0m [2;36mRunning [0m[2;32mdefault[0m[2;36m > [0m[2;32mprepare[0m
[31mWARNING [0m Skipping, prepare playbook not configured.
[34mINFO    [0m [2;36mRunning [0m[2;32mdefault[0m[2;36m > [0m[2;32mconverge[0m

PLAY [Converge] ****************************************************************

TASK [Gathering Facts] *********************************************************
[32mok: [instance-2][0m
[32mok: [instance-1][0m

TASK [Include elasticsearch-role] **********************************************

TASK [elasticsearch-role : Fail if unsupported system detected] ****************
[36mskipping: [instance-1][0m
[36mskipping: [instance-2][0m

TASK [elasticsearch-role : include_tasks] **************************************
[36mincluded: /home/netology/Projects/ansible_test_roles/playbook/roles/elasticsearch-role/tasks/download_yum.yml for instance-1[0m
[36mincluded: /home/netology/Projects/ansible_test_roles/playbook/roles/elasticsearch-role/tasks/download_apt.yml for instance-2[0m

TASK [elasticsearch-role : Download Elasticsearch's rpm] ***********************
[32mok: [instance-1 -> localhost][0m

TASK [elasticsearch-role : Copy Elasticsearch to managed node] *****************
diff skipped: source file size is greater than 104448
[33mchanged: [instance-1][0m

TASK [elasticsearch-role : Download Elasticsearch's deb] ***********************
[32mok: [instance-2 -> localhost][0m

TASK [elasticsearch-role : Copy Elasticsearch to manage host] ******************
diff skipped: source file size is greater than 104448
[33mchanged: [instance-2][0m

TASK [elasticsearch-role : include_tasks] **************************************
[36mincluded: /home/netology/Projects/ansible_test_roles/playbook/roles/elasticsearch-role/tasks/install_yum.yml for instance-1[0m
[36mincluded: /home/netology/Projects/ansible_test_roles/playbook/roles/elasticsearch-role/tasks/install_apt.yml for instance-2[0m

TASK [elasticsearch-role : Update yum package manager repositories cache] ******
[32mok: [instance-1][0m

TASK [elasticsearch-role : Install Elasticsearch] ******************************
[33mchanged: [instance-1][0m

TASK [elasticsearch-role : Update repositories cache and install "python" package] ***
[33mchanged: [instance-2][0m

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
2 upgraded, 132 newly installed, 0 to remove and 123 not upgraded.
[33mchanged: [instance-2][0m

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
[33mchanged: [instance-2][0m

TASK [elasticsearch-role : Configure Elasticsearch] ****************************
[36mskipping: [instance-2][0m
[31m--- before: /etc/elasticsearch/elasticsearch.yml[0m
[32m+++ after: /home/netology/.ansible/tmp/ansible-local-53062vkx6fu88/tmpmziarkzo/elasticsearch.yml.j2[0m
[36m@@ -1,82 +1,7 @@[0m
[31m-# ======================== Elasticsearch Configuration =========================[0m
[31m-#[0m
[31m-# NOTE: Elasticsearch comes with reasonable defaults for most settings.[0m
[31m-#       Before you set out to tweak and tune the configuration, make sure you[0m
[31m-#       understand what are you trying to accomplish and the consequences.[0m
[31m-#[0m
[31m-# The primary way of configuring a node is via this file. This template lists[0m
[31m-# the most important settings you may want to configure for a production cluster.[0m
[31m-#[0m
[31m-# Please consult the documentation for further information on configuration options:[0m
[31m-# https://www.elastic.co/guide/en/elasticsearch/reference/index.html[0m
[31m-#[0m
[31m-# ---------------------------------- Cluster -----------------------------------[0m
[31m-#[0m
[31m-# Use a descriptive name for your cluster:[0m
[31m-#[0m
[31m-#cluster.name: my-application[0m
[31m-#[0m
[31m-# ------------------------------------ Node ------------------------------------[0m
[31m-#[0m
[31m-# Use a descriptive name for the node:[0m
[31m-#[0m
[31m-#node.name: node-1[0m
[31m-#[0m
[31m-# Add custom attributes to the node:[0m
[31m-#[0m
[31m-#node.attr.rack: r1[0m
[31m-#[0m
[31m-# ----------------------------------- Paths ------------------------------------[0m
[31m-#[0m
[31m-# Path to directory where to store the data (separate multiple locations by comma):[0m
[31m-#[0m
 path.data: /var/lib/elasticsearch
[31m-#[0m
[31m-# Path to log files:[0m
[31m-#[0m
 path.logs: /var/log/elasticsearch
[31m-#[0m
[31m-# ----------------------------------- Memory -----------------------------------[0m
[31m-#[0m
[31m-# Lock the memory on startup:[0m
[31m-#[0m
[31m-#bootstrap.memory_lock: true[0m
[31m-#[0m
[31m-# Make sure that the heap size is set to about half the memory available[0m
[31m-# on the system and that the owner of the process is allowed to use this[0m
[31m-# limit.[0m
[31m-#[0m
[31m-# Elasticsearch performs poorly when the system is swapping the memory.[0m
[31m-#[0m
[31m-# ---------------------------------- Network -----------------------------------[0m
[31m-#[0m
[31m-# By default Elasticsearch is only accessible on localhost. Set a different[0m
[31m-# address here to expose this node on the network:[0m
[31m-#[0m
[31m-#network.host: 192.168.0.1[0m
[31m-#[0m
[31m-# By default Elasticsearch listens for HTTP traffic on the first free port it[0m
[31m-# finds starting at 9200. Set a specific HTTP port here:[0m
[31m-#[0m
[31m-#http.port: 9200[0m
[31m-#[0m
[31m-# For more information, consult the network module documentation.[0m
[31m-#[0m
[31m-# --------------------------------- Discovery ----------------------------------[0m
[31m-#[0m
[31m-# Pass an initial list of hosts to perform discovery when this node is started:[0m
[31m-# The default list of hosts is ["127.0.0.1", "[::1]"][0m
[31m-#[0m
[31m-#discovery.seed_hosts: ["host1", "host2"][0m
[31m-#[0m
[31m-# Bootstrap the cluster using an initial set of master-eligible nodes:[0m
[31m-#[0m
[31m-#cluster.initial_master_nodes: ["node-1", "node-2"][0m
[31m-#[0m
[31m-# For more information, consult the discovery and cluster formation module documentation.[0m
[31m-#[0m
[31m-# ---------------------------------- Various -----------------------------------[0m
[31m-#[0m
[31m-# Require explicit names when deleting indices:[0m
[31m-#[0m
[31m-#action.destructive_requires_name: true[0m
[32m+network.host: 0.0.0.0[0m
[32m+discovery.seed_hosts: ["172.17.0.2"][0m
[32m+node.name: node-a[0m
[32m+cluster.initial_master_nodes: [0m
[32m+   - node-a[0m

[33mchanged: [instance-1][0m

TASK [elasticsearch-role : Configure Elasticsearch] ****************************
[36mskipping: [instance-1][0m
[31m--- before: /etc/elasticsearch/elasticsearch.yml[0m
[32m+++ after: /home/netology/.ansible/tmp/ansible-local-53062vkx6fu88/tmpt0bbcbwx/elasticsearch.yml.j2[0m
[36m@@ -1,82 +1,13 @@[0m
[31m-# ======================== Elasticsearch Configuration =========================[0m
[31m-#[0m
[31m-# NOTE: Elasticsearch comes with reasonable defaults for most settings.[0m
[31m-#       Before you set out to tweak and tune the configuration, make sure you[0m
[31m-#       understand what are you trying to accomplish and the consequences.[0m
[31m-#[0m
[31m-# The primary way of configuring a node is via this file. This template lists[0m
[31m-# the most important settings you may want to configure for a production cluster.[0m
[31m-#[0m
[31m-# Please consult the documentation for further information on configuration options:[0m
[31m-# https://www.elastic.co/guide/en/elasticsearch/reference/index.html[0m
[31m-#[0m
[31m-# ---------------------------------- Cluster -----------------------------------[0m
[31m-#[0m
[31m-# Use a descriptive name for your cluster:[0m
[31m-#[0m
[31m-#cluster.name: my-application[0m
[31m-#[0m
[31m-# ------------------------------------ Node ------------------------------------[0m
[31m-#[0m
[31m-# Use a descriptive name for the node:[0m
[31m-#[0m
[31m-#node.name: node-1[0m
[31m-#[0m
[31m-# Add custom attributes to the node:[0m
[31m-#[0m
[31m-#node.attr.rack: r1[0m
[31m-#[0m
[31m-# ----------------------------------- Paths ------------------------------------[0m
[31m-#[0m
[31m-# Path to directory where to store the data (separate multiple locations by comma):[0m
[31m-#[0m
 path.data: /var/lib/elasticsearch
[31m-#[0m
[31m-# Path to log files:[0m
[31m-#[0m
 path.logs: /var/log/elasticsearch
[31m-#[0m
[31m-# ----------------------------------- Memory -----------------------------------[0m
[31m-#[0m
[31m-# Lock the memory on startup:[0m
[31m-#[0m
[31m-#bootstrap.memory_lock: true[0m
[31m-#[0m
[31m-# Make sure that the heap size is set to about half the memory available[0m
[31m-# on the system and that the owner of the process is allowed to use this[0m
[31m-# limit.[0m
[31m-#[0m
[31m-# Elasticsearch performs poorly when the system is swapping the memory.[0m
[31m-#[0m
[31m-# ---------------------------------- Network -----------------------------------[0m
[31m-#[0m
[31m-# By default Elasticsearch is only accessible on localhost. Set a different[0m
[31m-# address here to expose this node on the network:[0m
[31m-#[0m
[31m-#network.host: 192.168.0.1[0m
[31m-#[0m
[31m-# By default Elasticsearch listens for HTTP traffic on the first free port it[0m
[31m-# finds starting at 9200. Set a specific HTTP port here:[0m
[31m-#[0m
[31m-#http.port: 9200[0m
[31m-#[0m
[31m-# For more information, consult the network module documentation.[0m
[31m-#[0m
[31m-# --------------------------------- Discovery ----------------------------------[0m
[31m-#[0m
[31m-# Pass an initial list of hosts to perform discovery when this node is started:[0m
[31m-# The default list of hosts is ["127.0.0.1", "[::1]"][0m
[31m-#[0m
[31m-#discovery.seed_hosts: ["host1", "host2"][0m
[31m-#[0m
[31m-# Bootstrap the cluster using an initial set of master-eligible nodes:[0m
[31m-#[0m
[31m-#cluster.initial_master_nodes: ["node-1", "node-2"][0m
[31m-#[0m
[31m-# For more information, consult the discovery and cluster formation module documentation.[0m
[31m-#[0m
[31m-# ---------------------------------- Various -----------------------------------[0m
[31m-#[0m
[31m-# Require explicit names when deleting indices:[0m
[31m-#[0m
[31m-#action.destructive_requires_name: true[0m
[32m+network.host: 0.0.0.0[0m
[32m+discovery.seed_hosts: ["0.0.0.0"][0m
[32m+node.name: node-a[0m
[32m+cluster.initial_master_nodes: [0m
[32m+   - node-a[0m
[32m+   [0m
[32m+http.cors.enabled: true[0m
[32m+http.cors.allow-origin: "*"[0m
[32m+http.cors.allow-headers: Authorization[0m
[32m+xpack.security.enabled: true[0m
[32m+xpack.security.transport.ssl.enabled: true[0m

[33mchanged: [instance-2][0m

RUNNING HANDLER [elasticsearch-role : restart Elasticsearch] *******************
[33mchanged: [instance-1][0m

RUNNING HANDLER [elasticsearch-role : restart Elasticsearch Deb] ***************
[33mchanged: [instance-2][0m

PLAY RECAP *********************************************************************
[33minstance-1[0m                 : [32mok=9   [0m [33mchanged=4   [0m unreachable=0    failed=0    [36mskipped=2   [0m rescued=0    ignored=0
[33minstance-2[0m                 : [32mok=10  [0m [33mchanged=6   [0m unreachable=0    failed=0    [36mskipped=2   [0m rescued=0    ignored=0

[34mINFO    [0m [2;36mRunning [0m[2;32mdefault[0m[2;36m > [0m[2;32midempotence[0m

PLAY [Converge] ****************************************************************

TASK [Gathering Facts] *********************************************************
[32mok: [instance-2][0m
[32mok: [instance-1][0m

TASK [Include elasticsearch-role] **********************************************

TASK [elasticsearch-role : Fail if unsupported system detected] ****************
[36mskipping: [instance-1][0m
[36mskipping: [instance-2][0m

TASK [elasticsearch-role : include_tasks] **************************************
[36mincluded: /home/netology/Projects/ansible_test_roles/playbook/roles/elasticsearch-role/tasks/download_yum.yml for instance-1[0m
[36mincluded: /home/netology/Projects/ansible_test_roles/playbook/roles/elasticsearch-role/tasks/download_apt.yml for instance-2[0m

TASK [elasticsearch-role : Download Elasticsearch's rpm] ***********************
[32mok: [instance-1 -> localhost][0m

TASK [elasticsearch-role : Copy Elasticsearch to managed node] *****************
[32mok: [instance-1][0m

TASK [elasticsearch-role : Download Elasticsearch's deb] ***********************
[32mok: [instance-2 -> localhost][0m

TASK [elasticsearch-role : Copy Elasticsearch to manage host] ******************
[32mok: [instance-2][0m

TASK [elasticsearch-role : include_tasks] **************************************
[36mincluded: /home/netology/Projects/ansible_test_roles/playbook/roles/elasticsearch-role/tasks/install_yum.yml for instance-1[0m
[36mincluded: /home/netology/Projects/ansible_test_roles/playbook/roles/elasticsearch-role/tasks/install_apt.yml for instance-2[0m

TASK [elasticsearch-role : Update yum package manager repositories cache] ******
[32mok: [instance-1][0m

TASK [elasticsearch-role : Install Elasticsearch] ******************************
[32mok: [instance-1][0m

TASK [elasticsearch-role : Update repositories cache and install "python" package] ***
[32mok: [instance-2][0m

TASK [elasticsearch-role : Install Java using Ansible] *************************
[32mok: [instance-2][0m

TASK [elasticsearch-role : Install Elasticsearch] ******************************
[32mok: [instance-2][0m

TASK [elasticsearch-role : Configure Elasticsearch] ****************************
[36mskipping: [instance-2][0m
[32mok: [instance-1][0m

TASK [elasticsearch-role : Configure Elasticsearch] ****************************
[36mskipping: [instance-1][0m
[32mok: [instance-2][0m

PLAY RECAP *********************************************************************
[32minstance-1[0m                 : [32mok=8   [0m changed=0    unreachable=0    failed=0    [36mskipped=2   [0m rescued=0    ignored=0
[32minstance-2[0m                 : [32mok=9   [0m changed=0    unreachable=0    failed=0    [36mskipped=2   [0m rescued=0    ignored=0

[34mINFO    [0m Idempotence completed successfully.
[34mINFO    [0m [2;36mRunning [0m[2;32mdefault[0m[2;36m > [0m[2;32mside_effect[0m
[31mWARNING [0m Skipping, side effect playbook not configured.
[34mINFO    [0m [2;36mRunning [0m[2;32mdefault[0m[2;36m > [0m[2;32mverify[0m
[34mINFO    [0m Running Ansible Verifier

PLAY [Verify] ******************************************************************

TASK [Example assertion] *******************************************************
[32mok: [instance-2] => {[0m
[32m    "changed": false,[0m
[32m    "msg": "All assertions passed"[0m
[32m}[0m
[32mok: [instance-1] => {[0m
[32m    "changed": false,[0m
[32m    "msg": "All assertions passed"[0m
[32m}[0m

PLAY RECAP *********************************************************************
[32minstance-1[0m                 : [32mok=1   [0m changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
[32minstance-2[0m                 : [32mok=1   [0m changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

[34mINFO    [0m Verifier completed successfully.
[34mINFO    [0m [2;36mRunning [0m[2;32mdefault[0m[2;36m > [0m[2;32mcleanup[0m
[31mWARNING [0m Skipping, cleanup playbook not configured.
[34mINFO    [0m [2;36mRunning [0m[2;32mdefault[0m[2;36m > [0m[2;32mdestroy[0m

PLAY [Destroy] *****************************************************************

TASK [Destroy molecule instance(s)] ********************************************
[33mchanged: [localhost] => (item=instance-1)[0m
[33mchanged: [localhost] => (item=instance-2)[0m

TASK [Wait for instance(s) deletion to complete] *******************************
[1;30mFAILED - RETRYING: [localhost]: Wait for instance(s) deletion to complete (300 retries left).[0m
[33mchanged: [localhost] => (item=instance-1)[0m
[33mchanged: [localhost] => (item=instance-2)[0m

TASK [Delete docker networks(s)] ***********************************************

PLAY RECAP *********************************************************************
[33mlocalhost[0m                  : [32mok=2   [0m [33mchanged=2   [0m unreachable=0    failed=0    [36mskipped=1   [0m rescued=0    ignored=0

[34mINFO    [0m Pruning extra files from scenario ephemeral directory
