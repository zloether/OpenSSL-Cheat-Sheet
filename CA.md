# Certification Authority
Generating certificates from a self-signed CA

## Create the CA key and certificate

Generate CA Private Key
```
openssl genrsa -out ca.key 4096
```

Create CA Certificate
```
openssl req -x509 -new -nodes -key ca.key -sha256 -days 365 -config self_signed_ca.conf -out ca.pem
```


## Issue Certificates Signed by CA

Generate RSA private key and CSR all at once
```
openssl req -new -sha256 -newkey rsa:2048 -nodes -keyout private.key -out server.csr
```

Create certificate using CA
```
openssl x509 -req -days 360 -in server.csr -CA ca.pem -CAkey ca.key -CAcreateserial -out server.crt -sha256
```