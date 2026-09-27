---
title: "Virt Manager: Virtualização no Linux"
date_created: 2026-08-17
author: "Bruno César"
privacy: public
tags:
  - publico
  - linux/virtualizacao
  - linux/kvm
  - linux/virt-manager
---

# 🖥️ Virt Manager: Virtualização no Linux

> [!info] Instalação e configuração do Virt Manager para gerenciamento de máquinas virtuais usando KVM no Omarchy (Arch Linux), Fedora e Ubuntu.

---

## 📦 1. Instalar Virt Manager & KVM

### Omarchy & Arch Linux

```bash
sudo pacman -S --needed qemu-desktop virt-manager virt-viewer dnsmasq bridge-utils iptables-nft edk2-ovmf
sudo systemctl enable --now libvirtd
```

### Fedora

```bash
sudo dnf install -y @virtualization
sudo systemctl enable --now libvirtd
```

### Ubuntu

```bash
sudo apt update && sudo apt install -y qemu qemu-kvm libvirt-daemon libvirt-clients bridge-utils virt-manager
sudo systemctl enable --now libvirtd
```

---

## ⚙️ 2. Configurar permissões do usuário

> [!tip] Para gerenciar suas VMs de forma nativa, ágil e segura com o seu próprio usuário (sem solicitar sudo no Virt-Manager), adicione sua conta aos grupos `libvirt` e `kvm`.

### Omarchy & Arch Linux

```bash
sudo usermod -aG libvirt,kvm $USER
```

### Fedora

```bash
sudo usermod -aG libvirt $USER
```

### Ubuntu

```bash
sudo usermod -aG libvirt,kvm $USER
```

> [!note] Após adicionar o usuário aos grupos, faça logout e login novamente (ou execute `newgrp libvirt`) para aplicar as novas permissões.

---

## 📦 3. Instalar QEMU Guest Agent (Dentro da VM)

### Omarchy & Arch Linux

```bash
sudo pacman -S --needed qemu-guest-agent
sudo systemctl enable --now qemu-guest-agent
```

### Fedora

```bash
sudo dnf install -y qemu-guest-agent
sudo systemctl enable --now qemu-guest-agent
```

### Ubuntu

```bash
sudo apt install -y qemu-guest-agent
sudo systemctl enable --now qemu-guest-agent
```

---

## 🔗 Notas Relacionadas
- [Windows 11 no KVM](06_virtualizacao_win11_kvm.md) — Configuração de VM Windows 11 com drivers VirtIO.
- [Containers com Distrobox e Docker](04_containers_distrobox_docker.md) — Solução leve de isolamento de processos.
- [Omarchy: Pós-instalação](02_omarchy_pos_instalacao.md) — Permissões de grupos e suporte a virtualização.
