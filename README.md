# snippets

Generate SSH key

```
openssl genrsa -des3 -out client.key.pem 4096
```

Generate CSR

```
openssl req -new -sha256 -key client.key.pem -out client.csr.pem
```
