---
id: bw7jogrnauiehnik0wpe4b1
title: K8s
desc: ''
updated: 1678698502051
created: 1655235270066
---

- [Apps](#apps)
- [Version](#version)
  - [Plugins](#plugins)
- [Config](#config)
- [Comands](#comands)
- [AWS](#aws)
- [Users](#users)
- [Ingress](#ingress)
  - [Nginx Controller](#nginx-controller)
- [Weave (Net connection)](#weave-net-connection)
- [Bugs/Errors](#bugserrors)
- [Scalling](#scalling)
- [Certificates](#certificates)
- [Security](#security)

## Apps

- [K9s](https://k9scli.io)
- [Lens](https://github.com/lensapp/lens)
  - [pod-menu](https://github.com/alebcay/openlens-node-pod-menu)
  - [version-update](https://github.com/ottimis/lens-version-update)
- [Kubectx](https://github.com/ahmetb/kubectx)
- [OpenCost](https://github.com/opencost/opencost)

## Version

```bash
# display version
kubectl version
# display api version
kubectl api-versions | grep -i apps
```

### Plugins

[Krew](https://krew.sigs.k8s.io/)

```bash
# secret plugin
kubectl krew install whisper-secret
kubectl whisper-secret docker-registry my-secret --docker-password -- -n test --docker-username admin

# clean manifest
kubectl krew install neat
kubectl get pod mypod -o yaml | kubectl neat
kubectl neat get -- svc -n default myservice -o yaml

# permissions manager
https://github.com/sighupio/permission-manager

# Config files
kubectl krew install konfig
```

## Config

- Multiple context for different clusters. [kubeconfig](https://ahmet.im/blog/mastering-kubeconfig/)

```bash
kubectl config get-contexts
kubectl config use-context minikube
# extract config
kubectl config view --minify --flatten --context=minikube > minikube

# merge config
cd ~/.kube
kubectl konfig merge config <filename> > merged-config && mv -f merged-config config
```

## Comands

- Create labels

```bash
# Crate a label
kubectl label nodes kworker-rj1 workload=production

# Display labels
kubectl get nodes --show-labels

# Grep pods by labels
kubectl label --list nodes kworker-rj1 | grep -i workload workload=production
```

- Clean replicaset

```bash
kubectl delete replicaset $(kubectl get replicaset -o jsonpath='{ .items[?(@.spec.replicas==0)].metadata.name }' -n minikube) -n minikube 
```

- Saber el Storage Class del cluster

```bash
kubectl describe sc
kubectl get storageclass
```

- Force delete Pod
  
```bash
kubectl delete pod --force=true --wait=false --grace-period=0 podname -n ns
```

- Kubelet
 
```bash
sudo netstat -tulpn | grep kubelet
curl 127.0.0.1:10248/healthz
```

- Add nodes

```bash
# In Control Plane
kubeadm token create --print-join-command
# In worker node
kubeadm join url:6443 --token  --discovery-token-ca-cert-hash
# Enable kubelet
systemctl enable kubelet
# Ignoring Swap memory error
--ignore-preflight-errors=Swap
```

## AWS

- Configuration for AWS and K8s.

```bash
aws configure
aws sts get-caller-identity
# Download aws-iam-authenticator for get the token
curl -o aws-iam-authenticator https://amazon-eks.s3.us-west-2.amazonaws.com/1.21.2/2021-07-05/bin/linux/amd64/aws-iam-authenticator
```

## Users

```bash
kubectl get clusterrolebindings -o json | jq -r '.items[] | select(.subjects[0].kind=="Group") | select(.subjects[0].name=="system:masters")'
```

- Edit aws-auth for add new IAM roles.

```bash
kubectl edit -n kube-system configmap/aws-auth
# user example
arn:aws:iam::<userID>:user/<user-name>
```

```json
apiVersion: v1
data:
  mapAccounts: |
    []
  mapRoles: |
    - "groups":
      - "system:bootstrappers"
      - "system:nodes"
      "rolearn": "arn:aws:iam::<number>:role/<name>"
      "username": "system:node:{{EC2PrivateDNSName}}"
  mapUsers: |
    - "userarn": "arn:aws:iam::<number>:user/<user>"
      "username": "user"
      "groups":
      - "system:masters"
kind: ConfigMap
metadata:
  creationTimestamp: "2021-11-03T15:26:30Z"
  labels:
    app.kubernetes.io/managed-by: Terraform
    terraform.io/module: terraform-aws-modules.eks.aws
  name: aws-auth
  namespace: kube-system
  resourceVersion: "222342"
  uid: ce527f0b-e046-4b51-a853-b0abe675beeb
```

- Example of yaml

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: aws-auth
  namespace: kube-system
data:
  mapRoles: |
    - rolearn: <ARN of instance role (not instance profile)>
      username: system:node:{{EC2PrivateDNSName}}
      groups:
        - system:bootstrappers
        - system:nodes
```

## Ingress

### Nginx Controller

https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/

mTLS:
  - https://stackoverflow.com/questions/63025817/mtls-setup-using-self-signed-cert-in-kubernetes-and-nginx
  - https://awkwardferny.medium.com/configuring-certificate-based-mutual-authentication-with-kubernetes-ingress-nginx-20e7e38fdfca
  - https://medium.com/littlemanco/the-magic-of-tls-x509-and-mutual-authentication-explained-b2162dec4401
  - https://stackoverflow.com/questions/55690321/mutual-tls-based-on-specific-ip

```bash
# Enable client certificate authentication
nginx.ingress.kubernetes.io/auth-tls-verify-client: "on"
# Create the secret containing the trusted ca certificates
nginx.ingress.kubernetes.io/auth-tls-secret: "namespace/secret"
# Specify if certificates are passed to upstream server
nginx.ingress.kubernetes.io/auth-tls-pass-certificate-to-upstream: "true" 

# Proxy
nginx.ingress.kubernetes.io/proxy-ssl-secret: "namespace/secret"
nginx.ingress.kubernetes.io/proxy-ssl-protocols: "TLSv1.3"
nginx.ingress.kubernetes.io/proxy-ssl-name: "example.com"

# HTTPS Backend
nginx.ingress.kubernetes.io/backend-protocol: HTTPS
nginx.ingress.kubernetes.io/secure-backends: "true"
nginx.ingress.kubernetes.io/ssl-redirect: "true"
nginx.ingress.kubernetes.io/force-ssl-redirect: "true"

# Pass https
nginx.ingress.kubernetes.io/ssl-passthrough: "true"

# Add TLSv3
nginx.ingress.kubernetes.io/configuration-snippet: |
    proxy_ssl_protocols             TLSv1.3;

# Snippets
nginx.org/server-snippets: |
  location / {
    proxy_set_header Host         $host;
    proxy_set_header Upgrade      $http_upgrade;
    proxy_set_header Connection   $connection_upgrade;
  }

nginx.org/server-snippets: |
  ssl_certificate /etc/nginx/secrets/namespace-secret-name; # namespace-name
  ssl_certificate_key /etc/nginx/secrets/namespace-secret-name; # namespace-name

# Timeout
nginx.ingress.kubernetes.io/proxy-read-timeout: "3600"
```

## Weave (Net connection)

```bash
# Test connection in Workers
curl 'http://127.0.0.1:6784/status'
kubectl exec -n kube-system weave-net-j8k27 -c weave -- /home/weave/weave --local status
# display errors
kubectl logs -n kube-system <a-weave-pod-id> weave | grep -i error
# remove database and reboot Worker Node
rm /var/lib/weave/weave-netdata.db
reboot
```

## Bugs/Errors

- Broken connection between services with Names or IPs.


1. I would check my coreDNS pod under kube-system if there is an issue.
2. You could also try using the FQDN (fully qualified domain name) postgres-postgresql.[YOURNAMESPACE].svc.cluster.local
3. the postgres-postgresql service IP
4. postgres-postgresql-0 incase there is a problem with your svc networking


## Scalling

HorizontalPodAutoscaler

- Increase load deploying more Pods.

PodDisruptionBudget

- For HA you neeed to define Disruptions if a Node of the Cluster is down or upgraded. Stablish the minimum and maximum Pods are needed mandatory for your App.

## Certificates

```bash
# conexion to API for see the certificate
openssl s_client -showcerts -connect localhost:6443 | openssl x509 -noout -text 
```

Check certs expiration with `kubeadm`

```bash
kubeadm certs check-expiration
```

Renew certificates

```bash
kubeadm certs renew all
# output
Done renewing certificates. You must restart the kube-apiserver, kube-controller-manager, kube-scheduler and etcd, so that they can use the new certificates.
```

Find `admin.conf` file for restart the Pods

```bash
find / -name admin.conf
kubectl --kubeconfig=/etc/kubernetes/admin.conf get nodes
```

Copy the new configuration

```bash
cp /etc/kubernetes/admin.conf /root/.kube/config
```

## Security

Secure a K8s in AWS

https://blog.appsecco.com/hacking-an-aws-hosted-kubernetes-backed-product-and-failing-904cbe0b7c0d

[def]: #apps

Kube