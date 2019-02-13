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

### Import Request

```
easyrsa import-req ../enterprise_mongo_server/pki/reqs/mongoserver.req mongoserver
```


