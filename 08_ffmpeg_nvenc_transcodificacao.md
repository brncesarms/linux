---
title: "FFmpeg: Transcodificação de Vídeo com NVIDIA NVENC"
date_created: 2026-08-17
author: "Bruno César"
privacy: public
tags:
  - publico
  - linux/ffmpeg
  - linux/nvidia
  - linux/multimedia
---

# 🎬 FFmpeg: Transcodificação de Vídeo com NVIDIA NVENC

> [!info] Guia completo de transcodificação de vídeo usando FFmpeg com aceleração de hardware NVIDIA RTX, incluindo codecs AV1 e otimizações de qualidade.

---

## 🎥 Comandos Principais

### Sem perda de qualidade

```bash
ffmpeg -i ENTRADA.mp4 -c:v av1_nvenc -preset p7 -cq 26 -filter:v fps=60 -c:a libopus -b:a 128k SAIDA.mkv

```

### Com perda de qualidade (otimizado para tamanho)

```bash
ffmpeg -i ENTRADA.mp4 -c:v av1_nvenc -preset p6 -cq 45 -vf "scale=-1:720,fps=24" -c:a libopus -b:a 32k -ac 1 SAIDA.mkv

```

---

## 🔍 O que cada parte do comando faz

| Parâmetro | Descrição |
|---|---|
| `-i entrada.mp4` | Especifica o arquivo de vídeo original |
| `-c:v av1_nvenc` | Usa o codificador AV1 acelerado pela placa NVIDIA |
| `-preset p7` | Predefinição NVIDIA com ótimo balanço entre qualidade e eficiência |
| `-cq 26` | Qualidade Constante (valores menores = melhor qualidade) |
| `-filter:v fps=60` | Define 60 quadros por segundo no vídeo de saída |
| `-c:a libopus` | Converte áudio para o codec Opus |
| `-b:a 128k` | Taxa de bits do áudio (128 kbps = qualidade transparente) |
| `saida.mkv` | Nome e contêiner do arquivo final |

---

## 📉 Dicas para Reduzir Tamanho do Arquivo

> [!tip] Estas técnicas ajudam a reduzir drasticamente o tamanho do arquivo, mas podem afetar a qualidade.

### 1. Reduzir Resolução (Downscale)

Reduzir de 1080p/4K para 720p corta o tamanho drasticamente:

- Use o filtro: `-vf scale=-1:720`

### 2. Elevar Compressão (CQ 40+)

Quanto maior o número do `-cq`, menor o tamanho final:

- Altere para: `-cq 45`

### 3. Áudio em Mono e Bitrate Mínimo

O codec Opus é extremamente eficiente:

- Use: `-c:a libopus -b:a 32k -ac 1`

### 4. Forçar FPS Menor

Forçar 24fps economiza espaço significativamente:

- Use: `-filter:v fps=24`

---

## ⚠️ Configuração NVIDIA no Fedora

> [!warning] Para que a aceleração por hardware funcione, é necessário instalar os drivers proprietários da NVIDIA.

### 1. Atualizar sistema e adicionar repositórios

```bash
sudo dnf -y update

```

```bash
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

```

### 2. Trocar ffmpeg-free por ffmpeg completo

```bash
sudo dnf swap ffmpeg-free ffmpeg --allowerasing

```

| Comando | Função |
|---|---|
| `sudo` | Executa com privilégios de superusuário |
| `dnf` | Gerenciador de pacotes do Fedora |
| `swap` | Troca um pacote por outro em operação única |
| `ffmpeg-free` | Pacote limitado que será removido |
| `ffmpeg` | Pacote completo que será instalado |
| `--allowerasing` | Permite apagar pacotes conflitantes |

### 3. Atualizar grupos de software

```bash
sudo dnf group upgrade multimedia

```

> [!info] O grupo `multimedia` engloba FFmpeg, reprodutores de vídeo, codecs de áudio e plugins do GStreamer.

```bash
sudo dnf group upgrade core

```

> [!info] O grupo `core` atualiza componentes críticos do sistema (utilitários do kernel, inicialização e ferramentas básicas).

---

## 🔗 Notas Relacionadas
- [Omarchy: Pós-instalação](02_omarchy_pos_instalacao.md) — Drivers proprietários NVIDIA e CUDA.
- [Fedora: Pós-instalação](03_fedora_pos_instalacao.md) — Configuração de codecs RPM Fusion.
- [Guia Principal de Linux](README.md) — Índice geral.
