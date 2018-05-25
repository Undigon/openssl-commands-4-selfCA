# The last steps
If your rootCA.pem or rootCA.key were given the `chmod a-rwx` treatment, you'll need to be root or use sudo.
## Sign it!
### On multiple lines

```shell-script
sudo openssl x509 -req \
-in /path/to/server.csr \
-extfile /path/to/server.cnf \	#Copy this from openssl.cnf (/etc/ssl/openssl.cnf) and modify it.
-extensions v3_req \ 		#This is inside server.cnf under [ v3_req ].
-CA /path/leading-to/rootCA.pem \
-CAKey /path/leading-to/rootCA.key \
-CAcreateserial \
-out /path/to/server.crt \	#You can provide an absolute or relative path I think.
-days 366 \			#Don't choose more days than rootCA's validity.
-sha256				#Or any other provided it is not SHA1, it's being phased out.
```
### Everything in a single line.
```shell-script
sudo openssl x509 -req -in /path/to/server.csr -extfile /path/to/server.cnf -extensions v3_req -CA /path/leading-to/rootCA.pem -CAkey /path/leading-to/rootCA.key -CAcreateserial -out server.crt -days 366 -sha256
```
## Verify it!
If everything went smoothly you should be able to verify that it contains everything you asked, including the *SAN*. 
```shell-script
openssl x509 -text -noout -in /path/to/server.crt
```
## True last step
Congratulations, you can modify your `/etc/apache2/sites-enabled/default-ssl.conf` and/or restart your server with `service apache2 restart`.
