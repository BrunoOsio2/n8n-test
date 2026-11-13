# Roteiro da Apresentação — Etapa 2 (entrega no Moodle)

> A apresentação começa pela **demonstração** (Etapa 1, ao vivo) e depois passa para a
> **experiência de desenvolvimento** (estes slides). Preencha os `[...]` com o que você
> realmente viveu — os desafios ficam mais fortes com casos reais.

---

## Slide 1 — Capa
- Título: Agente de IA para Pesquisa de Empresas
- Seu nome, disciplina (Tópicos Avançados), 2026

## Slide 2 — O problema / objetivo
- Agente que, dado o nome de uma empresa, pesquisa na web e devolve um relatório
  com 5 seções + fontes, em uma única interação.

## Slide 3 — Arquitetura da solução
- Diagrama: GitHub Pages → Webhook n8n → AI Agent (Gemini) + SerpAPI → resposta.
- Explique por que o agente roda fora do GitHub Pages (Pages só serve estático).

## Slide 4 — Ferramentas e escolhas (item 1 da Etapa 2)
- **Plataforma do agente:** n8n (recomendado, montagem visual, webhook pronto).
- **Modelo:** Google Gemini 2.0 Flash (tinha chave, rápido e com camada gratuita).
- **Busca web:** SerpAPI (resultados do Google, integra como ferramenta no AI Agent).
- **Interface:** página estática no GitHub Pages (hospedagem gratuita).

## Slide 5 — Instruções do agente (item 2)
- Como o prompt força: as 5 seções fixas, uso obrigatório da busca, citar fontes,
  nunca inventar dado ("Informação não encontrada..."), e resposta única.
- Tratamento de nome ambíguo: o agente escolhe a empresa mais relevante e declara qual
  assumiu, sem perguntar ao usuário.
- Empresa inexistente: devolve mensagem de "não identificada" e encerra.

## Slide 6 — Integração com o sistema (item 3)
- A página faz `POST {company}` no webhook; o n8n responde `{answer: "...markdown..."}`.
- A página renderiza o Markdown com marked.js.
- Desafio típico: **CORS** — resolvido liberando origens no webhook e no header da resposta.

## Slide 7 — Desafios e soluções (item 4)
Exemplos (ajuste aos seus):
- [ ] Agente respondia sem buscar → reforcei no prompt "use a ferramenta sempre".
- [ ] Faltavam fontes → exigi seção "## Fontes" no formato.
- [ ] Resposta demorava/timeout → troquei para gemini-2.0-flash.
- [ ] Nome ambíguo (ex.: "Apple") → regra de escolher a mais relevante e declarar.

## Slide 8 — Apoio da IA no desenvolvimento (item 5)
- O que a IA **sugeriu**: estrutura do prompt, JSON do workflow, HTML da página.
- O que **você decidiu/verificou**: escolha das ferramentas, testes com empresas reais,
  ajuste das instruções após ver respostas ruins, conferência das fontes.

## Slide 9 — Resultado / demonstração
- Print da pesquisa de uma empresa com as 5 seções e as fontes.

## Slide 10 — Encerramento
- Aprendizados e possíveis melhorias (cache, mais fontes, histórico de buscas).
