# AD — Análise & Divulgação (scaffold)

Projeto: conjunto de microserviços para detectar eventos globais (catástrofes naturais, impactos em supply-chain, mercados de GPUs, cripto e indicadores macro), gerar análises e montar multimídia (imagens/vídeo) a partir de templates.

Principais módulos
- ingestão/: coleta de dados (USGS, CoinGecko, news, APIs).
- analysis/: detector de eventos, scoring de impacto, forecast (MVP básico).
- media/: gerador de imagens & vídeos a partir de roteiro + templates.
- api/: endpoints REST (FastAPI) para ingestão, análise e geração.
- pipelines/: scripts orquestradores (cron / loop).
- docs/: arquitetura, guias.

Rápido start (local)
1. Clone o repo:
   git clone https://github.com/jghjvgcv-cyber/ad.git
2. Crie e ative um venv (Python 3.10+ recomendado)
   python -m venv .venv
   source .venv/bin/activate   # Linux/macOS
   .venv\Scripts\activate      # Windows
3. Instale dependências:
   pip install -r requirements.txt
4. Configure variáveis (exemplo em .env.example)
   cp .env.example .env
   editar .env com TELEGRAM_TOKEN, TELEGRAM_CHAT_ID, etc.
5. Executar API:
   uvicorn src.main:app --reload --port 8000
6. Rodar pipeline de ingestão simples:
   python pipelines/ingest_pipeline.py

MVP sugerido inicialmente
- Ingestão: USGS (terremotos), CoinGecko (cripto).
- Detector básico: regras por magnitude/variação de preço.
- Notificações: Telegram.
- Gerador de thumbnail via Stable Diffusion (integração mínima).
- Endpoint para gerar vídeo curto a partir de template JSON.

APIs e chaves
- USGS: não requer chave para feeds públicos.
- CoinGecko: API pública (limites).
- TELEGRAM_TOKEN e TELEGRAM_CHAT_ID se usar alertas via Telegram.
- OPENAI_API_KEY (opcional) para gerar roteiros via LLM.
- STABLE_DIFFUSION config (endpoint/ckpt) se for usar geração de imagens.

Próximos passos
- Integrar mais fontes (GDELT, Glassnode, exchanges).
- Implementar modelos de forecast e detecção por ML.
- Permitir push automático para repositório se autorizado.

Contato
- repo: https://github.com/jghjvgcv-cyber/ad
