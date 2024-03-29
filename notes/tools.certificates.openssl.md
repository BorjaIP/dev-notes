---
id: 04z14el6i8h2d9sgvjwzvai
title: Openssl
desc: ''
updated: 1677159139784
created: 1655490070571
---

## Self sign certificate

```bash
openssl req -newkey rsa:2048 -new -nodes -x509 -days 3650 -keyout key.pem -out cert.pem
```

```bash
# verificar que es una CA
openssl x509 -noout -text -in ca/public/name.crt 
# tiene que salir algo así
 X509v3 Basic Constraints: critical
                CA:TRUE

# verificar un certificado
openssl verify -CAfile ca/public/name.crt k8s/ca-cert.pem

# comprobar el texto del certificado
openssl x509 -in /etc/ssl/certs/name.crt -text 

# información CSR o .req
openssl req -noout -text -in <name>.req

# pasar de crt a pem
openssl x509 -in k8s/ca-key.crt -out k8s/ca-key.pem -outform PEM

# extraer el CSR de un certificado
openssl x509 -x509toreq -in name.crt -signkey name.key -out name.csr

## Keytool
# convertir jks
keytool -importkeystore -srckeystore certificate.p12 -srcstoretype pkcs12 -destkeystore cert.jks
keytool -list -keystore generic.jks -v
# List CA
keytool -list -keystore $JAVA_HOME/lib/security/cacerts -storepass changeit
```

RootCA
    - Root Private key
    - Root Certificate
    - CSR (Certificate Signing Request) --> .req o .csr (El certificado creado para luego firmarlo con la CA)

## Create certificates

```bash
mkdir ca/<name>

# crear una key
openssl genrsa -out ca/<name>.key 2048

# crear un certificate request para firmar
openssl req -new -key ca/<name>.key -out ca/<name>.req
# con conf hecha
openssl req -new -key ca/<name>.key -out ca/<name>.req -config ca/<name>.cnf

# verificar que la firma con la key generada está bien
openssl req -verify -in ca/<name>.req -text -noout

# firmar el CSR de la request para que lo valide nuestra CA
# esto añade una línea en el txt como BBDD de todos los certificados
openssl ca -config ca/node.cnf -out ca/issued/name.crt -infiles ca/<name>.req
# firmar con SAN para dominio
openssl ca -config ca/node.cnf -out ca/issued/name.crt -extensions v3_req -infiles ca/<name>.req
# comprobar la firma
openssl x509 -noout -text -in ca/issued/name.crt

# verificar conexion
openssl s_client -connect <name>:443 -CAfile /etc/ssl/certs/<ca-name>.crt
echo | openssl s_client -connect redhat.com:443 2>/dev/null | openssl x509 -noout -ext subjectAltName

# crear una intermediate CA
openssl genrsa -out intermediate/private/intermediate.key 4096
# para evitar borrar la CA cambiarle los permisos
chmod 400 intermediate/private/intermediate.key

# crear la request
openssl req -config intermediate/intermediate.cnf -new -sha256 -key intermediate/private/intermediate.key -out intermediate/certificates/intermediate.csr

# firmarla con nuestra CA
openssl ca -config node.cnf -extensions v3_intermediate_ca v3_req -notext -md sha256 -in intermediate/certificates/intermediate.csr -out intermediate/certificates/intermediate.crt
# para evitar borrar la CA cambiarle los permisos
chmod 444 intermediate/public/intermediate.crt

# verify intermediate CA
openssl x509 -noout -text -in intermediate/certificates/intermediate.crt
openssl verify -CAfile public/<ca-name>.crt intermediate/public/intermediate.crt
```

## P12

```bash
# convert crt --> .p12 
openssl pkcs12 -export -clcerts -inkey client.key -in client.crt -out client.p12 -name "MyKey"

# see content of a P12
openssl pkcs12 -info -nodes -in yourfilename.p12 -passin pass:password

# list P12
keytool -list -v -keystore test.p12 -storepass password -storetype PKCS12

# list jks
keytool -v -list -keystore test.jks -storepass password

# extract certs
openssl pkcs12 -in path.p12 -out newfile.crt.pem -clcerts -nokeys

# extract keys
openssl pkcs12 -in path.p12 -out newfile.key.pem -nocerts -nodes
```

## CNF

User `critical` for force to in this case load the custom CA.

```conf
[v3_req]
subjectAltName                  = critical, @alt_names
basicConstraints                = critical, CA:FALSE
keyUsage                        = critical, digitalSignature, keyEncipherment, keyAgreement
extendedKeyUsage                = critical, serverAuth, clientAuth
subjectKeyIdentifier            = critical, hash
authorityKeyIdentifier          = critical, keyid, issuer
```