---
title: Kubernetes Cluster on Raspberry Pi
date: 2024-06-10 +0000
categories: [linux, docker, containers]
tags: [linux,documentation,arm64,amd64,cluster,pi]
---

## Preperation

Prep all the Raspberry Pis with the lite non desktop 64bit version of Raspberry Pi OS.
Be shure to set a unique hostname for each Raspberry Pi.

## Install k3s

ssh into the first node which will become the master and switch to root:

```bash
sudo su -
```

Update and install tailscale

```bash
apt update && apt upgrade -y && curl -fsSL https://tailscale.com/install.sh | sh && tailscale up --ssh
```

Modify the cmdline.txt file and reboot:

```bash
sed -i '1s/^/cgroup_enable=cpuset cgroup_memory=1 cgroup_enable=memory /' /boot/firmware/cmdline.txt
reboot
```

After logging back in, install k3s and verify the installation:

```bash
curl -sfL https://get.k3s.io | sh -
kubectl get nodes
```

## Join the other nodes

Repeat the install process for each node and extract the token from your master node.

```bash
cat /var/lib/rancher/k3s/server/node-token
```

ssh into the other nodes and join the cluster using the token and hostname from the master node:

```bash
curl -sfL https://get.k3s.io | K3S_URL=https://hostname:6443 K3S_TOKEN=token_from_earlier sh -
```

<!-- ## Install portainer

If you want to install portainer on your cluster, run the following commands on your master node:

```bash -->

