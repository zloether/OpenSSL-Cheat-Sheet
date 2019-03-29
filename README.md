# OpenSSL Cheat Sheet
Cheat sheet of useful commands for OpenSSL



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
openssl pkcs12 -export -in certificate.cer -inkey private.key -out certificate.pfx -certfile CACert.cer
```
