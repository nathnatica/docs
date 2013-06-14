#####SSL Setting
1. make a private key
`openssl genrsa -des3 -out server.key 1024`  

2. make a csr key
`openssl req -new -key server.key -out server.csr`  

3. remove password from the private key
`opnessl rsa -in server.key -out server.key.insecure`  
`mv server.key server.key.secure`   
`mv server.key.insecure server.key`     

4. make CA certificate  
`openssl x509 -req -days 1280 -in server.csr -signkey server.key -out server.crt`  

5. modify httpd.conf   
remove comment around `Include conf/extra/httpd-ssl.conf`  


might need to comment out  
`SSLPassPhraseDialog  builtin` part  


