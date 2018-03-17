## Prerequisites ##

1. Google Cloud Virtual Machine

1. Docker and docker-compose installed


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


## How to add new users with username password authentication##

1. Add user to users.conf 

```<username>:<password>:<sftp-uid>:<sftp-gid>:upload```

1. add a sub directory for that user in volume directory. Name of newly created directory should match username in users.conf file

```
cd sftp/volume
mkdir <username>
```

1. add volume for newly created user in docker-compose.yaml

```- ./volume/<username>:/home/<username>/upload```


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

1. add SSH key

Put public key to `<username>/.ssh/keys` dir. For more details see README.md


## Run sftp server ##

```
docker-compose up --build
```


## How to connect using username password##

```sftp testuser@<server-ip>

