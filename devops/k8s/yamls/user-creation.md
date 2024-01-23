# openssl 

openssl genrsa -out myuser.key 2048
openssl req -new -key myuser.key -out myuser.csr -subject="/CN=myname/O=mygroup"
openssl x509 -req -in myuser.csr -CA ca.crt -CAKey ca.key -CAcreateserial -out myuser.crt -days 356

openssl req -text -in myuser.csr -noout
openssl x509 -- in mycert.cert -text -noout