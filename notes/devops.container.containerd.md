---
id: llraahf8k3s4ervy6tnkubz
title: Containerd
desc: ''
updated: 1656430992461
created: 1655320685678
---

# Containerd

Commands ar the same as Docker commands.

```bash
# show images
crictl images
# show containers running
crictl ps
# display containerd information 
crictl info 
```

```bash
systemctl restart containerd
```

- How to add Insecure Registry:

```toml
# /etc/containerd/config.toml
# change <IP>:5000 to your registry url

[plugins."io.containerd.grpc.v1.cri".registry]
  [plugins."io.containerd.grpc.v1.cri".registry.mirrors]
    [plugins."io.containerd.grpc.v1.cri".registry.mirrors."<IP>:5000"]
      endpoint = ["http://<IP>:5000"]
  [plugins."io.containerd.grpc.v1.cri".registry.configs]
    [plugins."io.containerd.grpc.v1.cri".registry.configs."<IP>:5000".tls]
      insecure_skip_verify = true
```