

# TLS commands

genrsa --> req-->x509

**Creating a private key**
openssl rsa -pubin -outform der 
openssl dgst -sha256 -hex
openssl genrsa -out my.key 2048
**creatng a csr ***
openssl req -new -key my.key -out my.csr -subject="/CN=myname/O=mygroup"
**self-siginging a csr**
# TLS commands
openssl x509 -text -noout
openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt 
openssl rsa -pubin -outform der 
openssl dgst -sha256 -hex

openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | \
openssl dgst -sha256 -hex | sed 's/^.* //'

openssl x509 -req -in myuser.csr -CA ca.crt -CAKey ca.key -CAcreateserial -out myuser.crt -days 356

**opening a csr file**
openssl req  -in mycsr.csr --noout -text

**opening a cert file**
openssl x509 -text -noout
openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt 


openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | \
   openssl dgst -sha256 -hex | sed 's/^.* //'

openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null |    openssl dgst -sha256 -hex | sed 's/^.* //'