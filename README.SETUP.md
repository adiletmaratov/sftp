## Prerequisites ##

1. Google Cloud Virtual Machine

1. Docker and docker-compose installed

1. Read README.md


## How to setup sftp ##

1. Create a unix user

```sudo adduser sftp```

1. Add the user to docker group

```sudo usermod -aG docker sftp```

1. Change user

```sudo su - sftp```

1. Go to user's home dir

```cd /home/sftp```

1. Git clone the repo

```git clone <repo-url>```

1. Proceed to "How to add users" step


## Using Google Cloud Persistence Disk ##

In order to attach a persistent disk, follow this documentation https://cloud.google.com/compute/docs/disks/add-persistent-disk

Mount newly created disk to /home/sftp/sftp/volume directory so that all files in there are written to the disk.

After the disk is mounted, go ahead and make sftp user the owner of everything inside of /home/sftp/sftp/volume

```
sudo chown sftp *
```

## How to add users ##

1. Get sftp user and group ids `id -u sftp` and `id -g sftp`

1. Add user to users.conf 

```<username>:<password>:<sftp-uid>:<sftp-gid>:upload```

1. add a sub directory for that user in volume directory. Name of newly created directory should match username in users.conf file

```
cd sftp/volume
mkdir <username>
```

1. add volume for newly created user in docker-compose.yaml

```- ./volume/<username>:/home/<username>/upload```

Why should I mount a new volume for every user? https://askubuntu.com/questions/134425/how-can-i-chroot-sftp-only-ssh-users-into-their-homes


## How to add new users with SSH authentication ##

1. Add user to users.conf

```<username>:<sftp-uid>:<sftp-gid>:upload```

1. add a sub directory for that user in volume directory. Name of newly created directory should match username in users.conf file

```
cd sftp/volume
mkdir <username>
```

1. add volume for newly created user in docker-compose.yaml

```- ./volume/<username>:/home/<username>/upload```

Why should I mount a new volume for every user? https://askubuntu.com/questions/134425/how-can-i-chroot-sftp-only-ssh-users-into-their-homes

1. add SSH key

Put public key to `<username>/.ssh/keys` dir. For more details see README.md


## Run sftp server ##

Go to `volume` dir and run command 

```chmod 775 * ```

```
docker-compose up --build
```

Go to `volume` dir and run command 

```chmod 311 * ```

this will restrict users to read and make all directories write and excecute only.

## How to connect ##

To connect to sftp server run: 

```
sftp testuser@<server-ip>
```

Now you can use command to send files:

```
put /some/absolue/path/on/host upload/
```

