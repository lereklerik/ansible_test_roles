```shell
netology@netology:~/Projects/ansible_test_roles/playbook/roles/kibana-role$ molecule converge
INFO     default scenario test matrix: dependency, create, prepare, converge
INFO     Performing prerun...
INFO     Added ANSIBLE_LIBRARY=/home/netology/.cache/ansible-compat/1a2f45/modules:/home/netology/.ansible/plugins/modules:/usr/share/ansible/plugins/modules
INFO     Added ANSIBLE_COLLECTIONS_PATH=/home/netology/.cache/ansible-compat/1a2f45/collections:/home/netology/.ansible/collections:/usr/share/ansible/collections
INFO     Added ANSIBLE_ROLES_PATH=/home/netology/.cache/ansible-compat/1a2f45/roles:/home/netology/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles
INFO     Running default > dependency
WARNING  Skipping, missing the requirements file.
WARNING  Skipping, missing the requirements file.
INFO     Running default > create
INFO     Sanity checks: 'podman'

PLAY [Create] ******************************************************************

TASK [get podman executable path] **********************************************
ok: [localhost]

TASK [save path to executable as fact] *****************************************
ok: [localhost]

TASK [Log into a container registry] *******************************************
skipping: [localhost] => (item="instance-3 registry username: None specified") 
skipping: [localhost] => (item="instance-4 registry username: None specified") 

TASK [Check presence of custom Dockerfiles] ************************************
ok: [localhost] => (item=Dockerfile: None specified)
ok: [localhost] => (item=Dockerfile: None specified)

TASK [Create Dockerfiles from image names] *************************************
skipping: [localhost] => (item="Dockerfile: None specified; Image: docker.io/pycontribs/centos:7") 
skipping: [localhost] => (item="Dockerfile: None specified; Image: docker.io/pycontribs/ubuntu:latest") 

TASK [Discover local Podman images] ********************************************
ok: [localhost] => (item=instance-3)
ok: [localhost] => (item=instance-4)

TASK [Build an Ansible compatible image] ***************************************
skipping: [localhost] => (item=docker.io/pycontribs/centos:7) 
skipping: [localhost] => (item=docker.io/pycontribs/ubuntu:latest) 

TASK [Determine the CMD directives] ********************************************
ok: [localhost] => (item="instance-3 command: /sbin/init")
ok: [localhost] => (item="instance-4 command: None specified")

TASK [Remove possible pre-existing containers] *********************************
changed: [localhost]

TASK [Discover local podman networks] ******************************************
skipping: [localhost] => (item=instance-3: None specified) 
skipping: [localhost] => (item=instance-4: None specified) 

TASK [Create podman network dedicated to this scenario] ************************
skipping: [localhost]

TASK [Create molecule instance(s)] *********************************************
changed: [localhost] => (item=instance-3)
changed: [localhost] => (item=instance-4)

TASK [Wait for instance(s) creation to complete] *******************************
changed: [localhost] => (item=instance-3)
changed: [localhost] => (item=instance-4)

PLAY RECAP *********************************************************************
localhost                  : ok=8    changed=3    unreachable=0    failed=0    skipped=5    rescued=0    ignored=0

INFO     Running default > prepare
WARNING  Skipping, prepare playbook not configured.
INFO     Running default > converge

PLAY [Converge] ****************************************************************

TASK [Gathering Facts] *********************************************************
ok: [instance-4]
ok: [instance-3]

TASK [Include kibana-role] *****************************************************

TASK [kibana-role : Fail if unsupported system detected] ***********************
skipping: [instance-3]
skipping: [instance-4]

TASK [kibana-role : include_tasks] *********************************************
included: /home/netology/Projects/ansible_test_roles/playbook/roles/kibana-role/tasks/download_yum.yml for instance-3
included: /home/netology/Projects/ansible_test_roles/playbook/roles/kibana-role/tasks/download_apt.yml for instance-4

TASK [kibana-role : Download Kibana's rpm] *************************************
ok: [instance-3 -> localhost]

TASK [kibana-role : Copy Kibana to managed node] *******************************
diff skipped: source file size is greater than 104448
changed: [instance-3]

TASK [kibana-role : Download Kibana's deb] *************************************
ok: [instance-4 -> localhost]

TASK [kibana-role : Copy kibana to manage host] ********************************
diff skipped: source file size is greater than 104448
changed: [instance-4]

TASK [kibana-role : include_tasks] *********************************************
included: /home/netology/Projects/ansible_test_roles/playbook/roles/kibana-role/tasks/install_yum.yml for instance-3
included: /home/netology/Projects/ansible_test_roles/playbook/roles/kibana-role/tasks/install_apt.yml for instance-4

TASK [kibana-role : Update cache] **********************************************
ok: [instance-3]

TASK [kibana-role : Install Kibana] ********************************************
changed: [instance-3]

TASK [kibana-role : Update repositories cache] *********************************
changed: [instance-4]

TASK [kibana-role : Install Kibana] ********************************************
Selecting previously unselected package kibana.
(Reading database ... 25352 files and directories currently installed.)
Preparing to unpack /tmp/kibana-7.14.0-amd64.deb ...
Unpacking kibana (7.14.0) ...
Setting up kibana (7.14.0) ...
Creating kibana group... OK
Creating kibana user... OK
Created Kibana keystore in /etc/kibana/kibana.keystore
changed: [instance-4]

TASK [kibana-role : Configure Kibana] ******************************************
skipping: [instance-4]
--- before: /etc/kibana/kibana.yml
+++ after: /home/netology/.ansible/tmp/ansible-local-306406y0hqvc8g/tmpqb_e8hhm/kibana.yml.j2
@@ -1,111 +1,6 @@
-# Kibana is served by a back end server. This setting specifies the port to use.
-#server.port: 5601
-
-# Specifies the address to which the Kibana server will bind. IP addresses and host names are both valid values.
-# The default is 'localhost', which usually means remote machines will not be able to connect.
-# To allow connections from remote users, set this parameter to a non-loopback address.
-#server.host: "localhost"
-
-# Enables you to specify a path to mount Kibana at if you are running behind a proxy.
-# Use the `server.rewriteBasePath` setting to tell Kibana if it should remove the basePath
-# from requests it receives, and to prevent a deprecation warning at startup.
-# This setting cannot end in a slash.
-#server.basePath: ""
-
-# Specifies whether Kibana should rewrite requests that are prefixed with
-# `server.basePath` or require that they are rewritten by your reverse proxy.
-# This setting was effectively always `false` before Kibana 6.3 and will
-# default to `true` starting in Kibana 7.0.
-#server.rewriteBasePath: false
-
-# Specifies the public URL at which Kibana is available for end users. If
-# `server.basePath` is configured this URL should end with the same basePath.
-#server.publicBaseUrl: ""
-
-# The maximum payload size in bytes for incoming server requests.
-#server.maxPayload: 1048576
-
-# The Kibana server's name.  This is used for display purposes.
-#server.name: "your-hostname"
-
-# The URLs of the Elasticsearch instances to use for all your queries.
-#elasticsearch.hosts: ["http://localhost:9200"]
-
-# Kibana uses an index in Elasticsearch to store saved searches, visualizations and
-# dashboards. Kibana creates a new index if the index doesn't already exist.
-#kibana.index: ".kibana"
-
-# The default application to load.
-#kibana.defaultAppId: "home"
-
-# If your Elasticsearch is protected with basic authentication, these settings provide
-# the username and password that the Kibana server uses to perform maintenance on the Kibana
-# index at startup. Your Kibana users still need to authenticate with Elasticsearch, which
-# is proxied through the Kibana server.
-#elasticsearch.username: "kibana_system"
-#elasticsearch.password: "pass"
-
-# Enables SSL and paths to the PEM-format SSL certificate and SSL key files, respectively.
-# These settings enable SSL for outgoing requests from the Kibana server to the browser.
-#server.ssl.enabled: false
-#server.ssl.certificate: /path/to/your/server.crt
-#server.ssl.key: /path/to/your/server.key
-
-# Optional settings that provide the paths to the PEM-format SSL certificate and key files.
-# These files are used to verify the identity of Kibana to Elasticsearch and are required when
-# xpack.security.http.ssl.client_authentication in Elasticsearch is set to required.
-#elasticsearch.ssl.certificate: /path/to/your/client.crt
-#elasticsearch.ssl.key: /path/to/your/client.key
-
-# Optional setting that enables you to specify a path to the PEM file for the certificate
-# authority for your Elasticsearch instance.
-#elasticsearch.ssl.certificateAuthorities: [ "/path/to/your/CA.pem" ]
-
-# To disregard the validity of SSL certificates, change this setting's value to 'none'.
-#elasticsearch.ssl.verificationMode: full
-
-# Time in milliseconds to wait for Elasticsearch to respond to pings. Defaults to the value of
-# the elasticsearch.requestTimeout setting.
-#elasticsearch.pingTimeout: 1500
-
-# Time in milliseconds to wait for responses from the back end or Elasticsearch. This value
-# must be a positive integer.
-#elasticsearch.requestTimeout: 30000
-
-# List of Kibana client-side headers to send to Elasticsearch. To send *no* client-side
-# headers, set this value to [] (an empty list).
-#elasticsearch.requestHeadersWhitelist: [ authorization ]
-
-# Header names and values that are sent to Elasticsearch. Any custom headers cannot be overwritten
-# by client-side headers, regardless of the elasticsearch.requestHeadersWhitelist configuration.
-#elasticsearch.customHeaders: {}
-
-# Time in milliseconds for Elasticsearch to wait for responses from shards. Set to 0 to disable.
-#elasticsearch.shardTimeout: 30000
-
-# Logs queries sent to Elasticsearch. Requires logging.verbose set to true.
-#elasticsearch.logQueries: false
-
-# Specifies the path where Kibana creates the process ID file.
-#pid.file: /run/kibana/kibana.pid
-
-# Enables you to specify a file where Kibana stores log output.
-#logging.dest: stdout
-
-# Set the value of this setting to true to suppress all logging output.
-#logging.silent: false
-
-# Set the value of this setting to true to suppress all logging output other than error messages.
-#logging.quiet: false
-
-# Set the value of this setting to true to log all events, including system usage information
-# and all requests.
-#logging.verbose: false
-
-# Set the interval in milliseconds to sample system and process performance
-# metrics. Minimum is 100ms. Defaults to 5000.
-#ops.interval: 5000
-
-# Specifies locale to be used for all localizable strings, dates and number formats.
-# Supported languages are the following: English - en , by default , Chinese - zh-CN .
-#i18n.locale: "en"
+server.name: kibana
+server.host: "0.0.0.0"
+server.shutdownTimeout: "5s"
+xpack.monitoring.ui.container.elasticsearch.enabled: true
+elasticsearch.hosts: ["http://instance-1:9200"]
+kibana.index: ".kibana"
\ No newline at end of file

changed: [instance-3]

TASK [kibana-role : Configure Kibana] ******************************************
skipping: [instance-3]
--- before: /etc/kibana/kibana.yml
+++ after: /home/netology/.ansible/tmp/ansible-local-306406y0hqvc8g/tmpcyknp52s/kibana.yml.j2
@@ -1,111 +1,6 @@
-# Kibana is served by a back end server. This setting specifies the port to use.
-#server.port: 5601
-
-# Specifies the address to which the Kibana server will bind. IP addresses and host names are both valid values.
-# The default is 'localhost', which usually means remote machines will not be able to connect.
-# To allow connections from remote users, set this parameter to a non-loopback address.
-#server.host: "localhost"
-
-# Enables you to specify a path to mount Kibana at if you are running behind a proxy.
-# Use the `server.rewriteBasePath` setting to tell Kibana if it should remove the basePath
-# from requests it receives, and to prevent a deprecation warning at startup.
-# This setting cannot end in a slash.
-#server.basePath: ""
-
-# Specifies whether Kibana should rewrite requests that are prefixed with
-# `server.basePath` or require that they are rewritten by your reverse proxy.
-# This setting was effectively always `false` before Kibana 6.3 and will
-# default to `true` starting in Kibana 7.0.
-#server.rewriteBasePath: false
-
-# Specifies the public URL at which Kibana is available for end users. If
-# `server.basePath` is configured this URL should end with the same basePath.
-#server.publicBaseUrl: ""
-
-# The maximum payload size in bytes for incoming server requests.
-#server.maxPayload: 1048576
-
-# The Kibana server's name.  This is used for display purposes.
-#server.name: "your-hostname"
-
-# The URLs of the Elasticsearch instances to use for all your queries.
-#elasticsearch.hosts: ["http://localhost:9200"]
-
-# Kibana uses an index in Elasticsearch to store saved searches, visualizations and
-# dashboards. Kibana creates a new index if the index doesn't already exist.
-#kibana.index: ".kibana"
-
-# The default application to load.
-#kibana.defaultAppId: "home"
-
-# If your Elasticsearch is protected with basic authentication, these settings provide
-# the username and password that the Kibana server uses to perform maintenance on the Kibana
-# index at startup. Your Kibana users still need to authenticate with Elasticsearch, which
-# is proxied through the Kibana server.
-#elasticsearch.username: "kibana_system"
-#elasticsearch.password: "pass"
-
-# Enables SSL and paths to the PEM-format SSL certificate and SSL key files, respectively.
-# These settings enable SSL for outgoing requests from the Kibana server to the browser.
-#server.ssl.enabled: false
-#server.ssl.certificate: /path/to/your/server.crt
-#server.ssl.key: /path/to/your/server.key
-
-# Optional settings that provide the paths to the PEM-format SSL certificate and key files.
-# These files are used to verify the identity of Kibana to Elasticsearch and are required when
-# xpack.security.http.ssl.client_authentication in Elasticsearch is set to required.
-#elasticsearch.ssl.certificate: /path/to/your/client.crt
-#elasticsearch.ssl.key: /path/to/your/client.key
-
-# Optional setting that enables you to specify a path to the PEM file for the certificate
-# authority for your Elasticsearch instance.
-#elasticsearch.ssl.certificateAuthorities: [ "/path/to/your/CA.pem" ]
-
-# To disregard the validity of SSL certificates, change this setting's value to 'none'.
-#elasticsearch.ssl.verificationMode: full
-
-# Time in milliseconds to wait for Elasticsearch to respond to pings. Defaults to the value of
-# the elasticsearch.requestTimeout setting.
-#elasticsearch.pingTimeout: 1500
-
-# Time in milliseconds to wait for responses from the back end or Elasticsearch. This value
-# must be a positive integer.
-#elasticsearch.requestTimeout: 30000
-
-# List of Kibana client-side headers to send to Elasticsearch. To send *no* client-side
-# headers, set this value to [] (an empty list).
-#elasticsearch.requestHeadersWhitelist: [ authorization ]
-
-# Header names and values that are sent to Elasticsearch. Any custom headers cannot be overwritten
-# by client-side headers, regardless of the elasticsearch.requestHeadersWhitelist configuration.
-#elasticsearch.customHeaders: {}
-
-# Time in milliseconds for Elasticsearch to wait for responses from shards. Set to 0 to disable.
-#elasticsearch.shardTimeout: 30000
-
-# Logs queries sent to Elasticsearch. Requires logging.verbose set to true.
-#elasticsearch.logQueries: false
-
-# Specifies the path where Kibana creates the process ID file.
-#pid.file: /run/kibana/kibana.pid
-
-# Enables you to specify a file where Kibana stores log output.
-#logging.dest: stdout
-
-# Set the value of this setting to true to suppress all logging output.
-#logging.silent: false
-
-# Set the value of this setting to true to suppress all logging output other than error messages.
-#logging.quiet: false
-
-# Set the value of this setting to true to log all events, including system usage information
-# and all requests.
-#logging.verbose: false
-
-# Set the interval in milliseconds to sample system and process performance
-# metrics. Minimum is 100ms. Defaults to 5000.
-#ops.interval: 5000
-
-# Specifies locale to be used for all localizable strings, dates and number formats.
-# Supported languages are the following: English - en , by default , Chinese - zh-CN .
-#i18n.locale: "en"
+server.name: kibana
+server.host: "0.0.0.0"
+server.shutdownTimeout: "5s"
+xpack.monitoring.ui.container.elasticsearch.enabled: true
+elasticsearch.hosts: ["http://instance-2:9200"]
+kibana.index: ".kibana"
\ No newline at end of file

changed: [instance-4]

RUNNING HANDLER [kibana-role : restart Kibana Centos] **************************
changed: [instance-3]

RUNNING HANDLER [kibana-role : restart Kibana Deb] *****************************
changed: [instance-4]

PLAY RECAP *********************************************************************
instance-3                 : ok=9    changed=4    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0
instance-4                 : ok=9    changed=5    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0

```