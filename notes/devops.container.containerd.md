---
id: llraahf8k3s4ervy6tnkubz
title: Containerd
desc: ''
updated: 1675436651637
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

# Nerdctl

Install [nerdctl](https://github.com/containerd/nerdctl).

```bash
NERDCTL_VERSION=1.2.0 # see https://github.com/containerd/nerdctl/releases for the latest release

wget -q "https://github.com/containerd/nerdctl/releases/download/v${NERDCTL_VERSION}/nerdctl-${NERDCTL_VERSION}-linux-amd64.tar.gz" -O /tmp/nerdctl.tar.gz
mkdir -p ~/.local/bin
tar -C ~/.local/bin/ -xzf /tmp/nerdctl.tar.gz
```

```bash
# show kubernetes containers running
nerdctl -n k8s.io ps
# show docker containers running
nerdctl -n movy ps
```