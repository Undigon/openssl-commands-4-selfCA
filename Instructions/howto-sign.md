#Trying to break it on multiple lines. If your rootCA.pem or rootCA.key were given the "chmod a-rwx" treatment, you'll need to be root or use sudo.
sudo openssl x509 -req \
-in /path/to/server.csr \
-extfile /path/to/server.cnf \	#Copy this from openssl.cnf (/etc/ssl/openssl.cnf) and modify it as explained before.
-extensions v3_req \ 		#This is inside device.cnf under [ v3_req ].
-CA /path/leading-to/rootCA.pem \
-CAKey /path/leading-to/rootCA.key \
-CAcreateserial \
-out /path/to/server.crt \	#You can provide an absolute or relative path I think.
-days 366 \			#As many as you see fit, as long as it's less than the validity of the root certificate.
-sha256				#Or any other provided it is not SHA1, it's being phased out.

#Everything in a single line.
sudo openssl x509 -req -in /path/to/server.csr -extfile /path/to/server.cnf -extensions v3_req -CA /path/leading-to/rootCA.pem -CAkey /path/leading-to/rootCA.key -CAcreateserial -out server.crt -days 366 -sha256
