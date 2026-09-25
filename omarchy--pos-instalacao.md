---
title: "Omarchy: Pós-instalação"
date_created: 2026-08-28
tags:
  - omarchy
  - arch
  - linux/pos-instalacao
---

# 🌀 Omarchy: Pós-instalação

> [!info] Guia de configuração após uma instalação limpa do Omarchy 4 (Arch Linux + Hyprland), incluindo atualização do sistema, gestão de pacotes, drivers NVIDIA, tema, aplicativos padrão e ajustes.

> [!warning] Substitua `SEU_USUARIO` no hostname do exemplo e `SEU_ID_GITHUB` pelo nome de usuário da sua conta do GitHub.

---

## ℹ️ 0. Verificar a versão

Confirme a versão instalada do Omarchy e o estado do sistema:

```bash
omarchy version
omarchy system stats
omarchy debug --no-sudo --print
```

> [!tip] Sempre use `--no-sudo --print` no `omarchy debug` para evitar prompts interativos que travam o terminal.

---

## 🔄 1. Atualizar o sistema

O Omarchy gerencia a atualização do sistema (pacotes Arch + próprio Omarchy):

```bash
omarchy update
# ou sem confirmação:
omarchy update -y

```

---

## 📦 2. Gestão de pacotes

O Omarchy é baseado em **Arch Linux**, então usa o `pacman` para pacotes oficiais e ferramentas de AUR (`yay`/`paru`) para pacotes da comunidade.

### Pacotes oficiais (Arch)

```bash
# instalar via interface interativa do Omarchy
omarchy pkg install

# ou diretamente com pacman
sudo pacman -S NOME_DO_PACOTE

```

### Pacotes do Omarchy/OPR

```bash
omarchy pkg add NOME_DO_PACOTE

```

### Pacotes da AUR

```bash
omarchy pkg aur add NOME_DO_PACOTE

# interface interativa para escolher pacotes AUR
omarchy pkg aur install

```

### Editores de texto

> [!warning] O Omarchy **não vem com o `nano` instalado por padrão** — apenas o Neovim (`nvim`). Se preferir um editor mais simples, instale o `nano`:

```bash
sudo pacman -S nano

```

> [!tip] Escolha e defina o seu editor padrão do Omarchy (o Neovim já é o padrão atual):

```bash
omarchy default editor nvim    # Neovim
omarchy default editor vim     # Vim (se instalado)
omarchy default editor emacs   # Emacs

```

---

## 🎮 3. Drivers NVIDIA e GPU híbrida

> [!warning] Em notebooks com **GPU Intel + NVIDIA** (como este: iGPU Intel Raptor Lake + RTX 5060 Max-Q), o Omarchy usa Wayland/Hyprland com aceleração de hardware.

### Verificar a GPU detectada

```bash
lspci | grep -iE 'vga|3d|display'

```

### Instalar drivers NVIDIA (novo driver open source)

```bash
sudo pacman -S nvidia-open nvidia-utils xorg-xwayland

```

### Habilitar o serviço de persistência (se necessário para carregamento)

```bash
sudo systemctl enable --now nvidia-suspend.service nvidia-resume.service nvidia-hibernate.service

```

> [!tip] Depois de instalar os drivers, **reinicie** o sistema para carregar o módulo NVIDIA no kernel.

### Codecs multimídia

Para reprodução de vídeo e codecs proprietários:

```bash
sudo pacman -S ffmpeg libva-utils vulkan-icd-loader

```

---

## 🎨 4. Tema e aparência

O tema atual do sistema é **Tokyo Night**. Altere o tema a qualquer momento:

```bash
omarchy theme list
omarchy theme set NOME_DO_TEMA

```

> [!info] O shell (barra de status, notificações, OSD) e os terminais são recarregados automaticamente ao trocar de tema.

### Escala de texto

```bash
omarchy display text size 1.10   # ajuste ao seu monitor
omarchy display text size reset  # volta ao padrão

```

---

## 🧰 5. Aplicativos padrão

### Definir aplicativos padrão

```bash
omarchy default terminal kitty           # terminal já configurado (kitty)
omarchy default editor nvim              # editor já configurado (neovim)
omarchy default browser brave            # navegador já configurado (Brave)

```

### Instalar aplicativos populares de forma opcional

```bash
omarchy install browser firefox
omarchy install editor vscode
omarchy install editor zed

```

### Ambientes de desenvolvimento

```bash
omarchy install dev-env node
omarchy install dev-env python
omarchy install dev-env rust
omarchy install docker dbs   # bancos de dados via Docker

```

---

## 🖥️ 6. Relógio, idioma e localização

### Definir idioma/teclado

```bash
omarchy setup keyboard

```

> [!info] O setup interativo do Omarchy também inclui opções de segurança como senha do usuário e autenticação por impressão digital (`omarchy setup security fingerprint`).

---

## 📸 7. Capturas e gravação de tela

```bash
omarchy capture screenshot          # captura de tela
omarchy capture screenrecording --fullscreen   # gravação da tela
omarchy capture text                # extrai texto de uma captura (OCR)

```

---

## 🧹 8. Referência rápida de comandos do sistema

| Ação | Comando |
|---|---|
| Reiniciar | `omarchy system reboot` |
| Desligar | `omarchy system shutdown` |
| Logout | `omarchy system logout` |
| Bloquear tela | `omarchy system lock` |
| Atualizar sistema | `omarchy update` |
| Status (CPU/memória) | `omarchy system stats` |
| Resetar config p/ padrão | `omarchy refresh <app>` |

## 🔗 Notas Relacionadas
- [Linux: Atualizar Pacotes](1-atualizar-pacotes.md) — Comandos para atualizar pacotes no Fedora e Ubuntu.
- [Linux: FFmpeg com NVIDIA](ffmpeg.md) — Transcodificação de vídeo com aceleração NVENC.
- [Containers: Distrobox e Docker](containers--distrobox-docker-v2.md) — Gerenciamento de containers.
