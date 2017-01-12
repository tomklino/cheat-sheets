# Cryptography frequently useful commands

* read .crt files

```bash
openssl x509 -in /path/to/some.crt -text -noout
```

* view the certificate served by server

```bash
openssl s_client -showcerts -connect google.com:443
```
