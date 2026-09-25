---
title: "Tutorial: Varredura e Seleção do Melhor Canal Wi-Fi no Linux com nmcli"
date_created: 2026-08-17
author: "Bruno César"
privacy: public
tags:
  - publico
  - wifi
  - nmcli
  - linux
  - redes
---

# 📶 Guia Prático: Como Escolher o Melhor Canal Wi-Fi no Linux com `nmcli`

Este guia foi estruturado no formato Markdown ideal para ser importado diretamente no seu cofre do **Obsidian**. Ele combina os comandos práticos do `nmcli` com as melhores diretrizes de redes sem fio para otimizar a estabilidade e velocidade da sua rede doméstica.

---

## 🚀 Visão Geral
Para obter a melhor performance no Wi-Fi doméstico, o objetivo principal é **minimizar a interferência** de redes vizinhas e **maximizar a estabilidade** do sinal. O `nmcli` (cliente de linha de comando do NetworkManager) permite escanear o espectro de radiofrequência ao seu redor para identificar quais canais estão congestionados e quais estão livres.

> [!tip] **O que é um canal Wi-Fi?**
> É uma subfrequência específica dentro de uma banda de rádio (como 2.4 GHz ou 5 GHz) utilizada para a transmissão de dados entre o roteador e seus dispositivos.

---

## 🔍 Passo 1: Varredura de Redes ao Redor

O comando básico para listar todos os pontos de acesso (APs) ao seu redor e identificar seus respectivos canais é:

```bash
nmcli device wifi list

```
*(ou de forma abreviada: `nmcli dev wifi`)*

### 🔄 Forçando uma varredura atualizada
Por padrão, o `nmcli` utiliza dados em cache de até 30 segundos. Para forçar o NetworkManager a realizar uma nova varredura física do ambiente antes de exibir os resultados, adicione o parâmetro `--rescan yes`:

```bash
nmcli device wifi list --rescan yes

```

Se preferir realizar apenas a atualização das redes em segundo plano sem exibir a tabela imediatamente, use:
```bash
nmcli device wifi rescan

```

---

## 📊 Passo 2: Filtrando a Saída para Facilitar a Análise

A tabela padrão exibe muitas colunas. Para focar exclusivamente no que importa (Nome da Rede, Endereço Físico, Canal e Força do Sinal), você pode filtrar as colunas usando a opção `--fields` (ou `-f`):

```bash
nmcli -f SSID,BSSID,CHAN,SIGNAL,BAR-SIGNAL device wifi list

```

### Exemplo de saída gerada:
```text
SSID              BSSID              CHAN  SIGNAL  BAR-SIGNAL
MinhaRede_2G      00:11:22:33:44:55  6     95%     ▂▄▆█
Vizinho_A         AA:BB:CC:DD:EE:FF  11    72%     ▂▄▆_
Vizinho_B         11:22:33:44:55:66  4     45%     ▂▄__
```

---

## 🧠 Passo 3: Como Escolher o Canal Ideal

Agora que você tem a lista dos canais utilizados pelos seus vizinhos, siga as diretrizes técnicas abaixo dependendo da frequência da sua rede doméstica:

### 📶 Banda de 2.4 GHz (Mais Alcance, Mais Congestionada)
Na frequência de 2.4 GHz, os canais adjacentes se sobrepõem e causam interferências graves.

> [!important] **A Regra de Ouro da faixa de 2.4 GHz**
> Sempre configure seu roteador para os canais **1**, **6** ou **11**.
> Eles são os únicos três canais nesta faixa que possuem espaço de frequência suficiente para **não se sobreporem**.

*   **Por que evitar canais intermediários (como 2, 3, 4, 5, 7, 8, 9, 10)?**
    Se você utilizar o canal 4, por exemplo, sua rede sofrerá interferência destrutiva tanto de quem usa o canal 1 quanto de quem usa o canal 6. Compartilhar o canal 6 diretamente com um vizinho (interferência co-canal) é tecnicamente muito melhor para a estabilidade do que usar o canal 4 (interferência adjacente).
*   **Largura de Banda:** Configure a largura de banda (Channel Width) do seu roteador em **20 MHz** nesta faixa. A largura de 40 MHz em 2.4 GHz interfere com praticamente toda a banda disponível e reduz a estabilidade.

---

### 🚀 Banda de 5 GHz (Mais Velocidade, Menos Interferência)
A frequência de 5 GHz é muito mais ampla e possui até 25 canais de 20 MHz de largura que **não se sobrepõem**.

> [!warning] **O Cuidado com Canais DFS**
> Os canais de 5 GHz entre **52 e 144** são do tipo **DFS** (Dynamic Frequency Selection). Eles compartilham frequência com radares meteorológicos e militares.
> Se o seu roteador estiver em um canal DFS e detectar sinais de radar, ele desconectará os dispositivos temporariamente para trocar de canal de forma abrupta.

*   **Canais Seguros Recomendados (Não-DFS):**
    *   **Faixa Baixa:** 36, 40, 44, 48
    *   **Faixa Alta:** 149, 153, 157, 161, 165
*   **Selecione o canal menos povoado:** Dentre esses canais seguros, escolha aquele que tiver menos redes vizinhas transmitindo ou cujas redes vizinhas tenham o sinal mais fraco (`SIGNAL` mais baixo na saída do `nmcli`).
*   **Largura de Banda:** Se você estiver sofrendo com quedas frequentes, mude a largura de banda do roteador de 80 MHz ou 160 MHz para **40 MHz**. Canais mais largos carregam mais dados, mas captam muito mais ruído de canais adjacentes.

---

## 🛠️ Passo 4: Como Aplicar a Mudança

1. **O `nmcli` não altera as configurações do seu roteador.** O `nmcli` gerencia apenas a recepção do seu dispositivo Linux local.
2. Identifique o melhor canal (ex: canal 11 livre em 2.4 GHz ou canal 44 livre em 5 GHz).
3. Acesse o painel de administração web do seu roteador doméstico (geralmente inserindo o IP do roteador como `192.168.1.1` ou `192.168.0.1` no seu navegador).
4. Navegue até as configurações de **Wi-Fi** / **Wireless**.
5. Altere o campo "Canal" (Channel) de *Auto* para o número que você escolheu e salve as alterações.

---

*Nota: Se você for configurar um Ponto de Acesso (Hotspot) diretamente no próprio computador Linux, aí sim você pode definir o canal via `nmcli` usando:*
```bash
nmcli device wifi hotspot channel <numero_do_canal>
```

---

> [!note] Resumo
> O `nmcli` cuida apenas do lado da recepção do seu dispositivo Linux. A escolha final do canal e da largura de banda é feita no painel administrativo do seu roteador, seguindo a regra dos canais 1/6/11 (2.4 GHz) ou dos canais não-DFS 36-48 e 149-165 (5 GHz).

---

## 🔗 Notas Relacionadas
- [Omarchy: Pós-instalação](02_omarchy_pos_instalacao.md) — Configuração e gestão de adaptadores Wi-Fi.
- [Atualizar Pacotes Multi-Distro](01_atualizar_pacotes.md) — Manutenção de pacotes de rede e firmware.
- [Guia Principal de Linux](README.md) — Índice geral.
