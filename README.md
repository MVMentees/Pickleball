# Pickleball project
Here is the first we hope of many projects for us to tackle with MV.

This works in conjunction with the universe-pickleball docker image and assumes the volume for that docker
is mounted on the host at /home/dockeradmin/PBD

## Quick Start
In your home directory, add this repo

  $ `git clone https://github.com/MVMentees/Pickleball.git`

Add your own branch

  $ `git branch -c *yourname*`

## Add DIR type files to the repo
You will notice that D_xxx files are in the repo.  These are DICT files which have been moved to the
repo and then symbolic linked from the docker volume.   There is also the PB.BP file which is the 
DIR type file used to store the Pickleball program source.  It to is symbolic linked from the repo.

The files exist here in the repo, but in the docker volume they have this type of a link
```text
 PB.BP -> /home/dockeradmin/Pickleball/PB.BP
```

This is achieved by first creating the file in the docker, then moving the file to the repo,
then setting the symbolic link in its place

### Source code files

From UniVerse you can create the file
```
ICREATE.FILE NEWBP 19
```
Then on the host volume in Linux move it and create a symbolic link in it's place

```
mv /home/dockeradmin/PBD/PICKLE/PB.BP /home/dockeradmin/Pickleball/PB.BP
ln -s /home/dockeradmin/Pickle/PB.BP /home/dockeradmin/PBD/PICKLE/PB.BP
```
When this is done, the repo will keep all the source and the docker will simply point to that source.

### DICT files

From UniVerse you create the data file
```
ICREATE.FILE LOCATIONS 3 16 59
```
Then on the host put the DICT \(D_filename\) in the repo as a DIR file and replace the hash file on the docker volume with a symbolic link

```
mkdir -m777 /home/dockeradmin/Pickle/D_LOCATION
rm /home/dockeradmin/PBD/PICKLE/D_LOCATION
ln -s /home/dockeradmin/Pickle/D_LOCATION /home/dockeradmin/PBD/PICKLE/D_LOCATION
```
When this is done, the repo will keep all the DICT items and the docker will simply point to those items.
