---
id: qlua4vp9ifk441c5timakez
title: Kustomize
desc: ''
updated: 1678701170097
created: 1655740681667
---

# Kustomize

```bash
Kustomize/
├── base
│   ├── deployment.yaml
│   ├── kustomization.yaml
│   └── service.yaml
└── qa
    ├── kustomization.yaml
    └── update-replicas.yaml
```

```bash
# build kustomize for show resources before apply
kubectl kustomize path/file
# kustomize apply
kubectl apply -k path/file
```
