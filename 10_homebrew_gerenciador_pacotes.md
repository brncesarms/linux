---
title: "Homebrew: Gerenciador de Pacotes para Linux"
date_created: 2026-08-17
author: "Bruno César"
privacy: public
tags:
  - publico
  - linux/homebrew
  - linux/gerenciador-pacotes
---

# 🍺 Homebrew: Gerenciador de Pacotes para Linux

> [!info] Instalação e configuração do Homebrew (Linuxbrew) no Fedora e Ubuntu para instalar ferramentas de linha de comando sem precisar de sudo.

---

## 📦 1. Instalar dependências

- **Fedora**
```bash
sudo dnf group install -y "Development Tools"
sudo dnf install -y procps-ng curl file git

```

- **Ubuntu**
```bash
sudo apt update && sudo apt install -y build-essential procps curl file git

```

---

## 📦 2. Executar o script oficial do Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

```

---

## ⚙️ 3. Configurar o PATH no seu terminal

> [!tip] Tanto o Fedora quanto o Ubuntu costumam usar o Bash como shell padrão (ou Zsh se tiver configurado). Adicione o Homebrew às suas variáveis de ambiente executando o comando abaixo.

- **Bash**
```bash
echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> ~/.bashrc
eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"

```

- **Zsh**
```bash
echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> ~/.zshrc
eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"

```

---

## ✅ 4. Pronto para usar!

> [!info] Agora pode instalar qualquer ferramenta de linha de comando sem precisar de sudo.

- Teste a instalação com:
```bash
brew doctor

```

---

## 🔗 Notas Relacionadas
- [Atualizar Pacotes Multi-Distro](01_atualizar_pacotes.md) — Gerenciamento complementar aos pacotes de sistema.
- [Instalação e Configuração do Git](11_git_instalacao_configuracao.md) — Controle de versão e ferramentas CLI.
- [Guia Principal de Linux](README.md) — Índice geral.
