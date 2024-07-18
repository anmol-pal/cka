# What are TLS Certificates

Data transfered over network can be sniffed easily if not encrypted.

The encrypted data is sent along with the key to decrypt it - Symmetric Encryption [Not safe] as same key is used to encrypt and decrypt the data

Better Practice:
Asymmetric Encryption:
It uses a pair of keys [Private Key and Public Key]
Private key is kept private, Public key is shared

If you encrypt data with public key, it can only be decrypted with a private key, so no matter who gets hold of your public key.

so server sends the public key to initiate the connection , client will recieve the [public-key] and send its encrypted [sensitive-data] along with [symmetric-key] to decrypt [sensitive-data] encrypted by the [public-key] which can be decrypted by server [private-key] in possession of server.

Hacker can pretend to be the server , and send its own [public-key] and client might send its own [sensitive-data] with symmetric key to decrypt [sensitive-data] encrypted by [public-key] sent by fraudulent server.

Here comes concept of Certificate Authority.

* Creating a legit certificate that web-browsers will trust
- Submit a certificate signing request(CSR)  using key and domain-name of the website
```openssl req -new -key my-bank.key -out my-bank.csr -subj "/C=US/ST=CA/O=MyOrg,Inc./CN=my-bank.com"```
now CA signs the certificate and sends it back to you

* How does browser know if the certificate was signed by the fake CA ?
- CAs themselves have a set of public and private key-pair , CA's use their private keys to sign certificates and  public-keys are built in sent to the browser.

Any company that wants to create their own CA Authority, will have a private CA Server deployed within the company.
Then you can have the public CA certificate installed on the browser of the employees.

--------
Summary

[1.] We use Asymmetric encryption with a pair of public and private key.
[2.] Admin uses a pair of keys to secure ssh connectivity to servers
[3.] Server uses a pair of keys to secure HTTP Traffic
    [3.1] Server first sends a Certificate Signing request to a CA
    [3.2] CA Uses its private key to sign the CSR
    [3.3] The signed certificate is sent back to the server
    [3.4] Server configures its web-app with the signed certificate
[4.] User access the application and Server sends certificate with its public key
    [4.1] The user now uses CA's public key to validate the CA Certificate and retrieves CA's public key
    [4.2] User now generates a symmetric key that it wishes to use going forward
    [4.3] This symmetric key is encrypted using server's public key and sent back to server
[5.] The server now has user's private key to encrypt [sensitive data] sent by client

Now for Server to validate client , client may also generate a CA certificate and present it to server at the time of trust-building exercise.
