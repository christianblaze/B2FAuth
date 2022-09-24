What is Bitcoin 2-factor authentication (B2FAuth)?
==================================================
B2FAuth is a decentralized two-factor authentication system.

How does it work?
==================================================
### SETUP:
A client (the "Client") sets up B2FAuth as their 2-factor authentication method to access an app or website (the "SecuredApp") on a server ("Server") by generating a public key ("Pubkey") from the private key contained on their B2FAuth application (the "Privkey"), and hashing it (the "Pubhash").  The Pubhash is shared with the Server and both the Server and Client store it for future reference. [Salt](https://en.wikipedia.org/wiki/Salt_(cryptography)) may also be used to increase security or to derrive multiple Pubhashes from the same Pubkey.  

### LOGIN:
The next time the Client logs into the SecuredApp, the Server will ask for a B2FAuth code.  The Client generates the code by obtaining the current Bitcoin block hash (the "Current Block Hash"), combining it with the Pubhash, hashing the combined data, generating a new hash (the "Loginhash"), converting the Loginhash from hexadecimal to decimal, and creating a code consisting of the resulting first and last 3 digits (the "AuthCode").  On the Server side, the same steps are taken to generate the same AuthCode for verification.  If the Client provides the Server with the matching AuthCode, access is granted.  

The AuthCode changes everytime there is a new Bitcoin block generated, and it is mathematically impossible to predict what the next code might be, even if you know the Pubhash or Pubkey.  
