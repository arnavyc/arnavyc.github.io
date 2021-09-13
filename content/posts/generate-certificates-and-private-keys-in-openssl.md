---
author: "arnavyc"
title: "Generate Certificates and Private Keys in OpenSSL"
description: "This post shows how to generate certificates and private keys in OpenSSL"
categories:
- OpenSSL
- Shell
date: 2021-09-13T09:59:37+05:30
draft: false
---

This post shows how to generate certificates and private keys in OpenSSL.

# Installation

Install OpenSSL command line tools, using your favorite package manager.

## For Arch Linux

```sh
$ sudo pacman -S openssl
```

# Key Generation

## RSA Keys

To generate RSA private keys, run the following command:

```sh
$ openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:<num_bits> -out privkey.pem
```

replacing `<num_bits>` with number of bits you want for RSA key. Example: `2048` for a `RSA 2048` key.

To generate a self-signed certificate, run the following command:

```sh
$ openssl req -new -x509 -days <days> -key privkey.pem -out pubkey.pem
```

replacing `<days>` with desired number of days after which the certificate expires.

To generate a certificate request, run:

```sh
$ openssl req -new -sha256 -key privkey.pem -out pubkey.csr.pem
```

You can also generate both RSA private key and certificate request (or self-signed certificate) by running the following command: 

```sh
$ openssl req -new -sha256 -newkey rsa:4096 -keyout privkey.pem -out pubkey.csr.pem
```

Replacing `'-sha256'` with `'-x509 -days <days>'` and `pubkey.csr.pem` with `pubkey.pem`, where `<days>` is number of days for which certificate is valid, to generate a self-signed certificate. 

## NIST curves

To generate private keys with NIST curves, run the command: 

```sh
$ openssl genpkey -algorithm EC -pkeyopt ec_paramgen_curve:<NIST name> -pkeyopt ec_param_enc:named_curve -out privkey.pem
```

Replacing `<NIST name>` for `'P-256'`, `'P-384'` or `'P-521'` \(without quotes\) for generating `P-256`, `P-384` or `P-521` private key respectively. 

To generate a self-signed certificate, run the command: 

```sh
$ openssl req -new -x509 -days <days> -key privkey.pem -out pubkey.pem
```

Replacing `<days>` for number of days for which certificate is valid. 

To generate a certificate request, run the command: 

```sh
$ openssl req -new -sha256 -key privkey.pem -out pubkey.pem
```

# After Generation

You should make the private key read-only and prevent read access to other users. For that, run the command: 

```sh
$ chmod 400 privkey.pem
```

For the certificate, you do not need to prevent read access to other users. However, you would want to make it read-only. For that, run the command: 

```sh
$ # (or pubkey.csr.pem if you generated a certificate request)
$ chmod 444 pubkey.pem
```

