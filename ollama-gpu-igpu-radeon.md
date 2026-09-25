---
title: "Ativar GPU iGPU (Radeon 780M) no Ollama"
date_created: 2026-09-04
tags:
  - linux
  - ollama
  - gpu
  - amd
---

# 🎮 Ativar GPU iGPU (Radeon 780M) no Ollama

> 💡 **Lição aprendida em 2026-09-04**: o Ollama **descarta iGPUs por padrão** (AMD/Intel integradas). Se a máquina só tem iGPU (ex: Radeon 780M do GEEKOM A7 MAX), o modelo roda **100% na CPU** silenciosamente.

## 🚨 Sintoma

- `ollama ps` mostra `100% CPU` no PROCESSOR
- Log diz:

```
msg="dropping integrated GPU; to enable, set OLLAMA_IGPU_ENABLE=1" id=0 library=Vulkan
description="AMD Radeon 780M Graphics (RADV PHOENIX)"
```

## ✅ Solução

Adicionar a variável de ambiente ao serviço/daemon do Ollama:

```ini
Environment="OLLAMA_IGPU_ENABLE=1"
```

Exemplo com systemd user service:

```ini
[Service]
Environment="OLLAMA_HOST=127.0.0.1:11434"
Environment="OLLAMA_KEEP_ALIVE=2h"
Environment="OLLAMA_IGPU_ENABLE=1"
ExecStart=/usr/local/bin/ollama serve
```

Depois:

```bash
systemctl --user daemon-reload
systemctl --user restart ollama.service
```

## ⚠️ Cuidados aprendidos

- **Não defina `OLLAMA_LLM_LIBRARY` para uma pasta customizada** (ex: libs ROCm baixadas) — isso quebrou o *discovery* Vulkan e a GPU deixou de ser detectada. O backend Vulkan do sistema (`/usr/local/lib/ollama/vulkan/libggml-vulkan.so`) já resolve a 780M.
- A Radeon 780M roda via **Vulkan (RADV PHOENIX)** — sem precisar de pacote ROCm extra.
- Pacote ROCm cru do Ollama (`ollama-linux-amd64-rocm.tar.zst`) não trouxe ganho aqui; só gigabytes desperdiçados (~8.5GB limpos depois).

## 🔍 Verificação

```bash
ollama ps
# PROCESSOR deve mostrar: 100% GPU
```

---

## 🔗 Fontes
- [Ollama Docs — GPU FAQ](https://github.com/ollama/ollama/blob/main/docs/gpu.md)
- [Ollama — problema de iGPU (GitHub #issues)](https://github.com/ollama/ollama/issues)