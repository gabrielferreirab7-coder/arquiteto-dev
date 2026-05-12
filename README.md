# arquitetar

Skill para o Claude Code que transforma uma ideia solta em um mapa técnico executável.

Atua como estruturador técnico — não como executor. Faz perguntas, confirma o entendimento, detecta quando o escopo é grande demais para uma sessão e sugere divisão proativa. Gera um mapa completo no chat e cria automaticamente a documentação de fases em `docs/` — pronta para execução incremental em múltiplas sessões.

---

## O que ela faz

- Descobre o problema através de perguntas progressivas (uma por vez)
- Confirma o entendimento antes de estruturar qualquer coisa
- Detecta projetos com escopo grande e sugere divisão em fases antes de estruturar
- Gera um mapa técnico completo no chat
- Cria automaticamente `docs/plano-geral.md` e `docs/fase-N.md` ao final
- Marca explicitamente o que está assumido vs. confirmado
- Lista gaps e pontos de decisão que precisam de resposta antes da execução

## O que ela não faz

- Não executa nada
- Não chama outras skills automaticamente
- Não decide pelo usuário
- Não gera código

---

## Como usar

```
/arquitetar
```

Jogue uma ideia — pode ser vaga. O agente pergunta o que precisar, confirma o entendimento e gera o mapa.

---

## Output

### No chat

O mapa técnico é entregue diretamente na conversa com estas seções:

- **Definição do Problema** — o que está sendo construído, para quem, com qual objetivo
- **Tradução para Solução** — tipo de solução, como funciona, o que faz e o que não faz
- **Arquitetura Sugerida** — blocos, inputs, outputs, dependências, alternativas simples
- **Stack Recomendada** — tecnologias com justificativa prática para o projeto específico
- **Riscos e Travas** — segurança, APIs externas, custo, manutenção, o que pode quebrar
- **Gaps de Informação** — o que está assumido, o que precisa de decisão, o que foi deixado fora
- **Plano em Fases** — Fase 1 / Fase 2 / Fase 3 / Backlog (projetos divididos) ou MVP / V1 / Futuro (projetos simples)
- **Skills Candidatas** — skills que podem ser úteis no futuro, sem criar automaticamente

### Em arquivos (`docs/`)

Gerado automaticamente após o mapa, sem precisar pedir:

```
docs/
  plano-geral.md    ← mapa técnico completo + seção "Estado Atual" (fonte da verdade entre sessões)
  fase-1.md         ← escopo, tarefas, critério de conclusão + seções obrigatórias
  fase-2.md         ← idem
  fase-3.md         ← idem
```

Cada arquivo de fase inclui duas seções inegociáveis:

- **⚠️ Antes de Começar** — instrução obrigatória de ler o `plano-geral.md` antes de qualquer execução
- **⚠️ Após Executar** — instrução obrigatória de atualizar o arquivo da fase e o `plano-geral.md` (Estado Atual, Decisões Tomadas, Onde Estão as Coisas) antes de encerrar a sessão

O `plano-geral.md` funciona como fonte da verdade entre sessões e máquinas — registra decisões tomadas durante execução, desvios do plano original e localização de todos os serviços e recursos do projeto.

---

## Instalação

### Local (um projeto específico)

Copie `arquitetar.md` para `.claude/commands/` dentro do projeto:

```
seu-projeto/
  .claude/
    commands/
      arquitetar.md
```

### Global (todos os projetos)

Copie `arquitetar.md` para a pasta global do Claude Code:

```
C:\Users\<usuario>\.claude\commands\arquitetar.md   # Windows
~/.claude/commands/arquitetar.md                    # macOS / Linux
```

---

## Referências

O design da skill foi baseado em padrões extraídos de:

- **[agentic-project-management](https://github.com/sdi2200262/agentic-project-management)** — coleta de contexto em rounds progressivos, formato de task breakdown, confirmação de entendimento antes de avançar, transparência de raciocínio
- **[gitagent](https://github.com/open-gitagent/gitagent)** — padrão de parada explícita (o agente declara que parou e lista o que ficou em aberto)
- **[github/spec-kit](https://github.com/github/spec-kit)** — fluxo de especificação em fases (Constitution → Specify → Plan → Tasks); o `/arquitetar` cobre as quatro primeiras e para
- **[EntityProcess/openspec](https://github.com/EntityProcess/subagent)** — estrutura de change documents (proposal → design → tasks) que inspirou o Plano em Fases (MVP → V1 → Futuro)
