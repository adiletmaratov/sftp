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

