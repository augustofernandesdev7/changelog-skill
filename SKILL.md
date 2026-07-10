---
name: project-changelog
description: Gera um HTML de changelog/apresentação de projeto para mostrar a stakeholders não-técnicos (chefe, cliente, sócio) tudo que foi implementado numa rodada de trabalho, com simulações interativas reais de cada tela nova. Usar sempre que o usuário pedir um "changelog", "html de apresentação do projeto", "resumo do que foi feito", "documento pra mostrar pro patrão/cliente", ou qualquer variação disso — mesmo sem citar o nome "changelog" explicitamente, se a intenção for demonstrar progresso de forma visual e não-técnica. Este é o formato padrão pessoal do usuário para todos os projetos, sempre usar esta estrutura em vez de inventar uma nova.
---

# Changelog de Apresentação de Projeto

Formato pessoal e padrão do usuário para comunicar progresso técnico a públicos não-técnicos (chefe, sócio, cliente). Sempre que ele pedir algo assim, siga esta estrutura — não crie um formato novo do zero.

## Por que esse formato existe

O usuário já testou e aprovou esse modelo (ver `assets/template.html`, um template genérico de referência com conteúdo de exemplo — sem dados de nenhum projeto real). Ele quer o mesmo padrão visual e a mesma abordagem de conteúdo em todos os projetos futuros, para não precisar reexplicar o formato toda vez.

## Estrutura obrigatória

Um único arquivo HTML autossuficiente (sem dependências externas — sem CDN de fontes, sem bibliotecas JS externas), contendo:

1. **Sidebar de TOC fixa** à esquerda, com âncoras numeradas para cada feature (`#f1`, `#f2`, ...). Em telas estreitas (`max-width: 900px`) ela desaparece.
2. **Hero** no topo: nome do projeto + data no título (formato `Change Logs {NOME DO PROJETO} — {DD/MM/AAAA}`), um parágrafo curto explicando o que é o documento, e uma linha de estatísticas rápidas (nº de funcionalidades, telas novas, bugs corrigidos, etc.).
3. **Uma seção por funcionalidade** (`<section class="feature" id="fN">`), cada uma com:
   - Um ícone emoji + título + tag colorida (`Novo` verde / `Corrigido` vermelho / `Alterado` laranja).
   - Um parágrafo em **linguagem simples, sem jargão técnico** — o leitor não sabe o que é uma migration, uma RLS policy ou um middleware. Descreva o comportamento observável ("antes X acontecia, agora Y acontece"), nunca a implementação.
   - Um "device frame" (`.frame`, com barra de título estilo browser) contendo uma **simulação interativa de verdade em JavaScript puro** da tela — não uma screenshot estática, não uma descrição. O leitor precisa poder clicar em botões, preencher campos, ver o estado mudar. Isso é o coração do documento.
4. **Nota de rodapé** simples (projeto + data).

Veja `assets/template.html` para o scaffold completo de CSS (design tokens, tema claro/escuro, componentes reutilizáveis: `.btn`, `.badge`, `.mini-card`, `.stepper`, `.tabs`, `.msg-bubble`/`.msg-wrap` para notificações estilo WhatsApp/SMS, `.email-preview`, `.chat-wrap`, `.code-boxes` para códigos de verificação, `.diff-grid` para antes/depois) e os padrões de JS (toast de feedback, filtros de tabela, troca de abas, chat simulado, stepper de onboarding). O arquivo já vem com 10 seções de exemplo genéricas (projeto fictício "Acme SaaS") cobrindo os principais tipos de simulação — copie como ponto de partida, troque o conteúdo pelas funcionalidades reais do projeto atual, e não recrie o CSS do zero.

## Adaptando para um novo projeto

- **Cor de destaque**: o template usa tokens `--accent`/`--accent-light`/`--accent-deep` com um roxo neutro de exemplo. Para cada projeto novo, troque esses tokens (e os equivalentes no bloco dark) pela cor de marca real do projeto — procure num `tailwind.config`, CSS de tema, ou constante `BRAND` do próprio código antes de inventar uma cor.
- **Título e branding**: troque `{NOME DO PROJETO}` e `{DD/MM/AAAA}` (no `<title>`, no `<h1>` e na nota de rodapé) pelo nome do projeto atual e a data de hoje. Troque o texto do `.toc-brand` também.
- **Conteúdo das seções**: as 10 seções do template são só exemplos de estrutura — substitua todas pelo conteúdo real das funcionalidades implementadas na sessão de trabalho atual. Não invente funcionalidades nem deixe texto de exemplo no documento final. Use o histórico da conversa para saber exatamente o que foi feito.
- **Simulações**: cada tipo de tela pede um tipo de simulação diferente — reaproveite os componentes do template quando o formato bater (ex: um novo fluxo de confirmação por e-mail → reusar `.code-boxes`; uma nova tabela com filtro → reusar `table.sim` + filtro JS; uma nova automação de mensagens → reusar `.msg-bubble`/`.msg-wrap`). Quando não houver componente equivalente, crie um novo seguindo a mesma linguagem visual (tokens de cor, `border-radius`, `--shadow-md`).
- **Tema claro/escuro**: mantenha sempre os três blocos de tokens (`:root`, `@media (prefers-color-scheme: dark)`, `:root[data-theme="dark"]`/`"light"`) — o usuário sempre quer os dois temas funcionando.

## Onde publicar

Depois de montar o HTML, pergunte ao usuário como ele quer publicar (a menos que já tenha dito): como Claude Artifact (privado por padrão, precisa habilitar compartilhamento no menu do próprio artifact) ou hospedado na Vercel dele (URL própria, não depende de login no claude.ai). Use a ferramenta `Artifact` ou `mcp__claude_ai_Vercel__deploy_to_vercel` conforme a escolha.

## Regra importante: nunca commitar no repositório do projeto

Por padrão, **este HTML não deve ir para o repositório git do projeto** — é um documento interno/de apresentação, não parte do código do produto. Gere o arquivo fora do repositório (num diretório de scratchpad/temp) e só publique via Artifact ou deploy separado. Só inclua no repositório se o usuário pedir isso explicitamente.
