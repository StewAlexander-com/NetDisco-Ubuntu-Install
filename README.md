# NetDisco-Ubuntu-Install
Clearer instructions on how to load NetDisco on an Ubuntu server
## Install Instructions
1. Install an Ubuntu system (vm, kvm, using a live ISO, Virtualbox, etc)
2. Run `$sudo apt-get update`, `$sudo apt-get upgrade`, `sudo apt-get dist-upgrade` on the Ubuntu system
3. Reboot the system with `$sudo shutdown -r now`
4. Install **Cockpit, Cockpit-Docker, Cockpit-ws and Cockpit-packagekit** (using the sudo apt-get install command)
5. If docker is not yet installed, install it (using sudo apt-get install)
6. Pull / install the latest docker image from https://hub.docker.com/r/netdisco/netdisco  
* You May have to look at the tags, for a recent install I needed to use `$sudo docker pull netdisco/netdisco:latest-do`
7. Download docker-compose using `$sudo apt-get install docker-compose`
8. Run commands listed in the NetDisco Dockerhub site: https://hub.docker.com/r/netdisco/netdisco
```
$sudo groupadd netdisco -g 901
$sudo useradd -u 901 -p x -g netdisco netdisco
$mkdir -p netdisco/{logs,config,nd-site-local}
$sudo chown -R netdisco:netdisco netdisco
```
and ...
```
 $sudo curl -Ls -o docker-compose.yml https://tinyurl.com/nd2-dockercompose
 $docker-compose up  
 ```
 **_Be sure to use "sudo" first on the curl and docker-compose commands (i.e. $sudo curl -Ls -o ...)_ in Ubuntu, unless logged in as root**  

9. If the "docker-compose" command is successful NetDisco should be up  
10. Once installed go to: **_<IP_ADD>:9090/system_** for the Cockpit management console, and **_<IP_ADD>/#_** for NetDisco (where <IP_ADD> is the IP address for the Ubuntu server)  
11. Go to the NetDisco website, then go to the menu **Admin -> User Management**  
12. Create users / passwords, be sure to click the save button (at the right, looks like an an old style disk icon, refresh the page to make sure), and add a password to the guest account (click save again of course, **_do not delete "guest" yet_** )  
13. Open a connection to the NetDisco server, and edit the deployment.yml file (using nano or vi) located here:  
`/home/support/netdisco/config`
14. Change `no_auth: true` to `no_auth: false` in the **_deployment.yml file_**
15. Stop the docker containers (multiple ways to do this, one way is to use the Cockpit Management GUI)
16. From the server command line go to
`/home/support`
17. Issue the command `$sudo docker-compose up -d` (_the "d" flag runs the command in the background_), if everything goes well NetDisco should be back up
18. If NetDisco does not request a login, but instead takes you to the guest account, go to the user name menu on the right, and select "Log Out"  
19. Login as one of the accounts that were created in step **#12**, go to **Admin -> User Management** (as above), and delete the **guest** account
## Initial Setup
- Log in to NetDsico, go to the **Admin** menu and click all of the following one at a time
```
Discover All
Arpnip All
Macsuck All
NBTstat ALL
Run Expire Job
Update Statistics
```
- Then go to **Admin -> Job Queue** to watch the status of all the jobs, when done setup should be complete
