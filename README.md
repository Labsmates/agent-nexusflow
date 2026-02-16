# Agent NexusFlow

Workflow n8n d'orchestration IA multi-agents avec 22 sous-agents specialises.

## Architecture

```
Telegram Trigger --> Agent NexusFlow (AI Agent)
                         |
        +----------------+----------------+
        |                |                |
  22 Sub-Agents    Memory (Redis)    LLM Models
  (toolWorkflow)                   (GPT 5.1 + Claude)
```

## Sous-Agents (22 workflows)

Chaque sous-agent est un workflow n8n independant, orchestre par l'agent principal via des connexions `ai_tool`.

| # | Agent | Fichier | Nodes | Description |
|---|-------|---------|-------|-------------|
| 1 | **FAL** | [fal.json](workflows/fal.json) | 18 | Generate 8-second videos using Google VEO3 AI model via fal.ai and upload to Drive |
| 2 | **Redacteur** | [redacteur.json](workflows/redacteur.json) | 12 | Write professional content with web research (Tavily/Perplexity), convert to PDF via Gotenberg |
| 3 | **Builder** | [builder.json](workflows/builder.json) | 9 | Build and design n8n workflows using AI agent with n8n development expertise |
| 4 | **Avatar** | [avatar.json](workflows/avatar.json) | 26 | Create AI avatar videos with HeyGen using dual AI script writers |
| 5 | **Resume** | [resume.json](workflows/resume.json) | 10 | Summarize documents using OpenAI, generate styled PDF via Gotenberg |
| 6 | **Juridique IA** | [juridique-ia.json](workflows/juridique-ia.json) | 8 | Legal AI assistant with Redis memory and research for French law questions |
| 7 | **Image** | [image.json](workflows/image.json) | 9 | Generate AI images using DALL-E with intelligent style selection |
| 8 | **Agent Mail** | [agent-mail.json](workflows/agent-mail.json) | 14 | Manage Gmail with 9 email operations (read, send, reply, draft, label, delete) |
| 9 | **Calendrier Agent** | [calendrier-agent.json](workflows/calendrier-agent.json) | 9 | Manage Google Calendar events with full CRUD operations |
| 10 | **Web Agent** | [web-agent.json](workflows/web-agent.json) | 11 | Search web using Tavily/Perplexity/Wikipedia/Hacker News |
| 11 | **Agent Contacts** | [agent-contacts.json](workflows/agent-contacts.json) | 7 | Manage Airtable contacts database with search and add/update operations |
| 12 | **Agent PDF** | [agent-pdf.json](workflows/agent-pdf.json) | 9 | Create professional PDFs with AI-enhanced text and Gotenberg conversion |
| 13 | **Agent RAG** | [agent-rag.json](workflows/agent-rag.json) | 37 | RAG system for context-aware AI responses using vector database and embeddings |
| 14 | **DJ** | [dj.json](workflows/dj.json) | 33 | Generate professional DJ playlists using Qdrant RAG with BPM/tonality matching |
| 15 | **Agent Codeur** | [agent-codeur.json](workflows/agent-codeur.json) | 23 | Code in multiple languages with Redis memory, web research, and history tracking |
| 16 | **Agent Youtube** | [agent-youtube.json](workflows/agent-youtube.json) | 8 | Manage YouTube content and track video ideas using Google Sheets |
| 17 | **Photoshop** | [photoshop.json](workflows/photoshop.json) | 17 | Edit and combine images using dual AI models with Drive integration |
| 18 | **Agent Shopping** | [agent-shopping.json](workflows/agent-shopping.json) | 13 | Search shopping and travel (hotels, flights, restaurants, products) |
| 19 | **Agent Podcast** | [agent-podcast.json](workflows/agent-podcast.json) | 20 | Generate complete podcast episodes with script, voice, and publishing |
| 20 | **Agent Regisseur** | [agent-regisseur.json](workflows/agent-regisseur.json) | 14 | Multi-speaker podcast dialogue generator with dual AI hosts and ElevenLabs |
| 21 | **Docteur** | [docteur.json](workflows/docteur.json) | 6 | Medical and health AI assistant with research capabilities |
| 22 | **VPS Agent** | [vps-agent.json](workflows/vps-agent.json) | 12 | VPS server management and monitoring agent |

## Outils integres (non-workflow)

| Outil | Type | Description |
|-------|------|-------------|
| Think | toolThink | Raisonnement et reflexion |
| Calculator | toolCalculator | Calculs mathematiques |
| Date & Time | dateTimeTool | Operations date/heure |
| OpenWeatherMap | openWeatherMapTool | Meteo en temps reel |

## Import

### Workflow principal (Agent NexusFlow)

1. Ouvrir n8n
2. Aller dans **Workflows > Import from File**
3. Selectionner `agent-nexusflow.json`
4. Configurer les credentials necessaires

### Sous-agents

1. Importer d'abord tous les fichiers du dossier `workflows/`
2. Importer ensuite `agent-nexusflow.json` (le workflow principal)
3. Reconfigurer les `workflowId` dans chaque outil si necessaire
4. Configurer les credentials pour chaque sous-agent

## Credentials necessaires

| Service | Utilise par |
|---------|-------------|
| Telegram | Agent NexusFlow (trigger + responses) |
| OpenRouter | LLM principal (GPT 5.1) |
| Anthropic | LLM secondaire (Claude) |
| Redis | Memoire conversationnelle |
| Google Sheets | Agent Youtube, logging |
| Google Drive | FAL, Image, Resume, Redacteur, PDF, Podcast |
| Google Calendar | Calendrier Agent |
| Gmail | Agent Mail |
| ElevenLabs | Agent Podcast, Agent Regisseur |
| OpenAI | Resume, Image, Agent PDF, Builder |
| Tavily | Web Agent, Juridique, Codeur, Shopping, Docteur |
| Perplexity | Web Agent, Redacteur, Shopping |
| HeyGen | Avatar |
| Airtable | Agent Contacts |
| Gotenberg | Redacteur, Resume, Agent PDF |
| Qdrant | DJ (vector store) |

## Notes

- Les credentials ont ete retirees des fichiers JSON pour des raisons de securite
- Vous devez configurer vos propres credentials apres import
- Chaque sous-agent peut fonctionner independamment
- L'agent principal orchestre les 22 sous-agents via Telegram

## Stack Technique

- **n8n** v2.34.4
- **LLM**: GPT 5.1 (OpenRouter) + Claude (Anthropic)
- **Memory**: Redis Chat Memory
- **Voice**: ElevenLabs TTS + STT
- **Interface**: Telegram Bot
