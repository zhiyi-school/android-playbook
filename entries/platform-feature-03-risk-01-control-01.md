## platform-feature-03-risk-01-control-01

### Description

Insert here

### Demonstration
#### 01. 

Detect a certificate mismatch via CertificatePinner by first pinning a hash in your application at build time and then comparing it to the server's actual SHA-256 public key hash to ensure your application communicates only with the legitimate server

#### 02.

Prevent your application from sending network requests to unauthorised servers by rejecting any connection whose server certificate hash does not match the pinned value

