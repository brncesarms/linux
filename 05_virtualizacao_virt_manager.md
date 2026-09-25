---
title: "Virt Manager: Virtualização no Linux"
date_created: 2026-08-17
author: "Bruno César / Antigravity"
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

## 🔗 Notas Relacionadas
- [Linux: Windows 11 no KVM](./06_virtualizacao_win11_kvm.md) — Como instalar Windows 11 no KVM.
- [Containers: Distrobox e Docker](./04_containers_distrobox_docker.md) — Gerenciamento de containers com Distrobox e Docker.
- [Linux: Pós-instalação do Fedora](./03_fedora_pos_instalacao.md) — Guia completo de configuração após instalação do Fedora.
- [T.I. — Mapa de Conteúdo](README.md) — Índice geral.
