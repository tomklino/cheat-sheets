# openssl

* read the contents of a certifiacte file
```bash
openssl x509 -in something.com.cert.pem -text
```

* Create public private pair
```bash
openssl genrsa -out key.pem 2048
openssl rsa -in key.pem -outform PEM -pubout -out public.pem
```

* Create symetric key
```bash
openssl rand -base64 32 > key.bin
```

* Encrypt using symetric key
```bash
openssl enc -aes-256-cbc -salt -in file_to_encrypt.txt -out ecrypted_file.enc -kfile ./key.bin
```

* Encrypt using public key
```bash
openssl rsautl -encrypt -inkey aharon.pub.pem -pubin -in key.bin -out key.bin.aharon.enc
```
