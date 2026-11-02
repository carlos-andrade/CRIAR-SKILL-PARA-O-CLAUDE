# Pesquisa quantitativa e validação de estratégias

## Especificação antes do teste

Documentar hipótese, racional, universo, contrato/rolagem, período, fonte, granularidade, fuso, filtros, horários, regras de entrada/saída, stop, sizing e custos.

Regras devem ser determinísticas e executáveis sem interpretação retroativa. Fixar como são tratados sinais simultâneos, candles incompletos, ordens pendentes e execução intrabar.

## Separação temporal

- Treino: desenvolvimento/estimação.
- Validação: seleção e ajuste limitado.
- Teste fora da amostra: avaliação final sem ajuste.
- Walk-forward: repetição temporal de estimação e teste, quando apropriado.

Não embaralhar séries temporais de modo que informação futura contamine o passado.

## Vieses e ameaças

Controlar:
- look-ahead bias;
- survivorship bias;
- data snooping/multiple testing;
- overfitting e seleção de parâmetros;
- viés de rolagem e séries contínuas ajustadas;
- custos e slippage subestimados;
- execução irrealista e fills impossíveis;
- mudanças de regime e qualidade histórica do feed.

## Métricas

Quando dados permitirem, reportar:
- quantidade de operações e cobertura temporal;
- taxa de acerto;
- ganho/perda médio e payoff;
- expectativa por operação;
- fator de lucro;
- drawdown máximo e duração;
- distribuição por horário, lado e regime;
- exposição, turnover e custos;
- intervalos de confiança ou incerteza de amostragem.

Definições e método de agregação devem acompanhar as métricas. Não declarar estratégia superior com base apenas em lucro líquido, win rate ou uma amostra pequena.

## Evidência

Distinguir:
- backtest: simulação histórica dependente de dados/modelo;
- paper trading: simulação prospectiva, ainda sem execução real;
- trading real: ordens reais, custos e risco operacional.

Relatório deve incluir limitações, amostra, parâmetros testados e resultados negativos. Desempenho passado não garante resultados futuros.
