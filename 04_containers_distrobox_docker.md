---
title: "Containers: Distrobox e Docker"
date_created: 2026-08-28
author: "Bruno César"
privacy: public
tags:
  - publico
  - linux/containers
  - linux/docker
  - linux/distrobox
---

# 📦 Containers: Distrobox e Docker

> [!info] Guia completo de gerenciamento de containers usando Distrobox (Podman/Docker) e Docker no Fedora e Ubuntu, incluindo criação, execução e remoção.

---

## 🔧 Comandos Essenciais

### Distrobox

| Comando | Função |
|---|---|
| `distrobox create` | Cria um container padrão do Distrobox |
| `distrobox enter` | Entra no container padrão |
| `distrobox enter <nome> -- <comando>` | Executa um comando dentro do container |
| `distrobox list` | Lista todos os containers criados |
| `distrobox stop <nome>` | Para um container em execução |
| `distrobox rm <nome>` | Remove permanentemente um container |

> [!info] Mais informações: [Documentação oficial do Distrobox](https://distrobox.it)

### Docker

| Comando | Função |
|---|---|
| `docker create --name <nome> <imagem>` | Cria um container a partir de uma imagem |
| `docker exec -it <nome> bash` | Entra no container em execução |
| `docker exec <nome> <comando>` | Executa um comando em container rodando |
| `docker ps -a` | Lista todos os containers |
| `docker images` | Lista as imagens baixadas |
| `docker rm <nome>` | Remove permanentemente um container |

> [!tip] O **Distrobox** gerencia a inicialização do container de forma transparente (uso o Podman ou Docker por baixo). No Docker, o container precisa estar rodando para usar `docker exec`. Se estiver parado, use `docker start <nome>` antes.

---

## 📦 1. Criando Container

### Distrobox

```bash
# Distrobox: criando container do ubuntu
distrobox create -n NOME_CONTAINER --image ubuntu:24.04

```

### Docker

```bash
# Docker: criando container do ubuntu
docker run -it --name NOME_CONTAINER ubuntu:24.04

```

### Docker (Equivalente Completo ao Distrobox)

```bash
# Equivalente Completo (Estilo Distrobox com Integração ao Host)
docker create --name NOME_CONTAINER2 \
  --net=host \
  --ipc=host \
  -v /dev:/dev \
  -v $HOME:$HOME \
  -w $HOME \
  -e DISPLAY=$DISPLAY \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  -it ubuntu:24.04

```

> [!info] O `distrobox` compartilha automaticamente com o container a sua pasta pessoal (`$HOME`), a rede do host, dispositivos de hardware, servidor de áudio e interface gráfica (X11/Wayland).

---

## 🚀 2. Entrando no Container

### Distrobox

```bash
# Distrobox: entrando no container
distrobox enter NOME_CONTAINER

```

### Docker

```bash
# 1. Docker: Se o container já estiver rodando
docker exec -it NOME_CONTAINER bash

```

```bash
# 2. Docker: Se o container estiver parado
docker start NOME_CONTAINER && docker exec -it NOME_CONTAINER bash

```

> [!tip] Se o container for de uma imagem enxuta sem `bash` (como Alpine Linux), substitua `bash` por `sh`: `docker exec -it NOME_CONTAINER sh`.

---

## ⏹️ 3. Parar Container

### Distrobox

```bash
# Distrobox: parar container
distrobox stop NOME_CONTAINER

```

### Docker

```bash
# Docker: parar container
docker stop ID_CONTAINER

```

---

## 🗑️ 4. Removendo Container

### Distrobox

```bash
# Distrobox: removendo container do ubuntu
distrobox rm -f NOME_CONTAINER

```

### Docker

```bash
# Docker: removendo container do ubuntu
docker rm -f NOME_CONTAINER

```

---

## 🖥️ 5. Rodando Aplicativo dentro do Container

### Distrobox

```bash
# atalho: abrindo google chrome dentro do container do ubuntu
distrobox enter NOME_CONTAINER -- /usr/bin/google-chrome-stable

```

### Distrobox (Exportando o Aplicativo para o Host)

```bash
# dentro do container, exporta o app para o menu de aplicativos do host
distrobox-export --app /usr/bin/google-chrome-stable

```

> [!tip] Após exportar, o aplicativo aparece no menu de aplicativos e pode ser aberto como um programa nativo do sistema, sem precisar entrar no container primeiro.

### Docker

```bash
# atalho: abrindo google chrome dentro do container, se já estiver rodando
docker exec -d NOME_CONTAINER /usr/bin/google-chrome-stable

```

```bash
# atalho: abrindo google chrome dentro do container, se estiver parado
docker start NOME_CONTAINER && docker exec -d NOME_CONTAINER /usr/bin/google-chrome-stable

```

> [!warning] Para aplicativos gráficos (GUI), o container deve ter sido criado com permissões de vídeo/display compartilhadas com o host (`-e DISPLAY=$DISPLAY` e `-v /tmp/.X11-unix:/tmp/.X11-unix`). Execute `xhost +local:docker` no terminal do sistema antes de abrir o aplicativo.

## 🔗 Notas Relacionadas
- [Linux: Virt Manager](./05_virtualizacao_virt_manager.md) — Instalação e configuração do Virt Manager para virtualização.
- [Linux: Pós-instalação do Fedora](./03_fedora_pos_instalacao.md) — Guia completo de configuração após instalação do Fedora.
- [T.I. — Mapa de Conteúdo](README.md) — Índice geral.
