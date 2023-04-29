# openssl

* Read the contents of a certifiacte file

  ```bash
  openssl x509 -in something.com.cert.pem -text
  ```

* Create public private pair

  ```bash
  openssl genrsa -out private-key.pem 2048
  openssl rsa -in key.pem -outform PEM -pubout -out public.pem
  ```

* Create a self-signed certificate

  ```bash
  openssl req -new \
    -newkey rsa:4096 \
    -days 365 \
    -nodes -x509 \
    -subj /C=IL/CN=localhost \
    -keyout private-key.pem \
    -out self-signed.cert
  ```

* Create symetric key

  ```bash
  openssl rand -base64 32 > key.bin
  ```

* Encrypt using symetric key
  
  ```bash
  openssl enc \
    -aes-256-cbc \
    -salt \
    -in file_to_encrypt.txt \
    -out ecrypted_file.enc \
    -kfile ./key.bin
  ```

* Encrypt using public key

  ```bash
  openssl rsautl -encrypt \
    -inkey aharon.pub.pem \
    -pubin -in key.bin \
    -out key.bin.aharon.enc
  ```

* Decrypt using private key
  
  ```bash
  openssl rsautl -decrypt \
    -inkey priate-key.pem \
    -in filekey_encrypted.key \
    -out filekey.key
  ```

* Decrypt using symetric key
  
  ```bash
  openssl enc -d \
    -aes-256-cbc \
    -in kubeconfig_encrypted \
    -out kubeconfig \
    -kfile ./symetric-key.bin
  ```
