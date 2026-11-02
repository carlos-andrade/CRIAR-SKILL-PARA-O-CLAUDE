---
name: mini-indice-b3
description: Analisa o mini índice futuro WIN da B3, fluxo, microestrutura, VWAP/TWAP, delta, volume, FVG/ICT, contexto macro e risco. Use em perguntas sobre WIN, setups, execução ou backtests.
---

# Mini Índice Futuro B3 (WIN)

Skill para análise verificável do contrato futuro de mini Ibovespa (WIN). O objetivo é apoiar pesquisa e decisões disciplinadas, não emitir sinais automáticos nem prometer rentabilidade.

## Princípios obrigatórios

1. **Identifique o instrumento:** diferencie IBOV à vista, futuro cheio IND e mini futuro WIN. Registe vencimento/série, sessão, timeframe, fonte e timestamp.
2. **Valide os dados antes de interpretar:** granularidade, fuso, latência, campos ausentes, duplicados, negócios sem agressor classificado e eventuais ajustes. Sem dados suficientes, declare o que não pode ser concluído.
3. **Separe epistemicamente:** rotule factos observados, cálculos, inferências, hipóteses e desconhecidos.
4. **Não automatize a interpretação:** VWAP, TWAP, delta, volume, FVG, VIX e IBOV não são sinais isolados nem prova de intenção institucional.
5. **Integre risco e execução:** custos, slippage, spread, liquidez, risco por operação e limite diário são parte da análise.
6. **Não force trades:** cenário de não operação é uma conclusão válida.
7. **Fontes atuais:** confirme regras contratuais e horários nas fontes oficiais. Indique data de consulta e período de validade. Nunca simule feed em tempo real.

## Roteamento por referência

Consulte apenas o material necessário à tarefa:

- Especificação, vencimento, rolagem e sessões: `references/contrato-win.md`.
- Microestrutura, ticks, trades, agressão e limitações do feed: `references/microestrutura-fluxo.md`.
- VWAP, TWAP e gap: `references/vwap-twap.md`.
- Delta, volume e atividade: `references/delta-volume.md`.
- Fair Value Gap e conceitos ICT: `references/fvg-ict.md`.
- IBOV, VIX e calendário macro: `references/contexto-macro.md`.
- Risco, dimensionamento e execução: `references/risco-execucao.md`.
- Método quantitativo, backtest e vieses: `references/pesquisa-quantitativa.md`.
- Termos e unidades: `references/glossario.md`.
- Sequência de análise intradiária: `workflows/analise-intraday.md`.
- Definição de setup e avaliação: `workflows/pesquisa-estrategia.md`.
- Casos de comportamento: `tests/casos-de-teste.md`.

## Fluxo de análise completa

1. **Instrumento e dados:** contrato/vencimento, data, sessão, fuso, timeframe, fonte, timestamp, granularidade e latência.
2. **Integridade:** verificar lacunas, duplicados, ordenação, valores impossíveis e qualidade da classificação de agressor.
3. **Contexto:** calendário económico, eventos, IBOV e VIX, sem confundir mercados ou unidades.
4. **Preço:** estrutura, níveis observáveis, amplitude, volatilidade e reação do preço.
5. **Referências temporais/preço:** VWAP, TWAP, distância, inclinação e gap, com janela explícita.
6. **Fluxo:** trades, agressão, delta, volume por contrato e financeiro, spread e ritmo.
7. **Padrões:** FVG/ICT apenas com regras objetivas, contexto, mitigação e invalidação.
8. **Cenários:** principal, alternativo e não operação; cada um com condições observáveis.
9. **Risco:** gatilho condicional, invalidação, stop, objetivos, sizing somente com parâmetros confirmados, custos e riscos de execução.
10. **Conclusão:** evidência favorável/contrária, incerteza, dados ausentes e o que mudaria a leitura.

Adapte a profundidade ao pedido. Uma pergunta conceitual não exige executar o fluxo completo.

## Pesquisa e estratégias

Antes de avaliar uma estratégia, formalize hipótese, universo, período, dados, granularidade, regras determinísticas, horários, filtros, entrada, saída, stop e sizing. Separe treino, validação e teste fora da amostra. Inclua custos, slippage e plausibilidade de execução. Controle look-ahead, survivorship, data snooping e overfitting. Reporte amostra, expectativa, payoff, fator de lucro, drawdown e incerteza quando calculáveis. Diferencie backtest, paper trading e execução real.

## Formato de resposta recomendado

- **Instrumento e dados:** o que foi analisado e qualidade dos dados.
- **Factos observados:** valores e comportamentos diretamente verificáveis.
- **Interpretação:** inferências e hipóteses, com evidência favorável e contrária.
- **Cenários:** principal, alternativo e não operação.
- **Risco e invalidação:** condições que tornam a tese inválida.
- **Limitações:** dados ausentes, premissas e incerteza.
- **Fontes:** nome, URL, data de consulta e data/versão do conteúdo.

Não invente níveis, cotações, indicadores, eventos, estatísticas ou resultados. Não prometa ganhos. Dados históricos não garantem desempenho futuro.
