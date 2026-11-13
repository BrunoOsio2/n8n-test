# Agente de Pesquisa de Empresas

Trabalho de Tópicos Avançados — agente de IA que pesquisa informações sobre uma empresa
a partir do nome, integrado a uma página web.

**Arquitetura:** `GitHub Pages (index.html)` → `n8n.cloud (Webhook + AI Agent)` → `Gemini + SerpAPI`

## Arquivos
- `workflow-n8n.json` — workflow pronto para importar no n8n.
- `instrucoes-agente.md` — system prompt do agente.
- `index.html` — página de busca (GitHub Pages).
- `apresentacao-etapa2.md` — roteiro dos slides para o Moodle.

---

## Passo a passo

### 1. Configurar o n8n
1. Entre no [n8n.cloud](https://n8n.cloud) e crie um workspace.
2. **Workflows → Import from File** → selecione `workflow-n8n.json`.
3. Crie as credenciais (ícone de cada nó → *Create New Credential*):
   - **Google Gemini Chat Model** → cole sua **chave do Gemini** (Google AI Studio / `googlePalmApi`).
   - **SerpAPI** → cole sua **chave do SerpAPI**.
4. Clique em **Save** e depois ative o workflow (toggle **Active** no topo).

### 2. Pegar a URL do webhook
- Clique no nó **Webhook** → copie a **Production URL**
  (algo como `https://SEU-SUBDOMINIO.app.n8n.cloud/webhook/pesquisa-empresa`).
- Teste rápido pelo terminal:
  ```bash
  curl -X POST "SUA_URL_AQUI" \
    -H "Content-Type: application/json" \
    -d '{"company":"Nubank"}'
  ```
  Deve voltar um JSON com `{"answer": "## 1. Identificação..."}`.

### 3. Publicar a página no GitHub Pages
1. Edite `index.html`: troque `WEBHOOK_URL` pela sua Production URL.
2. Crie um repositório no GitHub e suba o `index.html`.
3. **Settings → Pages → Source: branch `main` / root** → salve.
4. Acesse `https://SEU-USUARIO.github.io/SEU-REPO/`.

### 4. Demonstração (Etapa 1)
- Abra a página, digite o nome de uma empresa e clique em Pesquisar.
- Mostre as 5 seções e as fontes retornadas.

---

## Observações técnicas
- **Chaves ficam só no n8n** — nunca no `index.html` (o JS é público no GitHub Pages).
- **CORS**: o webhook está com `allowedOrigins: "*"` e o nó de resposta envia
  `Access-Control-Allow-Origin: *`. Se o navegador reclamar de CORS, confira esses dois pontos.
- Se a resposta demorar/estourar tempo, aumente o timeout do n8n ou troque o modelo
  para `models/gemini-2.0-flash` (rápido) — já é o padrão no workflow.
