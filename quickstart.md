# Quick start for working with this project

## Create a VirtualBox Linux virtual to run docker

The Howto explains step by step how to create a Rocky 9 virtual machine that will allow you to run this and other docker images


[VirtualBox_howto.md](https://github.com/MVMentees/Gitting-started)

## Stage the box

This Howto explains how to stage the new Rocky 9 box with the needed packages and settings and how to setup the github ssh key authentication

[Stage_Box_howto.md](https://github.com/MVMentees/Gitting-started)

## Request and download the UniVerse database TE Edition

If you do not already have the UVTE version, request a download 

[Request download](https://www.rocketsoftware.com/en-us/products/multivalue/universe/linux-free-trial)


You will receive an email with the download link.  You will need to add that downloaded UVTE zip file to the project docker image directory in order for the docker to build the project image

## Get the project docker build from the MVMentees hub

Load the zip for the project you want to start
`
In this case the build_universe-pickleball.zip

1. In your home directory, access the docker from github
   
   ```
   cd ~
   wget -O build_universe-pickleball.zip \
   https://raw.githubusercontent.com/MVMentees/MV-Dockers/main/build_universe-pickleball.zip
   ```
   
2. Create a docker directory and unzip the build
   
    ```
    mkdir -m777 ~/pbdocker
    cd ~/pbdocker
    unzip ~/build_universe-pickleball.zip
    ```


3. Add the UVTE from the download above
   
    ```
    cd ~/pbdocker
    cp ~/Downloads/UVTE_LINUXX86_14.2.1.zip .
    ```

## Clone the github for the new project

1. Run the got clone command
   
    ```
    cd ~
    git clone git@github.com:MVMentees/Pickleball.git
    ```
   
2. Add your own Branch \(In this case "danell'\)
   
    ```
    cd ~/Pickleball
    git switch main
    git pull
    git switch -c danell
    git push -u origin danell
    ```


## Setup the docker to work with the git repo

1. Add dshare group as group number 150000

    `sudo groupadd -g 150000 dshare`

2. Add dshare group to the user on host

    `sudo usermod -aG dshare dockeradmin`

3. Change the group of the repo to dshare

    `sudo chgrp -R dshare ~/Pickleball`

4. Change permissions to 775 for repo
    
    `sudo chmod -R 2775 ~/Pickleball`

## Add dshare group to docker and docker users

```
vi ~/pbdocker/add_users_groups
<Shift>G  <Shift>A  <Enter>         will add to the bottom
:dshare:50001
user1:dshare
user2:dshare
user3:dshare
<Esc> :wq                           will write the item
 ```

## Add Volume for repo to docker compose yaml

```
vi ~/pbdocker/universe-pickleball.yaml
<Shift>G  <Shift>A  <Enter>         will add to the bottom
- ~/Pickleball:/home/dockeradmin/Pickleball:z
<Esc> :wq                           will write the item
```

## Run the docker compose yaml to start the machine

```
cd ~/pbdocker
docker compose -f ./universe-pickleball.yaml up -d
```

## Telnet to the machine and login as user1 with password user1

`telnet localhost 2301`

## Setup the repo

1. Create a PB.BP file 

    `ICREATE.FILE PB.BP 19`

2. Add it to the repo with REPO

    ```
    REPO PB.BP
    File found... DATA level = PB.BP, DICT level = D_PB.BP
    This is a DIR type file to move to repo

    Enter repo directory : /home/dockeradmin/Pickleball
    ```

3. Do the same for all the other files in the repo 

    ```
    ICREATE.FILE COURT 3 7 8
    REPO COURT
    ICREATE.FILE LOCATION 3 7 8
    REPO LOCATION
    ICREATE.FILE MEMBER 3 101 8
    REPO MEMBER
    ICREATE.FILE RESERVATION 3 503 8
    REPO RESERVATION
    ```

4. BASIC and CATALOG the PB.BP file

    ```
    BASIC PB.BP *
    CATALOG PB.BP *
    ```

5. Add or alter a few VOC items

    ```
    AE VOC LOGIN
    0001: PA
    0002: DOCKERLOGIN
    0003: PBLOGIN

    AE VOC LS
    001: PA
    002: SH -c "ls -l"

    AE VOC LSREPO
    001: PA
    002: SH -c "ls /home/dockeradmin/Pickleball -l"
    ```

6. Load the MVIS server to allow for web development

    Exit the docker by typing **quit** at ECL

    Then, use the MVIS.md document to guide you on the installation
    
    [See here for details](https://github.com/MVMentees/Pickleball/blob/main/MVIS.md)
