---
id: e2lg9nuosaj8cqrvhf8m5ko
title: Vault
desc: ''
updated: 1655490350741
created: 1655490348664
---

RootCA->Intermediate1->vault_intermediate

```bash
# The private key needs to be changed from pkcs8 to pkcs1 
# Para Vault hay que pasar la Root CA a un pem
openssl rsa -in pkcs8.key -out pkcs1.key -outform pem

# Quitar encriptación para meter la CA en Vault
openssl rsa -in ssl.key.encrypted -out ssl.key.decrypted
# Se han juntado la clave privada y publica de la CA
cat name.crt nameca.key.decrypted > <ca-name>.pem
```
