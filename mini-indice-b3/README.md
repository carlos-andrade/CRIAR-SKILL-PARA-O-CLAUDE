# Skill Mini Índice B3 (WIN)

Skill modular para análise do contrato futuro de mini Ibovespa (WIN), microestrutura, fluxo, VWAP/TWAP, delta, volume, FVG/ICT, contexto macro, risco e pesquisa quantitativa.

## Estrutura

- `SKILL.md`: regras centrais e encaminhamento.
- `references/`: conhecimento técnico por domínio, incluindo especificação matemática VWAP/TWAP.
- `workflows/calculo-vwap-twap.md`: procedimento reproduzível para cálculo e auditoria das referências.
- `workflows/`: procedimentos reproduzíveis.
- `tests/`: avaliações de comportamento e critérios de aceitação.

## Instalação

### Claude Code — projeto

Copie a pasta `mini-indice-b3/` para `.claude/skills/` no repositório em que pretende utilizar a Skill:

```bash
mkdir -p .claude/skills
cp -a mini-indice-b3 .claude/skills/
```

### Claude Code — utilizador

Copie a pasta para `~/.claude/skills/`.

### claude.ai

Comprima a pasta `mini-indice-b3/` em ZIP preservando-a como diretório raiz do arquivo. Carregue em Settings > Features > Skills, conforme a interface/plano vigente. A disponibilidade pode variar por produto e plano.

## Utilização

Faça pedidos naturais relacionados com WIN, por exemplo: análise intradiária, leitura de fluxo, auditoria de backtest, definição de setup ou avaliação de risco.

A Skill não fornece cotações por si só. A análise depende dos dados e ferramentas disponíveis no ambiente.

## Princípios de uso

- Não tratar indicadores como entradas automáticas.
- Distinguir factos, inferências, hipóteses e lacunas.
- Verificar parâmetros atuais da B3 em fonte oficial.
- Incorporar custos, slippage e execução.
- Aceitar não operar como resultado.
- Não prometer rentabilidade.

## Validação

Consulte `tests/casos-de-teste.md`, `tests/testes-vwap-twap.md` e `tests/checklist-validacao.md`. A validação documental da estrutura não equivale a avaliação empírica do modelo Claude; testes reais devem ser executados no ambiente em que a Skill será instalada.

## Fontes institucionais iniciais

- [Anthropic — Agent Skills](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview)
- [Anthropic — Skill authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices)
- [B3 — Futuro Mini de Ibovespa](https://www.b3.com.br/pt_br/produtos-e-servicos/negociacao/renda-variavel/futuro-mini-de-ibovespa.htm)

As fontes e parâmetros do contrato devem ser reconfirmados antes de uso operacional.
