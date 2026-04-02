# sensr-itsm-intelligence
Sistema de inteligência de dados ITSM integrado à API sensr.IT — agente LangChain ReAct analisa tickets, projetos e SLA, gerando insights e dashboard HTML/JS interativo com Chart.js.
# 🎫 sensr.IT — ITSM Intelligence Dashboard

![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-0.3-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-Dashboard-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![Chart.js](https://img.shields.io/badge/Chart.js-4.4-FF6384?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Concluído-brightgreen?style=for-the-badge)

> Sistema de inteligência de dados para a plataforma ITSM **sensr.IT** — consome a API REST, processa dados de Service e Projetos, analisa SLA e KPIs gerenciais com um agente **LangChain**, e entrega um **dashboard HTML/JS interativo** com 5 visões analíticas.

---

## 🧠 Arquitetura do Sistema

```
┌─────────────────────────────────────────────────────────┐
│                   sensr.IT REST API                      │
│  /tickets  /projects  /sla  /kpis  /categories  /agents │
└────────────────────┬────────────────────────────────────┘
                     │ SensrAPIClient
                     ▼
┌─────────────────────────────────────────────────────────┐
│                  ITSMDataProcessor                       │
│  Tickets · Projetos · SLA · Timeline · KPIs             │
└────────────────────┬────────────────────────────────────┘
                     │
          ┌──────────┴──────────┐
          │                     │
          ▼                     ▼
┌─────────────────┐   ┌─────────────────────────────────┐
│ DashboardGen    │   │   ITSMAnalystAgent (LangChain)   │
│                 │   │                                  │
│ HTML/JS com     │   │  🔧 AnalyzeTicketsTool           │
│ Chart.js        │   │  🔧 AnalyzeProjectsTool          │
│                 │   │  🔧 AnalyzeSLATool               │
│ 5 abas:         │   │  🔧 GenerateRecommendationsTool  │
│ · Visão Geral   │   │                                  │
│ · Tickets       │   │  Padrão ReAct + BaseTool         │
│ · Projetos      │   └─────────────────────────────────┘
│ · SLA           │
│ · IA & Insights │
└─────────────────┘
```

---

## ⚡ Execução Real do Pipeline

```
╔══════════════════════════════════════════════════════╗
║       sensr.IT — ITSM Intelligence Dashboard         ║
║  🦜 LangChain AI  |  📊 HTML/JS  |  🔌 sensr.IT API ║
╚══════════════════════════════════════════════════════╝

[SensrAPIClient] GET /tickets  → 200 chamados
[SensrAPIClient] GET /projects → 12 projetos
[SensrAPIClient] GET /sla      → período: 30 dias
[SensrAPIClient] GET /kpis     → 5 métricas

[DataProcessor] ✅ Processamento concluído

[AnalyzeTicketsTool]          ✅ 200 tickets | 5 insights
[AnalyzeProjectsTool]         ✅ 12 projetos | 3 em risco
[AnalyzeSLATool]              ✅ SLA: 82.0% | 3 violações
[GenerateRecommendationsTool] ✅ 6 recomendações

[DashboardGenerator] ✅ dashboard/index.html gerado

📊 RESUMO:
   Tickets analisados : 200
   Tickets em aberto  : 73
   Tickets críticos   : 4
   Projetos ativos    : 3
   Projetos em risco  : 3
   SLA geral          : 82.0%
   Recomendações IA   : 6
```

---

## 📊 Dashboard — 5 Visões Analíticas

### 1. Visão Geral
KPIs consolidados, gráfico de timeline (tickets abertos vs resolvidos nos últimos 14 dias), distribuição por prioridade e conformidade de SLA.

### 2. Tickets & Service
Distribuição por categoria e agente, tabela de chamados recentes com filtro por prioridade e status, tempo médio de resolução.

### 3. Projetos
Status de todos os projetos com barra de progresso, análise de orçamento (planejado vs realizado), nível de risco e gerente responsável.

### 4. SLA
Conformidade por prioridade (Crítica/Alta/Média/Baixa) e por categoria de chamado, com alertas visuais para violações.

### 5. IA & Insights
Insights gerados automaticamente pelo agente LangChain para tickets, projetos e SLA, além de recomendações estratégicas priorizadas (Urgente/Alta/Média/Baixa).

---

## 🔌 API sensr.IT — Endpoints Implementados

| Endpoint | Método | Descrição |
|---|---|---|
| `/tickets` | GET | Lista chamados com filtros |
| `/tickets/{id}` | GET | Detalhe de um chamado |
| `/projects` | GET | Lista projetos |
| `/projects/{id}` | GET | Detalhe de um projeto |
| `/sla` | GET | Relatório consolidado de SLA |
| `/kpis` | GET | KPIs gerenciais |
| `/categories` | GET | Categorias de chamados |
| `/agents` | GET | Agentes/atendentes |

---

## 🤖 Agente LangChain — Ferramentas

| Ferramenta | Responsabilidade |
|---|---|
| `AnalyzeTicketsTool` | Distribuição, gargalos, insights de chamados |
| `AnalyzeProjectsTool` | Progresso, orçamento, riscos de projetos |
| `AnalyzeSLATool` | Conformidade por prioridade e categoria |
| `GenerateRecommendationsTool` | Recomendações estratégicas priorizadas |

---

## 📁 Estrutura do Projeto

```
sensr-itsm/
├── main.py                        # Pipeline completo
├── requirements.txt
├── api/
│   ├── __init__.py
│   └── sensr_client.py            # SensrAPIClient + MockDataGenerator
├── agents/
│   ├── __init__.py
│   └── itsm_agent.py              # LangChain ReAct Agent + 4 BaseTool
├── core/
│   ├── __init__.py
│   ├── processor.py               # ITSMDataProcessor
│   └── dashboard_generator.py     # HTML/JS Dashboard Generator
└── dashboard/
    └── index.html                 # Dashboard gerado (abrir no navegador)
```

---

## 🚀 Como Executar

```bash
# Clone o repositório
git clone https://github.com/Engcarlosrodrigo-dev/sensr-itsm-intelligence.git
cd sensr-itsm-intelligence

# Instale as dependências
pip install -r requirements.txt

# Execute o pipeline
python main.py

# Abra o dashboard no navegador
# Arquivo: dashboard/index.html
```

Para conectar à API real do sensr.IT:
```bash
export SENSR_API_URL="https://api.sensr.it/v1"
export SENSR_API_KEY="sua-chave-aqui"
python main.py
```

---

## 🛠️ Stack Técnica

| Tecnologia | Uso |
|---|---|
| Python 3.11 | Linguagem principal |
| LangChain 0.3 | Agente ReAct + BaseTool |
| Chart.js 4.4 | Gráficos interativos no dashboard |
| HTML5 / JS | Dashboard sem framework |
| Pydantic | Schema das ferramentas LangChain |
| sensr.IT API | Fonte de dados ITSM |

---

*Projeto desenvolvido para gestão inteligente de dados ITSM — integrando API, processamento de dados, IA e visualização em um pipeline completo.*
