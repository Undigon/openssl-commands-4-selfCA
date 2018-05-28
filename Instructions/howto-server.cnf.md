# server.cnf
## About this file
This file contains instructions for openssl about what is needed, how to achieve it and some default options.
This file will contain non-sensitive but specific information that will go inside the *SAN* field of the certificate.
Because of this specificity I find it convenient to keep this file in the same folder as the future certificate sign requests of a specific server.

## How to get it
The template for this file is at the ssl folder. All you need to do is `cp /etc/ssl/openssl.cnf /path/to/server.cnf`

## What to do with it
You need to modify it to suit your needs.
First, a general modification: You need to uncomment or add a line. In my file that is

**line 125** `req_extensions = v3_req`

Second, you need to edit [ v3_req ] around **line 217**. It must read

```
[ v3_req ]

basicConstraints = CA:FALSE
keyUsage = nonRepudiation, digitalSignature, keyEncipherment
subjectAltName = @alt_names
```

And immediately below that

```
[ alt_names ]
IP.1 = #You can designate IP addresses if you need to. e.g. 127.0.0.1
IP.2 = #You need to designate one address per line. Try to keep it below 100.
IP...[etcetera]
DNS.1 = #DNS is another option. You can designate addresses like localhost or www.mysite.com
```
That should be everything you need. Everything else gets managed by the csr.
