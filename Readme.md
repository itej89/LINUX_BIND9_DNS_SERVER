# This repository contains docker compose configuration to create a DNS server in ubuntu 22.04

## Steps to start your own DNS server

1.  Clone the repository
2. cd into the DNS directory
3. Change Subnet in  " ./config/named.conf "
    <br>
    10.104.59.0/24; to your router's subnet
4. Change IP Address in  " ./config/named.conf "
    <br>
    10.104.59.0/24; to your host machine's IP Address
5. Change IP Address in " ./config/fouriermachines-com.zone " to your host PC IP address

6. Run ' docker compose up '. First time you will get an error saying 
    <br>
    ```
    53 address already in use
    ```
    But, this allows the host PC to download the docker image image from the docker repository

## Disable host's 53 port usage to allow bind-docker to establish connection
1. Open " resolved.conf "
    ```
    sudo gedit  /etc/systemd/resolved.conf 
    ```
2. Uncomment the line "DNSStubListener=yes" and modify it to "no"
    ```
    DNSStubListener=no
    ```
3. Restart systemd-resolved service
    ```
    sudo systemctl restart systemd-resolved
    ```
4. Run " docker compose up " again

5. This time you should see a success message