---
id: b29yw0u79bh2i3f0mo5f1j1
title: MongoDB
desc: ''
updated: 1655362543927
created: 1655362537182
---

Crear usuario y pass en una database especifica.

```bash 
mongo admin -u admin -p admin --eval "db.getSiblingDB('dummydb').createUser({user: 'dummyuser', pwd: 'dummysecret', roles: ['readWrite']})"
```