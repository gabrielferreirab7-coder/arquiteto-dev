# Arquiteto Dev — Histórico do Projeto

## O que é esse projeto

Um agente estruturador técnico para o Claude Code. Transforma uma ideia solta em um mapa técnico executável — com escopo, arquitetura, stack, riscos, gaps e fases de implementação. Atua antes da execução, não durante.

Invocado como `/arquitetar`.

---

## Premissas de design

- **Não é orquestrador.** Não executa, não chama outras skills, não coordena agentes.
- **Não é executor.** Apenas organiza, explicita e propõe estrutura.
- **Não decide pelo usuário.** Mapeia, aponta gaps e para.
- **Não depende de contexto pré-existente.** Funciona em projetos novos sem nenhuma documentação.
- **Output é a conversa.** Nada é salvo automaticamente — o mapa técnico fica no chat.

---

## Referências consultadas

### [agentic-project-management](https://github.com/sdi2200262/agentic-project-management)

O mais relevante das referências. Trouxe:

- **Coleta de contexto em rounds progressivos** antes de gerar qualquer output
- **Formato de task breakdown** adaptado para "skills candidatas" (objetivo / input / output)
- **Confirmação de entendimento** antes de avançar para a próxima fase
- **Validação explícita** — cada entregável tem critérios claros de sucesso
- **Transparência de raciocínio** — o agente apresenta o que entendeu antes de agir

Estrutura de planejamento em três documentos (Spec → Plan → Rules) serviu de referência para as seções do mapa técnico.

### [gitagent](https://github.com/open-gitagent/gitagent)

Framework de execução — menos relevante para o escopo de estruturação. Contribuiu com:

- **Padrão de hook de bloqueio**: o agente declara ativamente que parou, em vez de simplesmente não fazer nada. Origem da "Fase 4 — Parada explícita".
- Referência de como definir skills de forma declarativa

### [hivespec](https://github.com/EntityProcess/hivespec)

Repositório não encontrado publicamente. Foram explorados projetos relacionados da organização EntityProcess:

- **github/spec-kit**: fluxo em 6 fases (Constitution → Specify → Plan → Tasks → Implement → Review). O `/arquitetar` cobre as fases 1 a 4 e para — alinhamento intencional com o escopo.
- **EntityProcess/openspec**: estrutura de change documents (proposal → design → tasks) que influenciou o formato do Plano em Fases (MVP → V1 → Futuro).

### Skill `/mapear` (repositório local)

`C:\Users\gabri\OneDrive\Desktop\Unity - Projetos\Teste\.claude\commands\mapear.md`

A referência mais próxima em estilo e formato. Definiu as convenções de interação do `/arquitetar`:

- **Uma pergunta por vez** durante a descoberta — nunca listar várias de uma vez
- **Pergunta aberta primeiro**, aprofundando conforme o que aparece
- **Tom direto, conversa natural, sem formalidade** — regra explícita no arquivo
- **Confirma o plano antes de agir** — "Bora?" antes de qualquer criação
- **Processos vagos**: aprofunda antes de avançar, não gera output com base em suposição
- **Verifica o que existe** antes de criar — evita duplicatas e perguntas desnecessárias

Principal diferença: o `/mapear` foi projetado para um workspace já configurado com contexto pré-existente. O `/arquitetar` foi projetado para funcionar do zero, em projetos novos, onde o contexto é construído pela própria conversa.

---

## Evolução do design

### Decisão: output no chat, sem exportar arquivo

Discutida e definida durante o planejamento. O entregável é a conversa estruturada — não um documento gerado. O usuário decide o que fazer com o output depois.

Motivo: o agente atua como organizador de raciocínio, não como gerador de documentação. Forçar exportação adicionaria fricção e mudaria o papel dele.

### Decisão: sem dependência de contexto pré-existente

O `/mapear` lê arquivos de contexto (`empresa.md`, `estrategia.md`) porque foi projetado após um `/setup`. O `/arquitetar` não pode ter esse pré-requisito — será usado principalmente no início de projetos novos, sem nenhuma documentação.

Solução: verifica o workspace antes de perguntar (gracioso se existir algo), mas começa do zero pela conversa se não existir nada.

### Decisão: escopo local primeiro, global depois

O arquivo foi criado em `.claude/commands/` dentro deste diretório para validação. Quando aprovado, será movido para `C:\Users\gabri\.claude\commands\` para ficar disponível globalmente em qualquer projeto.

---

## Arquivos do projeto

```
Arquiteto Dev/
  projeto.md                          ← este arquivo
  .claude/
    commands/
      arquitetar.md                   ← o agente
```

---

## Status

- [x] Design definido
- [x] Referências pesquisadas e avaliadas
- [x] Agente criado em `.claude/commands/arquitetar.md`
- [ ] Validação em uso real
- [ ] Promoção para global (`C:\Users\gabri\.claude\commands\`)
