---
name: mini-indice-b3
description: Analisa o mini índice futuro WIN da B3, fluxo, microestrutura, VWAP/TWAP, Cumulative Delta, volume, absorção, IBOV, VIX, VXBR, calendário macro, regimes de mercado, FVG/ICT e risco. Use em perguntas sobre WIN, setups, execução ou backtests.
---

# Mini Índice Futuro B3 (WIN)

Skill para análise verificável do contrato futuro de mini Ibovespa (WIN). O objetivo é apoiar pesquisa e decisões disciplinadas, não emitir sinais automáticos nem prometer rentabilidade.

## Princípios obrigatórios

1. **Identifique o instrumento:** diferencie IBOV à vista, futuro cheio IND e mini futuro WIN. Registe vencimento/série, sessão, timeframe, fonte e timestamp.
2. **Valide os dados antes de interpretar:** granularidade, fuso, latência, campos ausentes, duplicados, negócios sem agressor classificado e eventuais ajustes. Sem dados suficientes, declare o que não pode ser concluído.
3. **Separe epistemicamente:** rotule factos observados, cálculos, inferências, hipóteses e desconhecidos.
4. **Não automatize a interpretação:** VWAP, TWAP, delta, volume, FVG, IBOV, VIX, VXBR e dados macro não são sinais isolados nem prova de intenção institucional.
5. **Integre risco e execução:** custos, slippage, spread, liquidez, risco por operação e limite diário são parte da análise.
6. **Não force trades:** cenário de não operação é uma conclusão válida.
7. **Fontes atuais:** confirme regras contratuais, calendários e metodologias nas fontes oficiais. Indique data de consulta e período de validade. Nunca simule feed em tempo real.

## Roteamento por referência

Consulte apenas o material necessário à tarefa:

- Especificação, vencimento, rolagem e sessões: `references/contrato-win.md`.
- Microestrutura, agressor, spread, ritmo e atividade/deslocamento: `references/microestrutura-fluxo.md`.
- VWAP/TWAP e especificação matemática: `references/vwap-twap.md` e `references/vwap-twap-especificacao-matematica.md`.
- Workflow de cálculo VWAP/TWAP: `workflows/calculo-vwap-twap.md`.
- CVD, delta, cobertura, volume e absorção: `references/delta-volume.md`.
- Workflow de fluxo: `workflows/analise-fluxo-microestrutura.md`.
- Testes de fluxo: `tests/testes-fluxo-microestrutura.md`.
- IBOV, VIX Cboe, VXBR e calendário macro: `references/contexto-macro.md`.
- Regimes, volatilidade realizada, basis e análise intermercado: `references/regimes-mercado.md`.
- Workflow de contexto/regime: `workflows/analise-contexto-regime.md`.
- Testes de contexto/regime: `tests/testes-contexto-regime.md`.
- FVG/ICT: `references/fvg-ict.md`.
- Risco, dimensionamento e execução: `references/risco-execucao.md`.
- Pesquisa quantitativa e vieses: `references/pesquisa-quantitativa.md`.
- Termos e unidades: `references/glossario.md`.
- Análise intradiária: `workflows/analise-intraday.md`.
- Pesquisa de estratégia: `workflows/pesquisa-estrategia.md`.
- Testes VWAP/TWAP: `tests/testes-vwap-twap.md`.
- Casos comportamentais gerais: `tests/casos-de-teste.md`.

## Fluxo de análise completa

1. **Instrumento e dados:** contrato/vencimento, data, sessão, fuso, timeframe, fonte, timestamp, granularidade e latência.
2. **Integridade:** verificar lacunas, duplicados, ordenação, valores impossíveis e qualidade da classificação de agressor.
3. **Contexto macro:** calendário oficial, consenso point-in-time, realizado, anterior/revisão e horário efetivo.
4. **Regime:** volatilidade realizada, amplitude, liquidez, IBOV, VIX Cboe, VXBR e variáveis externas com timestamps alinhados.
5. **Preço:** estrutura, níveis observáveis, amplitude e reação.
6. **Referências:** VWAP/TWAP em janelas alinhadas, distância, inclinação, dispersão e gap.
7. **Fluxo:** trades, agressão, CVD, delta, volume classificado/não classificado, spread, profundidade e ritmo.
8. **Atividade/deslocamento:** baseline comparável; absorção é hipótese sujeita a confirmação posterior.
9. **Padrões:** FVG/ICT com regras objetivas, contexto, mitigação e invalidação.
10. **Cenários e risco:** principal, alternativo e não operação; gatilho condicional, invalidação, stop, objetivos, sizing apenas com parâmetros confirmados, custos e riscos de execução.
11. **Conclusão:** evidência favorável/contrária, incerteza, dados ausentes e o que mudaria a leitura.

Adapte a profundidade ao pedido. Uma pergunta conceitual não exige executar o fluxo completo.

## Pesquisa e estratégias

Formalize hipótese, universo, período, dados, granularidade, regras determinísticas, horários, filtros, entrada, saída, stop e sizing. Separe treino, validação e teste fora da amostra. Inclua custos, slippage e plausibilidade de execução. Controle look-ahead, survivorship, data snooping e overfitting. Para contexto macro, use dados point-in-time, snapshots de consenso e calendário conhecido ex ante. Reporte amostra, expectativa, payoff, fator de lucro, drawdown e incerteza quando calculáveis. Diferencie backtest, paper trading e execução real.

## Formato de resposta recomendado

- **Instrumento e dados:** o que foi analisado e qualidade.
- **Contexto e regime:** eventos, fontes, timestamps, dimensões e eventuais divergências.
- **Factos observados:** valores diretamente verificáveis.
- **Cálculos:** fórmula, unidade, janela, parâmetros e tratamento.
- **Interpretação:** inferências e hipóteses, com evidência favorável e contrária.
- **Cenários:** principal, alternativo e não operação.
- **Risco e invalidação:** condições que tornam a tese inválida.
- **Limitações:** dados ausentes, premissas e incerteza.
- **Fontes:** nome, URL, data de consulta e versão/conteúdo.

Não invente níveis, cotações, indicadores, eventos, consensos, estatísticas ou resultados. Não prometa ganhos. Dados históricos não garantem desempenho futuro.
