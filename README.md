## Overview

Certificate Authority setup for playing with Enterprise Mongo

Using [Easy-RSA](https://github.com/OpenVPN/easy-rsa.git)

## Setup

Ran the following

```
easyrsa init-pki
```

### CA

```
easyrsa build-ca

Using SSL: openssl OpenSSL 1.1.0g  2 Nov 2017

Enter New CA Key Passphrase: 
Re-Enter New CA Key Passphrase: 
Generating RSA private key, 2048 bit long modulus
.....................................................+++
.....................................+++
e is 65537 (0x010001)
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Common Name (eg: your user, host, or server name) [Easy-RSA CA]:mongoadmin

CA creation complete and you may now import and sign cert requests.
Your new CA certificate file for publishing is at:
/home/fiona/wd/dwp/cis/enterprise_mongo_ca/pki/ca.crt
```

Remove the passphrase on the key (so that this project can be shared)

```
openssl rsa -in ca.key -out ca-unenc.key
``` 


### Import Request

```
easyrsa import-req ../enterprise_mongo_server/pki/reqs/mongoserver.req mongoserver
```

### Sign Request 

Signing this as a server certificate

```
easyrsa sign-req server mongoserver

Using SSL: openssl OpenSSL 1.1.0g  2 Nov 2017


You are about to sign the following certificate.
Please check over the details shown below for accuracy. Note that this request
has not been cryptographically verified. Please be sure it came from a trusted
source or that you have verified the request checksum with the sender.

Request subject, to be signed as a server certificate for 1080 days:

subject=
    commonName                = mongoserver


Type the word 'yes' to continue, or any other input to abort.
  Confirm request details: yes
Using configuration from /home/fiona/wd/dwp/cis/enterprise_mongo_ca/pki/safessl-easyrsa.cnf
Enter pass phrase for /home/fiona/wd/dwp/cis/enterprise_mongo_ca/pki/private/ca.key:
Can't open /home/fiona/wd/dwp/cis/enterprise_mongo_ca/pki/index.txt.attr for reading, No such file or directory
140712957637056:error:02001002:system library:fopen:No such file or directory:../crypto/bio/bss_file.c:74:fopen('/home/fiona/wd/dwp/cis/enterprise_mongo_ca/pki/index.txt.attr','r')
140712957637056:error:2006D080:BIO routines:BIO_new_file:no such file:../crypto/bio/bss_file.c:81:
Check that the request matches the signature
Signature ok
The Subject's Distinguished Name is as follows
commonName            :ASN.1 12:'mongoserver'
Certificate is to be certified until Jan 28 15:52:44 2022 GMT (1080 days)

Write out database with 1 new entries
Data Base Updated

Certificate created at: /home/fiona/wd/dwp/cis/enterprise_mongo_ca/pki/issued/mongoserver.crt
```


