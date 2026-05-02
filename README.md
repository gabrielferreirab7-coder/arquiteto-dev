# arquitetar

Skill para o Claude Code que transforma uma ideia solta em um mapa técnico executável.

Atua como estruturador técnico — não como executor. Faz perguntas, confirma o entendimento e gera um mapa completo com escopo, arquitetura, stack, riscos, gaps e fases de implementação. Para aí.

---

## O que ela faz

- Descobre o problema através de perguntas progressivas (uma por vez)
- Confirma o entendimento antes de estruturar qualquer coisa
- Gera um mapa técnico completo no chat
- Marca explicitamente o que está assumido vs. confirmado
- Lista gaps e pontos de decisão que precisam de resposta antes da execução

## O que ela não faz

- Não executa nada
- Não chama outras skills automaticamente
- Não salva arquivos
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

O mapa técnico é entregue no chat com estas seções:

- **Definição do Problema** — o que está sendo construído, para quem, com qual objetivo
- **Tradução para Solução** — tipo de solução, como funciona, o que faz e o que não faz
- **Arquitetura Sugerida** — blocos, inputs, outputs, dependências, alternativas simples
- **Stack Recomendada** — tecnologias com justificativa prática para o projeto específico
- **Riscos e Travas** — segurança, APIs externas, custo, manutenção, o que pode quebrar
- **Gaps de Informação** — o que está assumido, o que precisa de decisão, o que foi deixado fora
- **Plano em Fases** — MVP, V1 e o que fica para depois
- **Skills Candidatas** — skills que podem ser úteis no futuro, sem criar automaticamente

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
