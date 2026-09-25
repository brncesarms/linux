---
title: "Linux Systems Engineering, Virtualization & Containerization Runbooks"
date_created: 2026-08-17
author: "Bruno César / Antigravity"
privacy: public
tags:
  - publico
  - linux
  - arch
  - omarchy
  - fedora
  - docker
  - kvm
  - devops
---

# 🐧 Linux Systems Engineering, Virtualization & Containers

[![Platform](https://img.shields.io/badge/OS-Arch%20%7C%20Omarchy%20%7C%20Fedora%20%7C%20Ubuntu-1793D1?logo=linux&logoColor=white)](#)
[![Compositor](https://img.shields.io/badge/Wayland-Hyprland%20v0.40%2B-00ADD8?logo=wayland&logoColor=white)](#)
[![Containers](https://img.shields.io/badge/Containers-Docker%20%7C%20Distrobox-2496ED?logo=docker&logoColor=white)](#)
[![Virtualization](https://img.shields.io/badge/Hypervisor-KVM%20%7C%20QEMU%20%7C%20Virt--Manager-FF6600)](#)
[![Hardware Acceleration](https://img.shields.io/badge/Hardware%20Accel-NVIDIA%20NVENC%20%7C%20AMD%20ROCm-76B900?logo=nvidia&logoColor=white)](#)
[![Obsidian](https://img.shields.io/badge/Knowledge%20Base-Obsidian-483699?logo=obsidian&logoColor=white)](#)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](#)

> [!NOTE]
> **Repositório Oficial de Engenharia de Sistemas Linux**  
> Runbooks determinísticos de pós-instalação, hardening, ambientes Wayland/Hyprland modernos, isolamento de containers (Docker/Distrobox), hipervisores KVM/QEMU de alta performance e aceleração de IA e GPU (NVIDIA NVENC & AMD ROCm).

---

## 🎯 Visão Geral & Filosofia de Infraestrutura

Este repositório consolida procedimentos de engenharia e runbooks operacionais para estações de trabalho e hosts Linux de alta performance. Adotamos o paradigma de **sistemas reprodutíveis, isolamento em camadas e aceleração de hardware dedicada**, abrangendo desde distribuições rolling-release (Arch/Omarchy Linux) até estações de ciclo fixo (Fedora Workstation).

### Principais Pilares
1. **Ambientes Modernos Wayland**: Configuração avançada de compositores Wayland (Hyprland), suporte a WayVNC para administração remota e aceleração gráfica nativa.
2. **Isolamento de Cargas de Trabalho**: Utilização de Distrobox sobre Docker/Podman para executar dependências legadas e utilitários de compilação sem poluir o sistema operacional host.
3. **Hipervisores Paravirtualizados**: Implantação de VMs KVM/QEMU com barramento VirtIO, suporte a TPM 2.0 (`swtpm`) e UEFI/OVMF para máxima proximidade do hardware bare-metal.
4. **Aceleração Gráfica & Computação Heterogênea**: pipelines de transcodificação de mídia com NVIDIA NVENC e inferência local de Modelos de Linguagem (LLMs) em iGPUs AMD Radeon via ROCm/HSA.

---

## 📚 Índice Temático dos Runbooks

### 🌀 1. Sistemas Operacionais & Ambientes de Trabalho (OS & Desktops)
| Runbook | Descrição | Tecnologias |
| :--- | :--- | :--- |
| [**02. Pós-instalação do Omarchy**](02_omarchy_pos_instalacao.md) | Setup completo do Omarchy 4 (Arch Linux + Hyprland), firewall UFW, áudio PipeWire, drivers e apps. | `Omarchy`, `Arch`, `Hyprland`, `Wayland` |
| [**03. Pós-instalação do Fedora**](03_fedora_pos_instalacao.md) | Otimização do Fedora Workstation: RPM Fusion, drivers proprietários, paralelismo DNF e Flatpaks. | `Fedora`, `dnf`, `RPM Fusion`, `Flatpak` |
| [**01. Atualizar Pacotes Multi-Distro**](01_atualizar_pacotes.md) | Procedimentos padronizados de sincronização e atualização de pacotes no Omarchy, Fedora e Ubuntu. | `omarchy update`, `pacman`, `dnf`, `apt` |

### 📦 2. Containers & Isolamento de Ambientes
| Runbook | Descrição | Tecnologias |
| :--- | :--- | :--- |
| [**04. Containers com Distrobox e Docker**](04_containers_distrobox_docker.md) | Criação de subsistemas isolados (Ubuntu/Arch/Alpine) integrados ao home do usuário via Distrobox. | `Distrobox`, `Docker`, `OCI Containers` |

### 🖥️ 3. Virtualização & Hipervisores Locais (KVM/QEMU)
| Runbook | Descrição | Tecnologias |
| :--- | :--- | :--- |
| [**05. Virt-Manager & Hipervisor KVM**](05_virtualizacao_virt_manager.md) | Configuração da stack de virtualização KVM, QEMU, libvirt e grupos de segurança sem necessidade de root. | `libvirt`, `KVM`, `QEMU`, `Virt-Manager` |
| [**06. Windows 11 no KVM**](06_virtualizacao_win11_kvm.md) | Provisionamento de máquina virtual Windows 11 com drivers paravirtualizados VirtIO e vTPM. | `VirtIO`, `Windows 11`, `swtpm`, `OVMF` |

### ⚡ 4. Aceleração Gráfica, Multimídia & Inteligência Artificial
| Runbook | Descrição | Tecnologias |
| :--- | :--- | :--- |
| [**08. FFmpeg com Aceleração NVIDIA NVENC**](08_ffmpeg_nvenc_transcodificacao.md) | Transcodificação de vídeo de altíssima velocidade utilizando os encoders dedicados NVENC da NVIDIA. | `FFmpeg`, `NVENC`, `H.264 / HEVC` |
| [**09. Aceleração iGPU Radeon 780M no Ollama**](09_ollama_igpu_radeon_rocm.md) | Configuração de variáveis HSA e ROCm para rodar modelos locais na GPU integrada AMD Radeon. | `Ollama`, `AMD ROCm`, `HSA_OVERRIDE` |

### 🌐 5. Redes, Gerenciadores de Pacote & Ferramentas Dev
| Runbook | Descrição | Tecnologias |
| :--- | :--- | :--- |
| [**07. Varredura e Seleção de Canais Wi-Fi**](07_wifi_varredura_canais_nmcli.md) | Diagnóstico espectral de RF e seleção do melhor canal sem fio via NetworkManager CLI (`nmcli`). | `nmcli`, `NetworkManager`, `Wi-Fi 5GHz` |
| [**10. Gerenciador de Pacotes Homebrew**](10_homebrew_gerenciador_pacotes.md) | Instalação e uso do Linuxbrew para gestão de utilitários CLI em espaço de usuário sem sudo. | `Homebrew`, `Linuxbrew` |
| [**11. Instalação e Configuração do Git**](11_git_instalacao_configuracao.md) | Setup de credenciais, chaves criptográficas SSH Ed25519 e aliases produtivos para controle de versão. | `git`, `ssh-keygen`, `ed25519` |

---

## 🛠️ Como Utilizar este Repositório

### Clonagem Local
```bash
git clone git@github.com:brncesarms/linux.git
cd linux
```

### Visualização Recomendada
- **Obsidian**: Abra a pasta como um vault local para explorar conexões em grafo e links bidirecionais entre os runbooks.
- **Terminal CLI**: Os scripts e blocos de comandos foram desenhados para execução rápida via terminal Linux.

---

## 🤝 Conexão com a Caixa de Ferramentas Multiplataforma

Os scripts shell (`.sh`) e automações correspondentes a estes procedimentos estão centralizados em nosso repositório canônico de scripts:
🔗 **[Repositório brncesarms/scripts (Bash)](https://github.com/brncesarms/scripts/tree/main/bash)**

---

## 👤 Autor

**Bruno César**  
*Engenheiro de Infraestrutura, Redes & Automação*  
- **GitHub**: [@brncesarms](https://github.com/brncesarms)
- **LinkedIn**: [linkedin.com/in/brncesarms](https://linkedin.com/in/brncesarms)
