<div align="center">

# ⚡ NexFlow Server

### *Motor Profissional de Renderização em Lote e Orquestração para Adobe After Effects*

[![Latest Release](https://img.shields.io/github/v/release/sidneyts/Nexflow-Server-Releases?style=for-the-badge&color=blue&label=Vers%C3%A3o%20Est%C3%A1vel)](https://github.com/sidneyts/Nexflow-Server-Releases/releases/latest)
[![Plataformas](https://img.shields.io/badge/Plataformas-Windows%20%7C%20macOS-informational?style=for-the-badge&logo=windows&logoColor=white)](https://github.com/sidneyts/Nexflow-Server-Releases/releases)
[![After Effects](https://img.shields.io/badge/Adobe%20After%20Effects-2021%20a%202025-blueviolet?style=for-the-badge&logo=adobeaftereffects&logoColor=white)](https://www.adobe.com/products/aftereffects.html)
[![Licença](https://img.shields.io/badge/Licen%C3%A7a-Propriet%C3%A1ria%20%2F%20Enterprise-success?style=for-the-badge)](https://nexflowstudio.com)

<p align="center">
  <b>O agente desktop de alta performance que conecta o <a href="https://github.com/sidneyts/NexFlow-Studio">NexFlow Studio Web</a> à capacidade máxima de computação local do seu After Effects e FFmpeg.</b>
</p>

---

</div>

## 📖 O que é o NexFlow Server?

O **NexFlow Server** é a aplicação desktop oficial do ecossistema **NexFlow**, desenvolvida para atuar como o **motor de renderização e automação de vídeo** em estações de trabalho de produção e servidores dedicados (*render farms* locais).

Em ambientes de broadcast, jornalismo diário, agências e digital signage, a renderização de vídeos em alta resolução (4K, Full HD, verticais e formatos compostos como 3D/L3D) exige processamento gráfico pesado, fontes personalizadas e acesso a projetos locais do After Effects. 

Em vez de depender de servidores em nuvem lentos ou caros para processamento de vídeo, o **NexFlow Server** permite que sua equipe configure suas próprias máquinas de renderização locais. Ele se conecta silenciosamente ao **NexFlow Studio Web**, escuta os jobs de renderização criados pelos operadores em tempo real, executa a montagem e injeção de ativos no After Effects e entrega os vídeos finais prontos para exibição.

---

## 🔄 Fluxo de Trabalho e Arquitetura

```
┌─────────────────────────────────┐
│     NexFlow Studio (Web PWA)    │
│  - Edição de Matérias           │
│  - Automação de Textos e Mídias │
│  - Disparo de Render            │
└────────────────┬────────────────┘
                 │ (WebSockets / Pusher / Firestore)
                 ▼
┌────────────────────────────────────────────────────────┐
│              NexFlow Server (Desktop App)              │
│  1. Recebe o Job de Render em tempo real               │
│  2. Baixa mídias, fontes e metadados com cache         │
│  3. Prepara a pasta do job (Nomenclatura Legível)      │
│  4. Executa script JSX via aerender (After Effects)    │
│  5. Codifica e normaliza aspect ratio com FFmpeg       │
│  6. Sincroniza progresso quadro a quadro com o Studio  │
└────────────────┬───────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────┐
│    Vídeo Final Pronto no Disco  │
│  - Arquivo MP4 / MOV / WebM     │
│  - Metadados offline gravados   │
│  - Upload opcional para Storage │
└─────────────────────────────────┘
```

---

## 🚀 Principais Recursos

- ⚡ **Integração Nativa com Adobe After Effects:** Orquestração direta com o executável `aerender` do After Effects (suporte às versões 2021, 2022, 2023, 2024 e 2025).
- 📡 **Comunicação em Tempo Real:** Sincronização instantânea via WebSockets e Pusher com o painel web do NexFlow Studio, transmitindo progresso percentual, frames renderizados e status da fila.
- 🗂️ **Nomenclatura Humanamente Legível:** Pastas de trabalho nomeadas de forma clara e padronizada (`DDMMYYYY_TEMPLATE_FORMATO_INSTANCIA_shortid`), eliminando UUIDs ilegíveis e facilitando a localização de qualquer trabalho no disco.
- 🧹 **Gerenciador de Armazenamento e Limpeza Automática:** Serviço inteligente em segundo plano que monitora o espaço em disco e remove arquivos temporários antigos de acordo com a política de retenção configurada (1 a 30 dias), com trava de segurança para nunca interromper um render em execução.
- 🔤 **Download e Resolução Automática de Tipografia:** Identifica fontes ausentes no projeto e realiza o download automático em tempo real para o sistema operacional antes de disparar o render.
- 🛡️ **Metadados Offline de Diagnóstico:** Cada pasta de renderização armazena um arquivo `job-metadata.json` completo para auditoria independente da conexão com a nuvem.
- 🖥️ **Interface Moderna e Amigável:** Painel desktop com visualização clara da fila de jobs, botões de acesso direto às pastas no Explorador de Arquivos / Finder e monitor de status do After Effects.
- 🔄 **Atualizações Automáticas (Auto-Update):** Notificação e instalação de novas versões com um único clique.

---

## 📥 Download e Instalação

Baixe a versão mais recente diretamente na aba de [Releases](https://github.com/sidneyts/Nexflow-Server-Releases/releases/latest):

| Sistema Operacional | Arquitetura | Instalador Oficial |
| :--- | :--- | :--- |
| **Windows 10 / 11** | 64-bit (x64) | [💾 Baixar NexFlow Server (.exe)](https://github.com/sidneyts/Nexflow-Server-Releases/releases/latest) |
| **macOS (Apple Silicon)** | M1 / M2 / M3 / M4 (arm64) | [🍎 Baixar NexFlow Server (.dmg)](https://github.com/sidneyts/Nexflow-Server-Releases/releases/latest) |
| **macOS (Intel)** | Intel x64 | [🍏 Baixar NexFlow Server (.dmg)](https://github.com/sidneyts/Nexflow-Server-Releases/releases/latest) |
| **macOS Portátil** | Universal (.zip) | [📦 Baixar NexFlow Server (.zip)](https://github.com/sidneyts/Nexflow-Server-Releases/releases/latest) |

---

## ⚙️ Requisitos do Sistema

### 🖥️ Hardware Recomendado
- **Processador:** Intel Core i7 / AMD Ryzen 7 ou Apple Silicon (M1 Pro/Max/Ultra, M2, M3, M4).
- **Memória RAM:** Mínimo de 16 GB (32 GB ou mais recomendado para renders simultâneos e 4K).
- **Armazenamento:** SSD NVMe com pelo menos 20 GB de espaço livre para cache e saída de render.

### 📦 Software Necessário
- **Adobe After Effects:** Versão 2021 ou superior instalada na máquina.
- **Configuração Obrigatória no After Effects:**
  1. Abra o After Effects.
  2. Acesse `Editar > Preferências > Scripting & Expressões` (no macOS: `After Effects > Preferências > Scripting & Expressões`).
  3. Marque a caixa: **"Permitir que Scripts Grave Arquivos e Acessem a Rede"**.
  4. Clique em **OK**.

---

## 🚀 Como Usar (Passo a Passo)

1. **Instale e Abra o Aplicativo:** Execute o instalador baixado para seu sistema operacional.
2. **Conecte à Empresa:** Insira as credenciais ou a chave do servidor configurada no painel administrativo do NexFlow Studio.
3. **Deixe o Servidor Online:** A interface indicará o status em verde (*"Servidor Conectado & Aguardando Jobs"*).
4. **Dispare Renders pelo Studio Web:** Qualquer renderização enviada pela sua equipe na plataforma web será recebida e processada automaticamente pela máquina local.
5. **Acompanhe a Fila:** Visualize o progresso em tempo real e abra a pasta do vídeo renderizado com um único clique no botão de pasta.

---

## 📋 Registro de Mudanças (Changelog)

Todas as versões e melhorias são documentadas com riqueza de detalhes técnicos, notas de compatibilidade e validação de qualidade:

👉 **[Acesse o Histórico Completo de Versões e Notas de Release](https://github.com/sidneyts/Nexflow-Server-Releases/releases)**

---

<div align="center">
  <p><sub>Desenvolvido com excelência pela equipe <b>NexFlow</b> • Plataforma de Automação de Vídeo</sub></p>
</div>
