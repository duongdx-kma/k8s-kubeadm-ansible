<h3>Sign yourself certificate</h3>

- ##### create CA private key:
> openssl genrsa -des3 -out ca.key 2048

- #####  make CA "certificate signing request" file:
> openssl req -new -key ca.key -subj "/C=VN/ST=HN/L=HN/OU=duongdx_test/CN=*.duongdx.com" -out ca.csr

- ##### create CA certificate ca.crt from ca.csr have just been created
> openssl x509 -req -in ca.csr -signkey ca.key -out ca.crt

- ##### generate server key duongdx.com:
> openssl genrsa -out duongdx.key 2048

- #####  make "certificate signing request" file for duongdx.com:
> openssl req -new -key duongdx.key -subj "/C=VN/ST=HN/L=HN/OU=duongdx_test/CN=*.duongdx.com" -out duongdx.csr

- ##### create server certificate - duongdx.com
>  openssl x509 -req -days 3650 -in duongdx.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out duongdx.crt

- ##### make pem file:
> cat duongdx.key > duongdx.pem
> cat duongdx.csr >> duongdx.pem
> cat duongdx.crt >> duongdx.pem