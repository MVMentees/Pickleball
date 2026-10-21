# Pickleball project
Here is the first we hope of many projects for us to tackle with MV.

This works in conjunction with the universe-pickleball docker image and assumes the volume for that docker
is mounted on the host at /home/dockeradmin/PBD

## Quick Start
In your home directory, add this repo

`git clone https://github.com/MVMentees/Pickleball.git`

Add your own branch

```
cd ~/Pickleball
git branch -c *yourname*
```

## To work with docker
In order for this repo (and others) to work with docker, you will need to change the group to a group that is available from docker.  

The docker groups are offset by 99999, so a group called dshare needs to be created on the host as 150000 and on the docker as 50001

150000 - 99999 = 50001

This is accomplished with 5 steps

  1. Add the group dshare to the host as 150000
     
     `sudo groupadd -g 150000 dshare`
  
  2. Add that share to your user on the host

     `sudo usermod -aG dshare dockeradmin`
  
  3. Change the group of this repo to dshare

     `sudo chgrp -R dshare ~/Pickleball` 
  
  4. In the project docker add the group and add that group to user1, user2 and user3
  
     ```
     vi add_users_groups  (add these lines to the bottom)

     :dshare:50001
     user1:dshare
     user2:dshare
     user3:dshare
     ```
   
   5. In the yaml file for the project docker add this github repo directory
    
      ```
      vi universe-pickleball.yaml  (add this to the end in the volume area)

      - ~/Pickleball:/home/dockeradmin/Pickleball
      ```

