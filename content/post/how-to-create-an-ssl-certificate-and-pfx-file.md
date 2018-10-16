---
title: "How to create an SSL certificate and PFX file"
date: 2018-10-16T15:27:05+01:00
author: "Nick Kirby"
url: "/how-to-create-an-ssl-cert-and-pfx-file/"
image: ""
description: Find out how to create an SSL certificate and PFX file needed for uploading it to an Azure App Service. 
tags: ['security', 'azure']
draft: false
---

As a .NET web developer, from time to time I have to create an SSL certificate and bind it to an Azure App Service. 

Whilst the steps aren't complicated, I do this kind of thing so infrequently that every time I do it feels like I'm doing it for the first time and it takes me way longer than it should. 

This blog post is to help me next time I need to do this, hopefully it will help you too! 

> The steps in this blog post are for Windows users but other platforms will be similar 

### The steps involved

1. <a href="#1">Create a CSR and private key</a>
2. <a href="#2">Generate an SSL certificate</a>
3. <a href="#3">Generate a PFX file</a>

### Prerequisites 

- Some command line knowledge
- Install [OpenSSL](https://www.cloudinsidr.com/content/how-to-install-the-most-recent-version-of-openssl-on-windows-10-in-64-bit/) to a location such as `C:/OpenSSL`


## 1. <span id="1">Create a CSR and private key</span>

Create a Certificate Signing Request ([CSR](https://en.wikipedia.org/wiki/Certificate_signing_request)) using the online tool [csrgenerator.com](https://csrgenerator.com/). Fill out the required fields and click **Generate CSR** to generate a CSR and private key.

Copy the *"BEGIN CERTIFICATE REQUEST"* section (like below) and paste it to a file such as `signing-request.csr` to the location where you installed OpenSSL.

```
-----BEGIN CERTIFICATE REQUEST-----
MIICyTCCAbECAQAwgYMxCzAJBgNVBAYTAkdCMRgwFgYDVQQDDA9kaWFyeW9mYWRl
di5uZXQxEzARBgNVBAcMClNocmV3c2J1cnkxFzAVBgNVBAoMDkRpYXJ5IG9mIGEg
RGV2MRMwEQYDVQQIDApTaHJvcHNoaXJlMRcwFQYDVQQLDA5EaWFyeSBvZiBhIERl
djCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBALGKRRYMK/ychGjwOLjs
42FODnCZcsSHR7OLRtk8BdCtV6JhznJx/OX0xc40x2QxCofANgisbiOayvWfNya/
Qrfep6Nee/ahMvzDO9f2Qj87AQ80qmF9hh5VbS1te6h49YfS1ab4AOcDAZEfWR7o
9XrBbclyp2Z+Rd+KE19lZrVQRLQloZALYi44+S8DFNxe6dU5u2Us4YptNoymappH
ZN4xSn9pEWMxSKuO/ysdtWu5cCZWpPHNh3g3QTxGyLW4UKmkBhFO/Y502qOtEdV+
EpWyTUjbiwdZCenfkvtS6ycKF4YwoNlx/Ap7vKtheSmN9tNdesG4B+R8Hegv/u7C
w0UCAwEAAaAAMA0GCSqGSIb3DQEBCwUAA4IBAQCXYoAs3vwJ8Op0EgJpbLjibl1H
z696whKu1sy0QfyHSSsRkt9ZGJJ5jNX4Z1yAnTUWZQCWXIqfhkWxebkWDY4heuGq
fsoS4ot25m9s2EMYScBjpAtO05xfSZx5t1JjFYTP+sIKoTna9TWrhYyy4+cQtW1S
ZfqBUswL3dE58kSX7YYJn/6Gq1Ih8OCtYD0qmF5A1La95qu+asLvlcOGiS19SZkG
bGBPj09KyxYrZRwzQvAt7IdkbEXe4LbjJKZyIrPoGSR0xdWrA1p3R6SK+enh8RXW
BocENBXBHFU1AATw1iVfurgz9u9NQYJe9tXQgCSygzphMe1vi5UfpO3wcGsO
-----END CERTIFICATE REQUEST-----
```

Copy the *"BEGIN PRIVATE KEY"* section (like below) paste it to a file such as `private-key.key` to the location where you installed OpenSSL.

```
-----BEGIN PRIVATE KEY-----
MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQCxikUWDCv8nIRo
8Di47ONhTg5wmXLEh0ezi0bZPAXQrVeiYc5ycfzl9MXONMdkMQqHwDYIrG4jmsr1
nzcmv0K33qejXnv2oTL8wzvX9kI/OwEPNKphfYYeVW0tbXuoePWH0tWm+ADnAwGR
H1ke6PV6wW3JcqdmfkXfihNfZWa1UES0JaGQC2IuOPkvAxTcXunVObtlLOGKbTaM
pmqaR2TeMUp/aRFjMUirjv8rHbVruXAmVqTxzYd4N0E8Rsi1uFCppAYRTv2OdNqj
rRHVfhKVsk1I24sHWQnp35L7UusnCheGMKDZcfwKe7yrYXkpjfbTXXrBuAfkfB3o
L/7uwsNFAgMBAAECggEAeAyyOH1UhQTk9/xvroPoINTiKLtqAoAjOMHVz3Cp0fhU
iKWwLmzrgCcqVgwUQ6hxoWeUYfsOop653KqjZVzw5Vn2ax6pnhRUYNw3LAoFs7HX
PovzJeb1+K71G0Gr2zindgdXlwadvZenyJS085S84RvIe+4+Saza3JQGE3yCndie
vInQ3QriChCHNpD1fuZu7PGqEE1eWIxHl4qYoLw5HFrQ9mBAvlVXsIkDP/7zDkIj
4nVJ59Ku5xadgSfuEwPy6e3I5bjmg9o7wqD/lszkt89vEFRF87zsACkp1nmk1m3H
xZ7csm4sfrpHkBRzkASDjGiZDcCFxkqr/8pZr8yGYQKBgQDnqM9V6EWk9WLRMgtb
hDlxgaGyVYDLt0DGS2J/nAb7y63sg9Ce0sBp++q/O+tSNs3eXzxV01MKKlpdtjwQ
Spsxwy+HBfYdzhZp8Nk60y8TDhZ721FZ5sEhtPUO1P/wQ93ApsZEFvoo0amlJqzh
2HwqgMWWJFvEM/Qb+js+mV0oDQKBgQDEMcFsp0Vz5acbrtdE+g3JOpIwb644DBs6
gKuvomakcXSoUV/UApWt/nNleNz6FDAEqe3F/nFM1QaoVegoA/N52evM3eVyJ6pv
xO73cnIOAhaJMKfpe6pvUgTOefbJLuRqrduzqh0crj3hRZxh6bo60QA/qr9tJSgy
fKFL6ZDCGQKBgCimapt8gpwLoydqTKvma94LDUCp2EvnACrLl6Ek0+TjPMW/65+z
A6iVV//ul8B5dW6L755v0qZ6ABlpnOiO7uSwh2p+FU3tl+lHJhc4b448bp2VQpUv
9LvhcQ8FOVQD1Km1mhzgm00GXWppevS2dDNRHVrXTnMDWtZ99l9psfsRAoGAVTR+
ml9yzEiacG1YVD58qj3jq2F1OiYX1Sp4ZYiUJyqWzVq50Wtl8fCl0RXSclE+IWhj
OS+tqP6DK6xTbL16ihrYS1q7AP61CGFwnsp3OhoyC1a0NbRdaocmSz2wreLNlH75
AWgJyKDrguAmcGd/V3fZMc1H4XDXqkVyD3PaSFECgYEA20r8TzTCSu60411QpqC4
6DM1iqsTyEgfb9D0v7ZY1XfT6oer6MCl7jSh9Iip8FCDgnmb3xnwuh4eZTwgfZJ5
1/cN13DZ/U7hSzfZzogeBFz3EFYKNmjogpAn/mr1V5a2VnjPW3USBasVaEqzJZr8
eYHyrOf+deyFYfQgN7vZokk=
-----END PRIVATE KEY-----
```

## 2. <span id="2">Generate an SSL certificate</span>

Use the CSR to issue your SSL certificate with a Certificate Authority (I usually use [123-Reg](https://www.123-reg.co.uk/) but you can use any). 

Save the certificate to a file such as `certificate.cer` to the location where you installed OpenSSL.

## 3. <span id="3">Use the SSL certificate and private key to generate a PFX file</span>

Open [an Administrator](https://www.howtogeek.com/194041/how-to-open-the-command-prompt-as-administrator-in-windows-8.1/) command prompt and CD to the OpenSSL directory.

Execute the following command: 

```
openssl pkcs12 -export -out myserver.pfx -inkey private-key.key -in certificate.cer
```

When prompted, choose a password which you'll use to upload it to Azure.