---
id: 28vfrhdgzj8rf1w63xeakj7
title: Arch
desc: ''
updated: 1655319691507
created: 1655319210223
---

## Pacman

```bash
# Display information
pacman -Qii
# Packages installed
pacman -Qm
# All packages
pacman -Qqe
# Display information
pacman -Qi name
# Remove package
pacman -R name
# Remove all package from package
pacman -Rns name
# Remove packages your system doesn't need
pacman -Yc
```

## Java

https://rtfm.co.ua/en/arch-linux-set-a-java-version/

```bash
yay -S jdk
java --version
# Change java version
sudo archlinux-java status
```

## Certificates

Add trusted certificates:

- Move /usr/local/share/ca-certificates/*.crt to /etc/ca-certificates/trust-source/anchors/
- Do the same with all manually-added /etc/ssl/certs/*.pem files and rename them to *.crt
- Instead of update-ca-certificates, run `sudo trust extract-compat`


```bash
# one by one
trust anchor --store server.crt
sudo update-ca-trust

# list all
trust list

# all
sudo mv *.pem /etc/ca-certificates/trust-source/anchors/
sudo trust extract-compat
sudo update-ca-trust
```
