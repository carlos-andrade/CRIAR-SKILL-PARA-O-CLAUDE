# Skill Mini Índice B3 (WIN)

Skill modular para análise do contrato futuro de mini Ibovespa (WIN), microestrutura, fluxo, VWAP/TWAP, Cumulative Delta, volume, contexto intermercado, regimes de mercado, calendário macro, FVG/ICT, risco e pesquisa quantitativa.

## Estrutura

- `SKILL.md`: regras centrais e encaminhamento.
- `references/`: conhecimento técnico por domínio.
- `workflows/`: procedimentos reproduzíveis de cálculo e análise.
- `tests/`: avaliações comportamentais, fixtures e critérios de aceitação.

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

Faça pedidos naturais relacionados com WIN: análise intradiária, leitura de fluxo, contexto macro, avaliação de regime, auditoria de backtest, definição de setup ou avaliação de risco.

A Skill não fornece cotações por si só. A análise depende dos dados e ferramentas disponíveis no ambiente.

## Princípios

- Não tratar indicadores ou variáveis macro como entradas automáticas.
- Distinguir VIX Cboe (S&P 500) de S&P/B3 Ibovespa VIX (VXBR).
- IBOV é referência à vista, não substituto do contrato WIN.
- Usar consensos e calendários point-in-time em pesquisa histórica.
- Distinguir volatilidade implícita de realizada.
- Incorporar custos, slippage e execução.
- Aceitar não operar como resultado.
- Não prometer rentabilidade.

## Validação

Consulte:
- `tests/casos-de-teste.md`
- `tests/testes-vwap-twap.md`
- `tests/testes-fluxo-microestrutura.md`
- `tests/testes-contexto-regime.md`
- `tests/checklist-validacao.md`

A validação documental não equivale a avaliação empírica do modelo Claude. Testes reais exigem instalação e fixtures point-in-time.

## Fontes institucionais iniciais

- [Anthropic — Agent Skills](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview)
- [Anthropic — Skill authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices)
- [B3 — Ibovespa](https://www.b3.com.br/pt_br/market-data-e-indices/indices/indices-amplos/ibovespa.htm)
- [S&P DJI — S&P/B3 Ibovespa VIX](https://www.spglobal.com/spdji/pt/indices/indicators/sp-b3-ibovespa-vix/)
- [Cboe — VIX FAQ](https://www.cboe.com/tradable_products/vix/faqs)
- [BCB — Copom](https://www.bcb.gov.br/controleinflacao/copom)
- [BCB — Focus](https://www.bcb.gov.br/controleinflacao/relatoriofocus)
- [IBGE — Calendário de divulgações](https://www.ibge.gov.br/calendario-de-divulgacoes-novoript)

Reconfirmar metodologias, calendários e parâmetros vigentes antes de uso operacional.
