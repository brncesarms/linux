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

> [!info] Instalação e configuração do Virt Manager para gerenciamento de máquinas virtuais usando KVM no Fedora e Ubuntu.

---

## 📦 1. Instalar Virt Manager & KVM

### Omarchy & Arch Linux

```bash
sudo pacman -S --needed qemu-desktop virt-manager virt-viewer dnsmasq bridge-utils iptables-nft edk2-ovmf
sudo systemctl enable --now libvirtd
```

### Fedora

```bash
sudo dnf install @virtualization
systemctl reboot

```

### Ubuntu

```bash
sudo apt install -y qemu qemu-kvm libvirt-daemon libvirt-clients bridge-utils virt-manager
systemctl reboot

```

---

## ⚙️ 2. Configurar permissões do usuário

> [!tip] Para gerenciar suas VMs de forma nativa, ágil e segura com o seu próprio usuário, adicione sua conta aos grupos libvirt e kvm.

### Fedora

```bash
sudo usermod -aG libvirt $USER
systemctl reboot

```

### Ubuntu

```bash
sudo usermod -aG libvirt $USER
sudo usermod -aG kvm $USER
systemctl reboot

```

---

## 📦 3. Instalar QEMU Guest Agent

### Fedora

```bash
sudo dnf install -y qemu-guest-agent

```

### Ubuntu

```bash
sudo apt install -y qemu-guest-agent

```

---

## 🔗 Notas Relacionadas
- [Windows 11 no KVM](06_virtualizacao_win11_kvm.md) — Configuração de VM Windows 11 com drivers VirtIO.
- [Containers com Distrobox e Docker](04_containers_distrobox_docker.md) — Solução leve de isolamento de processos.
- [Omarchy: Pós-instalação](02_omarchy_pos_instalacao.md) — Permissões de grupos e suporte a virtualização.
