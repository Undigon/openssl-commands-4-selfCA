# server.csr
### Request a signature!
```shell-script
openssl req -new -nodes -keyout server.key -out server.csr -config server.cnf
```
### Verify it!
Check that it says everything you need it to say \[Points of interest: Common Name (CN) and Aliases (X509V3)\]
```shell-script
openssl req -text -noout -verify -in server.csr
```
