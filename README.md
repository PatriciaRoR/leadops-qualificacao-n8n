# LeadOps — Qualificação Inteligente de Leads com n8n, IA e PostgreSQL

Automação de qualificação e priorização de leads utilizando **n8n**, **IA generativa**, **PostgreSQL** e **Gmail**.

O fluxo recebe leads via webhook, valida os dados, verifica duplicidade no banco, interpreta a mensagem com IA, calcula um lead score por regras determinísticas, registra o histórico no PostgreSQL e envia alertas automáticos ao time comercial quando uma oportunidade é classificada como quente.

---

## Objetivo

Reduzir o trabalho manual envolvido na triagem de leads e permitir que oportunidades com maior potencial comercial sejam identificadas e priorizadas automaticamente.

O projeto foi pensado para simular um cenário real de integração entre Marketing, Operações e Tecnologia.

---

## Arquitetura

```text
Webhook REST
    ↓
Normalização e validação
    ↓
Consulta PostgreSQL
    ↓
Lead já existe?
   ↙          ↘
 SIM          NÃO
 ↓             ↓
UPDATE       INSERT
   ↘          ↙
    Análise com IA
          ↓
   Saída estruturada
          ↓
   Lead Score
          ↓
  QUENTE / MORNO / FRIO
          ↓
 Registrar interação
          ↓
      Lead quente?
       ↙       ↘
     SIM       NÃO
      ↓         ↓
 Alerta        Log
 comercial      ↓
      ↘        ↙
     Log da automação
          ↓
    Resposta HTTP
