---
id: dwtnlyjb6jg0ntomf1t7x4e
title: Terraform
desc: ''
updated: 1655319041780
created: 1655319029908
---

Examples --> https://github.com/linuxacademy/content-terraform-2021

[Terracost] Costes en la nube --> https://www.infracost.io/docs/features/terraform_modules/

```bash
# Download
TER_VER=`curl -s https://api.github.com/repos/hashicorp/terraform/releases/latest | grep tag_name | cut -d: -f2 | tr -d \"\,\v | awk '{$1=$1};1'`
wget https://releases.hashicorp.com/terraform/${TER_VER}/terraform_${TER_VER}_linux_amd64.zip

# Unzip
unzip terraform_${TER_VER}_linux_amd64.zip
sudo mv terraform /usr/local/bin/
```