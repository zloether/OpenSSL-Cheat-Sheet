# OpenSSL Cheat Sheet
Cheat sheet of useful commands for OpenSSL

## Certificates

Generate Private Key
```
openssl genrsa -out /path/to/www_server_com.key 2048
```
 

Decode Private Key
```
openssl rsa -text -in yourdomain.key -noout
```
 

Extract Public Key from Private Key
```
openssl rsa -in yourdomain.key -pubout -out yourdomain_public.key
```
 

Generate CSR from RSA private key
```
openssl req -new -sha256 -key private.key -out server.csr
```
 

Generate RSA private key and CSR all at once
```
openssl req -new -sha256 -newkey rsa:2048 -nodes -keyout private.key -out server.csr
```
 

Read contents of CSR
```
openssl req -in server.csr -noout -text
```
 

Extract private key from PFX
```
openssl pkcs12 -in bundle.pfx -nocerts -out private.key
```
 

Extract certificate from PFX
```
openssl pkcs12 -in bundle.pfx -nokeys -out public.pem
```
 

Remove passphrase from private key
```
openssl rsa -in private.key -out newPrivate.key
```
 

Add passphrase to private key
```
openssl rsa -des3 -in your.key -out your.encrypted.key
```
 

Convert DER to PEM
```
openssl x509 -inform der -in certificate .cer -out certificate.pem
```
 

Convert PEM to DER
```
openssl x509 -outform der -in certificate.pem -out certificate.cer
```
 

Create PFX from CER and KEY
```
openssl pkcs12 -export -in certificate.cer -inkey private.key -out certificate.pfx -certfile CACert.cer [-legacy]
```


Create Self Signed Certificate
```
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes
```


Create Certificate from CSR and KEY
```
openssl req -x509 -key private.key -in server.csr -out cert.pem -days 365 -nodes
```


Create certificate using CA
```
openssl x509 -req -days 360 -in server.csr -CA cacert.pem -CAkey cakey.pem -CAcreateserial -out server.crt -sha256
```

## Encryption
Encrypt a file
```
openssl enc -aes-256-cbc -pbkdf2 -base64 -in secrets.txt -out secrets.txt.enc
```


Decrypt a file
```
openssl enc -aes-256-cbc -d -pbkdf2 -base64 -in secrets.txt.enc -out secrets.txt
```


Generate Random Key for Encryption
```
openssl rand -hex -out key.bin 64
```


Encrypt a file using public key
```
openssl rsautl -encrypt -inkey publickey.pem -pubin -in key.bin -out key.bin.enc
```


Decrypt a file using a private key
```
openssl rsautl -decrypt -inkey private.key -in key.bin.enc -out key.bin
```


## Interact with Servers
Download entire certificate chain from remote server
```
openssl s_client -showcerts server:port
```


## OpenSSH
Convert RSA private key from OpenSSH to PEM format
```
ssh-keygen -p -m PEM -f ~/.ssh/id_rsa
```

