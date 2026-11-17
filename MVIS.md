# MVIS - Multi-value Information server

This is the layer between web based programs and the UniVerse database.   We will put this on the same Linux box as we have the universe-pickleball docker and Pickleball git repo

## Download and install the MVIS server

The MVIS server is free for Universe and can be retrieved from the download site with wget from the Linux command line.  This process will download and install the mvis server

```
cd ~/Downloads
wget https://rbc.rocketsoftware.com/downloads/software/MVIS_2.3.3.zip
unzip MVIS_2.3.3.zip
cd mvisPkg/
chmod +x mvis_install.sh
sudo ./mvis_install.sh install
```

## Install script 

* Do you agree with these statements (y/N)?  **Y**
* Enter the MultiValue Integration Server installation path or press [Enter] for /opt/cm: **Enter**
* If you want to use cloud services please enter 'AZURE', 'AWS' or press [Enter] for non-cloud mode: **Enter**
* Type in the correct option to proceed [local or MVServer]:  **MVServer**
* Would you like to start MultiValue Integration Server Admin? (Y/n) **Y**
* Press any key... **Enter**

## Start and test the MVIS Server

From a browser that can access the host go to the host address port 7077

`http://192.168.56.2:7077`

Login as **admin** with password of **admin**

## Add PICKLE as a new Account

Configuration >> Accounts **+Add Account**
| Prompt | Entry|
|----------------|------------|
| Account Name : | Pickleball |
| MV Server Name: | 192.168.56.2|
| MV Server Port: | 31501|
| Account Path: | /mystuff/PICKLE|
| Connection String : | uvcs|
|User ID: | user1|
| User Password: | user1|

Click on **[Test Connection]** and it should be successful

## Define the API metadata

Go to the **[API Information]** tab

| Prompt | Entry|
|----------------|------------|
| API Name: | pickleball_API|
| API Title: | API for Pickleball scheduling|
| Version : | 1.0|
 
Click on **[OK]**

It will prompt "The changes will be applied after restarting account. Would you like to restart 'Pickleball' account?".

Click **[Yes]**

## Change the MVISDEFN account to be in mystuff

1. Log into the docker as root with password root

   `telnet localhost 2301`

2. Move the /usr/uv/MVISDEFN account from /usr/uv to /mystuff

   `mv /usr/uv/MVISDEFN /mystuff/.`

3. Update the UV.ACCOUNT item

   ```
   cd /usr/uv
   /usr/uv/bin/uv
   AE UV.ACCOUNT MVISDEFN
   0011 /usr/uv/MVISDEFN
   .C;/usr/uv;/mystuff
   .FI
   ```

4. Exit the docker and change the /opt/cm/servers.yaml file

   ```
   vi /opt/cm/servers.yaml

   Change the /usr/uv/MVISDEFN to /mystuff/MVISDEFN
   ```

5. Reboot the Rocky 9 virtual machine and restart the docker and MVIS server

   ```
   sudo shutdown -r now

   When it reboots...

   docker compose -f ./universe-pickleball.yaml up -d
   cd /opt/cm
   sudo ./start-cm.sh
   sudo ./start-admin.sh
   ```
   
## Configure REST server

REST Server >> Accounts

Click **<** to expand **Pickleball**

Click **<** to expand **Subroutine Resources**

Click **+Add Subroutine**

