# 🤖 Automação de Atendimento Inteligente: Jira + n8n

[![Jira](https://img.shields.io/badge/Service%20Management-Jira-0052CC?style=for-the-the-badge&logo=atlassian)](https://www.atlassian.com/software/jira)
[![n8n](https://img.shields.io/badge/Workflow-n8n-FF6D5A?style=for-the-the-badge&logo=n8n)](https://n8n.io/)

> **Status do Projeto:** 🟢 Operacional e Publicado

## 📝 Sobre o Projeto
Esta automação foi desenvolvida para otimizar o fluxo de suporte no **Jira Service Management**. O objetivo principal é garantir que cada chamado que entre em "Progresso" receba uma resposta imediata e padronizada, eliminando o erro humano e o envio de mensagens duplicadas (spam).

### 🎯 Problemas Resolvidos
* **Demora no Primeiro Contato:** O robô responde em até 5 minutos.
* **Spam de Comentários:** Implementação de uma "trava lógica" que impede o robô de comentar mais de uma vez no mesmo chamado.
* **Padronização:** Garantia de que todos os clientes recebam a mesma qualidade de atendimento inicial.

---

## 🚀 Como Funciona?
O fluxo de trabalho (Workflow) construído no **n8n** segue quatro etapas fundamentais:

1. **Monitoramento (Schedule):** O robô verifica a fila do Jira a cada 5 minutos.
2. **Filtragem (JQL):** Ele busca apenas chamados onde o status é `Em Progresso`, o responsável é o usuário atual e — o mais importante — a descrição **não contém** o carimbo do robô.
3. **Interação (Add Comment):** Posta automaticamente uma mensagem de boas-vindas e orientações iniciais.
4. **Finalização (Update Issue):** Altera a descrição do chamado para incluir a tag `- comentado_por_dani`. Isso serve como um "selo de lido" para o robô.

---

## 🛠️ Tecnologias Utilizadas
* **Jira Software Cloud:** Gestão de chamados e tickets.
* **n8n (Low-code Automation):** Orquestração dos dados e lógica do robô.
* **JQL (Jira Query Language):** Linguagem de busca para filtragem precisa dos dados.

---

## 📖 Documentação Completa
Para ver o passo a passo detalhado com prints de tela e explicações para iniciantes, acesse nossa página oficial:

👉 **<a href="https://dannyrodrygues.github.io/automacao-Jira-N8N/" target="_blank">Visualizar Documentação Completa</a>**

---

## 🛠️ Configuração Técnica (Resumo)
Se você deseja replicar este projeto, atente-se aos seguintes campos:

* **Trigger:** `Interval: 5 minutes`.
* **JQL de Busca:** `status = "Em Progresso" AND assignee = currentUser() AND (description !~ "comentado_por_dani" OR description is EMPTY)`.
* **Expressão de Trava:** `{{ $json.fields.description }} - comentado_por_dani`.

---
Developed with ☕ by [Dani](https://github.com/DannyRodrygues)
