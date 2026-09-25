---
title: "Fedora: Pós-instalação"
date_created: 2026-08-17
author: "Bruno César"
privacy: public
tags:
  - publico
  - linux/fedora
  - linux/pos-instalacao
---

# 🐧 Fedora: Pós-instalação

> [!info] Guia de configuração após uma instalação limpa do Fedora 44, incluindo otimizações do DNF, RPM Fusion, Flathub e drivers NVIDIA.

---

## 📜 1. Script automático

> [!tip] Script de pós-instalação
> Substitua `SEU_USUARIO` pela sua conta do GitHub no comando abaixo:

```bash
sudo bash -c "$(wget -qO- https://raw.githubusercontent.com/SEU_USUARIO/linux_fedora_pos_instalacao/refs/heads/main/linux_fedora_pos_instalacao.sh)"
```

---

## ⚙️ 2. Configurar o DNF

Edite o arquivo:

```bash
sudo nano /etc/dnf/dnf.conf

```

Adicione abaixo de `[main]`:

```bash
fastestmirror=True
max_parallel_downloads=10
defaultyes=True
keepcache=True

```

| Opção | Descrição |
|---|---|
| `fastestmirror` | Usa o espelho mais rápido |
| `max_parallel_downloads` | Baixa até 10 pacotes simultaneamente |
| `defaultyes` | Aceita confirmações automaticamente |
| `keepcache` | Mantém o cache dos pacotes |

---

## 🔄 3. Atualizar o sistema

```bash
sudo dnf -y update

```

---

## 📦 4. Ativar RPM Fusion e codecs

```bash
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

```

---

## 📦 5. Ativar o Flathub

```bash
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

```

```bash
sudo dnf swap ffmpeg-free ffmpeg --allowerasing
sudo systemctl reboot

```

```bash
sudo dnf group upgrade core

```

---

## 🎮 6. Drivers NVIDIA

> [!warning] Para sistemas com placa de vídeo NVIDIA, instale os drivers proprietários correspondentes.

### RTX

```bash
sudo dnf install akmod-nvidia

```

### GTX

```bash
sudo dnf install akmod-nvidia-580xx

```

### CUDA

```bash
sudo dnf install xorg-x11-drv-nvidia-cuda

```

## 🔗 Notas Relacionadas
- [Linux: FFmpeg com NVIDIA](08_ffmpeg_nvenc_transcodificacao.md) — Transcodificação de vídeo com aceleração NVENC.
- [Linux: Atualizar Pacotes](01_atualizar_pacotes.md) — Comandos para atualizar pacotes no Fedora e Ubuntu.
- [Linux: Virt Manager](05_virtualizacao_virt_manager.md) — Instalação e configuração do Virt Manager para virtualização.
