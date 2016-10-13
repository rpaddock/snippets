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
$ openssl ca -extensions server_cert -days 375 -notext -md sha256 -in client.csr.pem -out client.cert.pem
$ chmod 444 client.cert.pem
```

Verify a certificate has a valid chain of trust

```
openssl verify -CAfile ca-chain.cert.pem client.cert.pem
```

## nginx

SSL Options

```
ssl_certificate           /etc/nginx/cert.crt;
ssl_certificate_key       /etc/nginx/cert.key;

ssl on;
ssl_session_cache  builtin:1000  shared:SSL:10m;
ssl_protocols  TLSv1 TLSv1.1 TLSv1.2;
ssl_ciphers 'EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH';
ssl_prefer_server_ciphers on;
```
