# SSL-TLS
 - SSL: Secure Sockets Layer, used to encrypt connections
 - TLS: Transport Security Layer, new version of SSL
 - SSL certificates (TLS certificates are still referred to as SSL) allows traffic between your clients and LB to be encrypted in transit
 - Public SSL certificates are issued by Certificate Auhorities (CA), ex. Symantec, GoDaddy, Comodo
 - SSL cert. have a set expiration date and must be renewed 
 - The LB uses an X.509 certificate (SSL/TLS server certificate)
 - ACM allows you to manage certificates, or you can upload your own certificates
 - HTTPS Listener (Client to LB)
    - You must specify a default certificate
    - Optional list of certs to support multiple domains
    - Clients can use SNI to specify the hostname they reach

## SNI - Server Name Indication
 - SNI solves the problem of loading multiple SSL certs onto one web server to serve multiple websites
 - A newer protocol, client indicates hostname of target server in the initial SSL handshake
 - Server then finds the correct cert, or returns the default
 - Only works for ALB, NLB, CloudFront, but not CLB
    - In ALB, each target group can have a seperate cert

 