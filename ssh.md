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
  HostName 10.0.0.1
  ForwardAgent yes
  IdentityFile ~/.ssh/id_rsa
  User root
```

* Port forwarding with ssh - bind local port 8000 to port 9000 on the remote machine

```bash
ssh -L 8000:127.0.0.1:9000 remote.machine.ssh
```
