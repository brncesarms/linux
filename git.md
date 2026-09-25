---
title: "Git: Instalação e Configuração"
date_created: 2026-08-17
tags:
  - linux/git
  - dev/git
---

# 🔧 Git: Instalação e Configuração

> [!info] Instalação e configuração básica do Git no Fedora e Ubuntu para controle de versão e repositórios.

---

## 📦 1. Instalar o Git

- **Fedora**
```bash
sudo dnf install -y git

```

- **Ubuntu**
```bash
sudo apt install -y git

```

---

## ⚙️ 2. Configurar o Git

> [!warning] Substitua pelos seus dados
> Use o e-mail e o nome de usuário da sua conta do GitHub/GitLab. Para ocultar o seu e-mail pessoal no GitHub, você pode usar o e-mail de privacidade gerado pela plataforma (`<id>+<seu-nome>@users.noreply.github.com`).

```bash
git config --global user.email "SEU_EMAIL@exemplo.com"
git config --global user.name "SEU_USUARIO"
```

## 🔗 Notas Relacionadas
- [Linux: Atualizar Pacotes](1-atualizar-pacotes.md) — Comandos para atualizar pacotes no Fedora e Ubuntu.
- [Linux: Homebrew](homebrew.md) — Instalação do Homebrew para gerenciar pacotes sem sudo.
