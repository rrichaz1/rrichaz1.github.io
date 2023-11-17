
# TLS security

TLS (Transport Layer Security) uses a combination of symmetric and asymmetric encryption to ensure message privacy. 
TLS uses a TLS handshake to establish a session. 
 During the handshake, the client and server agree on an encryption algorithm and a shared secret key. 
 The client encrypts the session key with the server's public key, and sends it back to the server. The server decrypts the client communication with its private key. 
The session key is used to encrypt the data transmitted by one party, and to decrypt the data received at the other end. Once the session is over, the session key is discarded. 
TLS also uses a public and private key system to encrypt and ensure data integrity. The client and server negotiate the strongest type of encryption that each can support. 
Once data is encrypted and authenticated, it is then signed with a message authentication code (MAC). The recipient can then verify the MAC to ensure the integrity of the data. 

nvisible to the end-user, a process called the “TLS/SSL handshake” creates a protected connection between your web server and web browser nearly instantaneously every time you visit a website. Websites secured by a TLS/SSL certificate will display HTTPS and the small padlock icon in the browser address bar. TLS/SSL certificates are used to protect both the end users’ information while it’s in transfer, and to authenticate the website’s organization identity to ensure users are interacting with legitimate website owners.

# THE TLS/SSL HANDSHAKE PROCESS
1. Each TLS certificate consists of a key pair made of a public key and private key.
2. These keys are important because they interact behind the scenes during website transactions.
3. Every time you visit a website, the client server and web browser communicate to ensure there is a secure TLS/SSL encrypted connection.
4. When a web browser (or client) directs to a secured website, the website server shares its TLS/SSL certificate and its public key with the client to establish a secure connection and a unique session key.
5. The browser confirms that it recognizes and trusts the issuer, or Certificate Authority, of the SSL certificate—in this case DigiCert. The browser also checks to ensure the TLS/SSL certificate is unexpired, unrevoked, and that it can be trusted.
6. The browser sends back a symmetric session key and the server decrypts the symmetric session key using its private key. The server then sends back an acknowledgement encrypted with the session key to start the encrypted session.
7. Server and browser now encrypt all transmitted data with the session key. They begin a secure session that protects message privacy, message integrity, and server security.

[Digital Certificates and secure connection](https://www.digicert.com/how-tls-ssl-certificates-work#:~:text=The%20browser%20sends%20back%20a,data%20with%20the%20session%20key.)

# Who should you trust? Implementing Security At Scale for FHIR

FHIR At Scale task force- guide created a [guide](http://hl7.org/fhir/us/udap-security/index.html)
1. Scalability 
    a. Frictionless app onboarding  - one app is reusable across mutiple FHIR end points. There is manual registration involved with different apps and vendors
    b. Life cycle management - app operator has to contact all operators to offboard or make changes
    b. Automated discovery and registration
    c. Reusable credentials for apps, servers & users
    d. Support for multiple trust communities - every data holder should not have to set up different endpoints

2. Security
    a. Built of seisting and widely used standards - TLS certificates are easy to get and can result in phishing attacks
        Oauth2.0
        Public Key Infrastructure
        OIDC
    b. Trusted apps and servers are identified using digital certificates
        a. Replace shared secrets amd manually exchanged keys with PKI certificates  
        b. Eliminate one-off registration and verififcation of every elient at every server   
        c. Increase confidence in identities of all actios in a transaction 
        d. Allow managemnet of an app over time - shared app identity within a community
        e. Enable more sophisticated buisness logic based on identity, purpose of use etc.


## Trusted Dynamic Client Registration

1. Client App Identity in UDAP certificate:
    identityof actor can be validated by 3rd party
    suppot for multiplr trust communities
    digital sigratures for authenticity and integrity
2. Certifications & Endorsements
    - self assertions e.g. privacy declarations
    - third party assertions e.g. security audits, data use agreements etc.
    - digital signatures for authenticity and integrity


## OAuth 2.0 Sign In with UDAP Trusted DCR

1. Client App uses certificate to register and authenticate
2. Client App validates server metadata
3. Verified app details shown to user
4. Trusted Identity Provider (IdP) can provide reusable digital identity and other user attributes

UPDAP 
http://hl7.org/fhir/us/udap-security/index.html


[HL7 FHIR Conference videos](https://info.hl7.org/hl7-fhir-security-education-event-live)