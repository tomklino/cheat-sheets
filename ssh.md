# ssh

* Generating ssh RSA key

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

* SCP syntax

```bash
scp -P<ssh port> <file on local machine> <username>@<server_ip>:/path/to/destination/filename
```

* An example ssh config entry

```
Host mymachine
  HostName 18.232.105.73
  ForwardAgent yes
  IdentityFile ~/.ssh/id_rsa
  User root
```
