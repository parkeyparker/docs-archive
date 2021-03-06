---
layout: default
title: "Split Puppet Enterprise Install, Puppet Master Answer File Reference"
canonical: "/pe/latest/install_split_console_answers.html"
---

The following example answers can be used as a baseline to perform an automated split installation of PE on the node assigned to the Puppet master component.

A .txt file version can be found in the `answers` directory of the PE installer tarball.

See [Installing with an answer file](./install_automated.html) for more details. In addition, [the Complete Answer File Reference](./install_complete_answer_file_reference.html) contains all answers that you can use to install PE.

>**Warning**: If you're performing a split installation of PE using an answer file, install the components in the following order:
>
> 1. Puppet master
> 2. Puppet DB and database support (which includes the console database)
> 3. The PE console

### Global Answers
These answers are always needed.

#### `q_install=y`

**Y** or **N** --- Whether to install. Answer files must set this to Y.

#### `q_vendor_packages_install=y`

**Y** or **N** --- Whether the installer has permission to install additional packages from the OS’s repositories. If this is set to N, the installation will fail if the installer detects missing dependencies.

### Additional Global Answers

These answers are optional.

#### `q_run_updtvpkg`

**Y** or **N** --- Only used on AIX. Whether to run `updtvpkg` command to add info about native libraries to the RPM database. The answer should usually be "Y", unelss you have special needs around the RPM.

### Component Answers
These answers are always needed.

#### `q_puppetmaster_install=y`

**Y** or **N** --- Whether to install the Puppet master component.

#### `q_puppetdb_install=n`

**Y** or **N** --- Whether to install the database support (the console Postgres server and PuppetDB) component.

### Additional Component Answers

These answers are optional.

#### `q_puppetagent_install`

**Y** or **N** --- Whether to install the Puppet agent component.

### Puppet Agent Answers
These answers are always needed.

#### `q_fail_on_unsuccessful_master_lookup`

**Y** or **N** --- Whether to quit the install if the Puppet master cannot be reached.

#### `q_skip_master_verification=n`

**Y** or **N** --- This is a silent install option, default is N. When set to "Y", the installer will skip master verification which allows the user to deploy agents when they know the master won’t be available.

### Puppet Master Answers
These answers are generally needed if you are installing the Puppet master component.

#### `q_all_in_one_install=n`

**Y** or **N** --- Whether or not the installation is an all-in-one installation, (i.e., are puppetdb and the console also being installed on this node).

#### `q_puppetmaster_certname=pe-master.<your local domain>`

**String** --- An identifying string for the Puppet master. This ID must be unique across your entire site. The server’s fully qualified domain name is often used as the Puppet master’s certname.

#### `q_puppetmaster_dnsaltnames=pe-master,pe-master.<your local domain>`

**String** --- Valid DNS names at which the Puppet master can be reached. Must be a comma-separated list. In a normal installation, defaults to <hostname>,<hostname.domain>,puppet,puppet.<domain>.

#### `q_puppetmaster_enterpriseconsole_hostname=pe-console.<your local domain>`

**String** --- The hostname of the server running the console component. Only needed if you are not installing the console component on the Puppet master server.

#### `q_puppetmaster_enterpriseconsole_port=443`

**Integer** --- The port on which to contact the console server. Only needed if you are not installing the console component on the Puppet master server.

#### `q_pe_check_for_updates=y`

**y** or **n**; **MUST BE LOWERCASE** --- Whether to check for updates whenever the `pe-puppetserver` service restarts. To get the correct update info, the server will pass some basic, anonymous info to Puppet Labs’ servers. Specifically, it will transmit:
   * the IP address of the client
   * the type and version of the client’s OS
   * the installed version of PE
   * the number of nodes licensed and the number of nodes used

If you wish to disable update checks (e.g. if your company policy forbids transmitting this information), you will need to set this to n. You can also disable checking after installation by editing the /etc/puppetlabs/installer/answers.install file.

#### `q_public_hostname=`

**String** --- A publicly accessible hostname where the console can be accessed if the host name resolves to a private interface (e.g., Amazon EC2). This is set automatically by the installer on EC2 nodes, but can be set manually in environments with multiple hostnames.

### Additional Puppet Master Answers

These answers are optional.

#### `q_tarball_server`

**String** --- The location from which PE agent tarballs will be downloaded before installation. Note that agent tarballs are only available for certain operating systems. For details, see the [PE agent installation instructions](./install_agents.html).

#### `q_exit_and_update_auth_conf=y`

**Y** or **N** --- (Upgrade only) Whether to accept the presence of a modified auth.conf file when upgrading. For details see [modified auth.conf files](./install_upgrading_notes.html#upgrading-to-38-with-a-modified-authconf-file).

#### `q_puppetmaster_r10k_remote='git@<your.git.server.com>:puppet/control.git'`

**String** --- The git url to be passed to the `r10k.yaml` file. This can be any URL that is supported by r10k (and normally git). This answer is OPTIONAL and only needed if you would like r10k configured when Puppet Enterprise is installed.

#### `q_puppetmaster_r10k_private_key=/root/.ssh/id_dsa`

**String** --- The local filesystem path on the Puppet master where the SSH private key can be found and used by r10k. This answer is OPTIONAL and only needed if you would like r10k configured when Puppet Enterprise is installed. This must be specified in conjunction with `q_puppetmaster_r10k_remote`.

#### `q_puppetmaster_code_manager_auto_configure`

**Y** or **No** --- (Install only) Whether or not to automatically configure the code manager service.

#### `q_puppetmaster_file_sync_service_enabled`

**Y** or **No** --- Whether or not to enable the file sync service.

>**Note**: See [Do Not Use 'n' for File Sync Question in Answer File To Disable File Sync On Install](./release_notes_known_issues_install.html#do-not-use-n-for-file-sync-question-in-answer-file-to-disable-file-sync-on-install) before adding this question to an answer file.

#### `q_puppetmaster_external_node_terminus`

**Y** or **N** --- Use an external node classifier. **Important**: Use of an external node classifier in PE is **neither supported nor tested**, and you will not be able to access classification-related features of PE, such as the node manager or RBAC service in PE console.

### PuppetDB Answers

#### `q_puppetdb_hostname=pe-puppetdb.<your local domain>`

**String** --- The hostname of the server running PuppetDB.

### Additional PuppetDB Answers
These answers are optional.

#### `q_puppetdb_plaintext_port`

**Integer** --- The port on which PuppetDB accepts plain-text HTTP connections (default port is 8080).

