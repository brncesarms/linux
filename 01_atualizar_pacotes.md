---
title: "Linux: Atualizar Pacotes"
date_created: 2026-08-17
author: "Bruno César"
privacy: public
tags:
  - publico
  - linux/atualizacao
  - linux/fedora
  - linux/ubuntu
---

# 🔄 Linux: Atualizar Pacotes

> [!info] Comandos para atualizar pacotes no Fedora e Ubuntu, garantindo que o sistema esteja sempre na versão mais recente.

---

## 🌀 Omarchy & Arch Linux

> [!info] O Omarchy unifica as atualizações do sistema base Arch, pacotes AUR e utilitários de ambiente via ferramenta nativa `omarchy` ou `pacman`.

```bash
# Atualização completa recomendada do ecossistema Omarchy:
omarchy update -y

# Atualização nativa dos repositórios oficiais do Arch Linux:
sudo pacman -Syu
```

---

## 🐧 Fedora

> [!info] O pull mais recente das atualizações de segurança (Fastest Mirror + 10 downloads paralelos configurado no pós-instalação).

```bash
sudo dnf upgrade --refresh
```

> [!tip] Para atualizar para uma nova versão do Fedora, use o plugin de upgrade de sistema:
> ```bash
> sudo dnf system-upgrade reboot
> ```

---

## 🟠 Ubuntu

```bash
sudo apt update && sudo apt upgrade -y && sudo apt dist-upgrade -y
```

> [!tip] Após o término, é recomendado reiniciar o computador se houver atualização de kernel:
> ```bash
> systemctl reboot
> ```

## 🔗 Notas Relacionadas
- [Linux: Pós-instalação do Fedora](03_fedora_pos_instalacao.md) — Guia completo de configuração após instalação do Fedora.
- [Linux: Homebrew](10_homebrew_gerenciador_pacotes.md) — Instalação do Homebrew para gerenciar pacotes sem sudo.
