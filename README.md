# Ansible to configure server for .Net Core 3.1 runtime and Microsoft SQL Server

### Project description

This project using ansbile, for configure **linux servers** to install nessesary packages to hosts .net core runtime on version 3.1 and Microsoft SQL Server. 
Script have division on separate server to .net runtime and MSSQL server. The scripts support the configuration of more servers on each element. Both elements have groups in inventory file.

### Pre-requisites
* local machine must have installed packages:
    *  ansilbe
    *  python-3
* remote machine must have installed packages:
    * python-3

### To-Do tasks before run script first time:


1. Go to inventory file and bellow "dotnetServers" grups add server(s) when .net core runtime must be installed. Declare server using pattern: 
    ``` shell
        friendly_name ansible_host=IpServer
    ```
    example:
    ``` shell
        DotNetServerInPoznan ansible_host=192.168.1.29
    ```
2. Using the above description, also add servers for the group  "databaseServers".
3. Below servers lists is configuration to connect to group server(s). In this section to:  
    ```ssh
        ansible_user=
        ansible_ssh_private_key_file=
    ```
    add correctly params, where ***ansible_user*** is  user to connect on remote server. ***ansible_ssh_private_key_file*** is path to id_rsa.pub file on local machine. ex.:
    ```ssh
        ansible_user=admin
        ansible_ssh_private_key_file=/home/mateusz/.ssh/id_rsa.pub
    ```

4. Create a vault file, and named him `vault.yaml`. To create this file use command:
	```sh
	ansible-vault create vault.yml
	```
    After set main password to this file, using below template to fill this file.
    ```yaml
    # vault file template
    sa_password: 'some password'
    ```
### Run
1. When all the above points is done, run ansible script using command:

    ```sh
	ansible-playbook -i inventory run.yaml --ask-vault-pass --ask-become-pass
    ```