# snippets

## OpenSSL

Generate SSH key
_Note: You may want to omit the -aes256 option to create a key without a password_

```
$ openssl genrsa -aes256 -out client.key.pem 4096
$ chmod 400 client.key.pem
```

Generate CSR

```
$ openssl req -key client.key.pem -new -sha256 -out client.csr.pem
```

Sign a CSR
_Note: If the certificate is going to be used for user authentication, use the usr_cert extension_

```
$ openssl ca -extensions server_cert -days 375 -notext -md sha256 \
-in client.csr.pem \
-out client.cert.pem
$ chmod 444 intermediate/certs/www.example.com.cert.pem
```

Verify a certificate has a valid chain of trust

```
openssl verify -CAfile ca-chain.cert.pem client.cert.pem
```
