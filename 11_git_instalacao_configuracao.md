---
title: "Git: Instalação e Configuração"
date_created: 2026-08-17
author: "Bruno César"
privacy: public
tags:
  - publico
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

---

## 🔗 Notas Relacionadas
- [Omarchy: Pós-instalação](02_omarchy_pos_instalacao.md) — Ambiente de desenvolvimento e chave SSH.
- [Homebrew: Gerenciador de Pacotes](10_homebrew_gerenciador_pacotes.md) — Instalação de utilitários auxiliares (gh, delta).
- [Guia Principal de Linux](README.md) — Índice geral.
