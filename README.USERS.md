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
