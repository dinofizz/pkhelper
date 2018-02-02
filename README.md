# pkhelper

pkhelper is a bash script which aids in the collection of information about the public keys of a certificate chain.

This is useful when needing the SHA-1 fingerprint of a certificate's public key for use in certificate pinning scenarios.

## Overview

pkhelper performs the following actions:

1) Saves the full chain of certificates to a file.
2) Extracts each individual certificate in the chain to individual files.
3) Displays the subject of the certificate and fingerprint data for the certificate's public key.

The files are saved in a folder named by the host whose certificate chain is being queried. See example usage below.

## Pre-requisites

You will need a bash shell, sed, awk and the OpenSSL client binary.

To check if you have the OpenSSL client binary executable enter the following in your terminal:

```
$ openssl version
OpenSSL 1.0.2k  26 Jan 2017
```

## Usage

pkhelper takes arguments for the host and port of the target address whose certificate chain and public key(s) you would like to inspect.

```
$ ./pkhelper -h www.google.com -p 443
Checking if www.google.com directory exists.
www.google.com directory exists, deleting.
Creating www.google.com directory
Connecting to www.google.com:443 and saving full chain to file www.google.com/www.google.com_fullchain.pem


www.google.com.1.pem

-----BEGIN CERTIFICATE-----
MIIEdjCCA16gAwIBAgIIUHhcStTgTEwwDQYJKoZIhvcNAQELBQAwSTELMAkGA1UE
BhMCVVMxEzARBgNVBAoTCkdvb2dsZSBJbmMxJTAjBgNVBAMTHEdvb2dsZSBJbnRl
cm5ldCBBdXRob3JpdHkgRzIwHhcNMTgwMTE2MDg1NzMxWhcNMTgwNDEwMDg0MjAw
WjBoMQswCQYDVQQGEwJVUzETMBEGA1UECAwKQ2FsaWZvcm5pYTEWMBQGA1UEBwwN
TW91bnRhaW4gVmlldzETMBEGA1UECgwKR29vZ2xlIEluYzEXMBUGA1UEAwwOd3d3
Lmdvb2dsZS5jb20wggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQDa7/L5
amnY7wapio5tS6wRg5ApLDr0jw3E9yIHj/WHVacPYXjZW8rCX8wVF2aEFvGxf+OY
siPaaGsdUi4NLKQZPi58tlQ3pEyxe7lX9DbOxaBiIwnKIUhNV5yWgTmciHJ+BGfs
JBfhOOWYqA2G/L/hZo0aKRPooEq3SKvOqcdB8poXBFtiNsJ1Q+WuPRyDrdXK+60q
rxgeVr8qZPIQJXZOaeaz5YgZG75W9iNC2WUdGkbuq5Wp2v0vLAzSlZ363gT9ZFD/
H8mJJ5JpO+9iC1AqeVxhdaj6PeMVvA4nNLU4u3aG+lmTMiTAnhTtdE91fo05jrx8
4uHiBF9JxZy9jbXrAgMBAAGjggFBMIIBPTATBgNVHSUEDDAKBggrBgEFBQcDATAZ
BgNVHREEEjAQgg53d3cuZ29vZ2xlLmNvbTBoBggrBgEFBQcBAQRcMFowKwYIKwYB
BQUHMAKGH2h0dHA6Ly9wa2kuZ29vZ2xlLmNvbS9HSUFHMi5jcnQwKwYIKwYBBQUH
MAGGH2h0dHA6Ly9jbGllbnRzMS5nb29nbGUuY29tL29jc3AwHQYDVR0OBBYEFMcE
jkZ9tW4nfomOiMHJ3qiZiOATMAwGA1UdEwEB/wQCMAAwHwYDVR0jBBgwFoAUSt0G
Fhu89mi1dvWBtrtiGrpagS8wIQYDVR0gBBowGDAMBgorBgEEAdZ5AgUBMAgGBmeB
DAECAjAwBgNVHR8EKTAnMCWgI6Ahhh9odHRwOi8vcGtpLmdvb2dsZS5jb20vR0lB
RzIuY3JsMA0GCSqGSIb3DQEBCwUAA4IBAQBKESXhISsT6zY8aX7z+18ERjDPQd3W
xt9W2lN5MspWearA3BUhOCoa1Pdd4afG65bqhzp6xVXyANb2KpE5Skb/erciaGo2
XstWAkUv4UgN/nnfxlbTTKgULjOdrI9H/x2d8g8mpdO6bV3r9qSzf67sHL6J7pwe
EyWg6PXIJfN5ewQonmz4isF9KDlMD2BkgyfnAo8cSzbwDKPfjzzf9WPk7BBiIMkH
CVGqGhTRKSnGchdvXBo+zla7TJJ1y9T7Khhl6M5fpr7DWoVIQKqFv/7O3IhFpkYG
XFMPjfaVZ1VRb5uBr0XJooxEsgqxcIEtPE2upmri/DshNS/i4B1fSTKQ
-----END CERTIFICATE-----


Subject: subject= /C=US/ST=California/L=Mountain View/O=Google Inc/CN=www.google.com
Public key fingerprint (hex values): SHA1 Fingerprint=56:0A:28:39:F5:35:A7:B4:92:2C:C4:DB:2A:7E:7A:47:74:B7:B6:A0
Base64 encoded public key fingerprint: PLpHCbGn5NtdI/wNHPGTfnpvDTU=


www.google.com.2.pem

-----BEGIN CERTIFICATE-----
MIIEKDCCAxCgAwIBAgIQAQAhJYiw+lmnd+8Fe2Yn3zANBgkqhkiG9w0BAQsFADBC
MQswCQYDVQQGEwJVUzEWMBQGA1UEChMNR2VvVHJ1c3QgSW5jLjEbMBkGA1UEAxMS
R2VvVHJ1c3QgR2xvYmFsIENBMB4XDTE3MDUyMjExMzIzN1oXDTE4MTIzMTIzNTk1
OVowSTELMAkGA1UEBhMCVVMxEzARBgNVBAoTCkdvb2dsZSBJbmMxJTAjBgNVBAMT
HEdvb2dsZSBJbnRlcm5ldCBBdXRob3JpdHkgRzIwggEiMA0GCSqGSIb3DQEBAQUA
A4IBDwAwggEKAoIBAQCcKgR3XNhQkToGo4Lg2FBIvIk/8RlwGohGfuCPxfGJziHu
Wv5hDbcyRImgdAtTT1WkzoJile7rWV/G4QWAEsRelD+8W0g49FP3JOb7kekVxM/0
Uw30SvyfVN59vqBrb4fA0FAfKDADQNoIc1Fsf/86PKc3Bo69SxEE630k3ub5/DFx
+5TVYPMuSq9C0svqxGoassxT3RVLix/IGWEfzZ2oPmMrhDVpZYTIGcVGIvhTlb7j
gEoQxirsupcgEcc5mRAEoPBhepUljE5SdeK27QjKFPzOImqzTs9GA5eXA37Asd57
r0Uzz7o+cbfe9CUlwg01iZ2d+w4ReYkeN8WvjnJpAgMBAAGjggERMIIBDTAfBgNV
HSMEGDAWgBTAephojYn7qwVkDBF9qn1luMrMTjAdBgNVHQ4EFgQUSt0GFhu89mi1
dvWBtrtiGrpagS8wDgYDVR0PAQH/BAQDAgEGMC4GCCsGAQUFBwEBBCIwIDAeBggr
BgEFBQcwAYYSaHR0cDovL2cuc3ltY2QuY29tMBIGA1UdEwEB/wQIMAYBAf8CAQAw
NQYDVR0fBC4wLDAqoCigJoYkaHR0cDovL2cuc3ltY2IuY29tL2NybHMvZ3RnbG9i
YWwuY3JsMCEGA1UdIAQaMBgwDAYKKwYBBAHWeQIFATAIBgZngQwBAgIwHQYDVR0l
BBYwFAYIKwYBBQUHAwEGCCsGAQUFBwMCMA0GCSqGSIb3DQEBCwUAA4IBAQDKSeWs
12Rkd1u+cfrP9B4jx5ppY1Rf60zWGSgjZGaOHMeHgGRfBIsmr5jfCnC8vBk97nsz
qX+99AXUcLsFJnnqmseYuQcZZTTMPOk/xQH6bwx+23pwXEz+LQDwyr4tjrSogPsB
E4jLnD/lu3fKOmc2887VJwJyQ6C9bgLxRwVxPgFZ6RGeGvOED4Cmong1L7bHon8X
fOGLVq7uZ4hRJzBgpWJSwzfVO+qFKgE4h6LPcK2kesnE58rF2rwjMvL+GMJ74N87
L9TQEOaWTPtEtyFkDbkAlDASJodYmDkFOA/MgkgMCkdm7r+0X8T/cKjhf4t5K7hl
MqO5tzHpCvX2HzLc
-----END CERTIFICATE-----


Subject: subject= /C=US/O=Google Inc/CN=Google Internet Authority G2
Public key fingerprint (hex values): SHA1 Fingerprint=A6:12:0F:C0:B4:66:4F:AD:0B:3B:6F:FD:5F:7A:33:E5:61:DD:B8:7D
Base64 encoded public key fingerprint: Q9rWMO5T+KmAym79hfRqo3mQ4Oo=


www.google.com.3.pem

-----BEGIN CERTIFICATE-----
MIIDfTCCAuagAwIBAgIDErvmMA0GCSqGSIb3DQEBBQUAME4xCzAJBgNVBAYTAlVT
MRAwDgYDVQQKEwdFcXVpZmF4MS0wKwYDVQQLEyRFcXVpZmF4IFNlY3VyZSBDZXJ0
aWZpY2F0ZSBBdXRob3JpdHkwHhcNMDIwNTIxMDQwMDAwWhcNMTgwODIxMDQwMDAw
WjBCMQswCQYDVQQGEwJVUzEWMBQGA1UEChMNR2VvVHJ1c3QgSW5jLjEbMBkGA1UE
AxMSR2VvVHJ1c3QgR2xvYmFsIENBMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIB
CgKCAQEA2swYYzD99BcjGlZ+W988bDjkcbd4kdS8odhM+KhDtgPpTSEHCIjaWC9m
OSm9BXiLnTjoBbdqfnGk5sRgprDvgOSJKA+eJdbtg/OtppHHmMlCGDUUna2YRpIu
T8rxh0PBFpVXLVDviS2Aelet8u5fa9IAjbkU+BQVNdnARqN7csiRv8lVK83Qlz6c
JmTM386DGXHKTubU1XupGc1V3sjs0l44U+VcT4wt/lAjNvxm5suOpDkZALeVAjmR
Cw7+OC7RHQWa9k0+bw8HHa8sHo9gOeL6NlMTOdReJivbPagUvTLrGAMoUgRx5asz
PeE4uwc2hGKceeoWMPRfwCvocWvk+QIDAQABo4HwMIHtMB8GA1UdIwQYMBaAFEjm
aPkr0rKV10fYIyAQTzOYkJ/UMB0GA1UdDgQWBBTAephojYn7qwVkDBF9qn1luMrM
TjAPBgNVHRMBAf8EBTADAQH/MA4GA1UdDwEB/wQEAwIBBjA6BgNVHR8EMzAxMC+g
LaArhilodHRwOi8vY3JsLmdlb3RydXN0LmNvbS9jcmxzL3NlY3VyZWNhLmNybDBO
BgNVHSAERzBFMEMGBFUdIAAwOzA5BggrBgEFBQcCARYtaHR0cHM6Ly93d3cuZ2Vv
dHJ1c3QuY29tL3Jlc291cmNlcy9yZXBvc2l0b3J5MA0GCSqGSIb3DQEBBQUAA4GB
AHbhEm5OSxYShjAGsoEIz/AIx8dxfmbuwu3UOx//8PDITtZDOLC5MH0Y0FWDomrL
NhGc6Ehmo21/uBPUR/6LWlxz/K7ZGzIZOKuXNBSqltLroxwUCEm2u+WR74M26x1W
b8ravHNjkOR/ez4iyz0H7V84dJzjA1BOoa+Y7mHyhD8S
-----END CERTIFICATE-----


Subject: subject= /C=US/O=GeoTrust Inc./CN=GeoTrust Global CA
Public key fingerprint (hex values): SHA1 Fingerprint=73:59:75:5C:6D:F9:A0:AB:C3:06:0B:CE:36:95:64:C8:EC:45:42:A3
Base64 encoded public key fingerprint: wHqYaI2J+6sFZAwRfap9ZbjKzE4=
```

 

