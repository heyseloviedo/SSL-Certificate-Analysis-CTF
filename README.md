# SSL Certificate Analysis CTF

## Objective

The objective of this project was to inspect Cyber Skyline's SSL/TLS certificate and identify the certificate issuer, determine the public key length, and verify how many certificates were provided in the certificate chain. The challenge focused on reading certificate details in Chrome and using OpenSSL in Terminal to inspect the TLS connection.

### Skills Learned

- Identifying a certificate issuer from SSL/TLS certificate details.
- Reading public key information and determining RSA key length.
- Understanding the purpose of a certificate chain.
- Using OpenSSL to inspect certificates presented by a remote HTTPS server.
- Interpreting common SSL/TLS certificate fields and command-line output.

### Tools Used

- Google Chrome Certificate Viewer
- macOS Terminal
- OpenSSL `s_client`

## Steps

### Step 1 - Review the SSL Certificate Challenge

The Cyber Skyline SSL challenge asked three questions: identify the issuer of Cyber Skyline's SSL certificate, determine the SSL key length, and count the certificates in the certificate chain.

![Cyber Skyline SSL Challenge](images/challenge.png)

*Ref 1: Cyber Skyline SSL challenge showing the three certificate questions.*

### Step 2 - Identify the Certificate Issuer

The certificate for `*.cyberskyline.com` was opened in Chrome's Certificate Viewer. Under **Issued By**, the Common Name was listed as **Sectigo Public Server Authentication CA DV R36**.

**Answer:** Sectigo Public Server Authentication CA DV R36

![Certificate Issuer](images/issuer.png)

*Ref 2: Chrome Certificate Viewer showing Sectigo Public Server Authentication CA DV R36 as the issuer.*

### Step 3 - Determine the SSL Key Length

The **Details** tab was opened and **Subject Public Key Info** was inspected. Under **Subject's Public Key**, the field value displayed **Modulus (2048 bits)**.

**Answer:** 2048 bits

![Public Key Length](images/key-length.png)

*Ref 3: Certificate details showing a 2048-bit modulus for the public key.*

### Step 4 - Inspect the Certificate Chain with OpenSSL

OpenSSL was used in macOS Terminal to inspect the TLS connection and certificate chain with the following command:

```bash
openssl s_client -connect cyberskyline.com:443 -servername cyberskyline.com -showcerts
```

The output displayed three server-provided certificates in the **Certificate chain** section, numbered **0**, **1**, and **2**.

**Answer:** 3 certificates

![OpenSSL Certificate Chain](images/certificate-chain.png)

*Ref 4: OpenSSL output used to inspect the Cyber Skyline certificate chain.*

## Results

- **Certificate Issuer:** Sectigo Public Server Authentication CA DV R36
- **SSL Key Length:** 2048 bits
- **Certificates in Chain:** 3
