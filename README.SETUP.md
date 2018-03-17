## How to setup sftp ##

1. Create user

```sudo adduser sftp```

1. Add user to docker group

```sudo usermod -aG docker sftp```

1. Change user

```sudo su - sftp```

1. Go to user's home dir

```cd /home/sftp```

1. Git clone the repo

```git clone <repo-url>```

1. Proceed to "How to add users" step


## How to add new users ##

1. Add user to users.conf 

```<username>:<password>:<sftp-uid>:<sftp-gid>:upload```

1. add a sub directory for that user in volume directory. Name of newly created directory should match username in users.conf file

```
cd sftp/volume
mkdir <username>
```

1. add volume for newly created user in docker-compose.yaml

```- ./volume/<username>:/home/<username>/upload```


## Run sftp server ##

```
docker-compose up --build
```

