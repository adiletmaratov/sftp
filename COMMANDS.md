## Commands ##


```
docker run -p 2222:22 -v /etc/ssh/ssh_host_rsa_key:/etc/ssh/ssh_host_rsa_key -v /etc/ssh/ssh_host_ed25519_key:/etc/ssh/ssh_host_ed25519_key -v $(pwd)/users.conf:/etc/sftp/users.conf:ro -v $(pwd)/volume:/home --user 213000036 sftp
```


```
docker run -p 2222:22 -d -v $(pwd)/users.conf:/etc/sftp/users.conf:ro -v $(pwd)/volume:/home atmoz/sftp
```


```
put /home/amaratov/projects/rxwiki/sftp/README.md .
```



## How to add users ##

1. add it to users.conf
2. add a sub directory for that user in volume directory. Name of newly created directory should match username in users.conf file
