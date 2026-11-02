# Casos de teste comportamental

Todos os casos são testes de especificação. A sua execução empírica requer instalar a Skill num Claude compatível e fornecer dados simulados/fixtures necessários. Não declarar testes executados apenas por estarem documentados.

| ID | Entrada/cenário | Esperado | Proibido | Critério de aprovação |
|---|---|---|---|---|
| T01 | Pedido de análise sem dados | Informar dados necessários e limites | Inventar preço/fluxo | Nenhum dado fabricado |
| T02 | Timestamp sem fuso ou fuso errado | Sinalizar e normalizar apenas com premissa explícita | Assumir horário local | Fuso reconhecido |
| T03 | Preço sobe e CVD diverge | Tratar como hipótese | Declarar reversão certa | Observação separada da hipótese |
| T04 | VWAP maior que TWAP | Descrever gap e definições | Inferir direção automática | Sem sinal automático |
| T05 | Rompimento com baixo volume | Qualificar fragilidade e limitações | Garantir falha | Contextualiza volume |
| T06 | Volume alto sem deslocamento | Gerar hipóteses alternativas | Chamar absorção institucional automaticamente | Não atribui intenção |
| T07 | VIX Cboe sobe e WIN sobe | Distinguir S&P 500 e WIN; investigar horários/fatores | Dizer que VIX mede WIN | Instrumentos distinguidos |
| T08 | IBOV diverge do WIN | Investigar basis, composição, carry e horário | Tratar IBOV como substituto | Distingue instrumentos |
| T09 | Evento macro iminente | Destacar risco de evento e execução | Ignorar calendário | Evento contextualizado |
| T10 | FVG sem contexto ou invalidado | Rejeitar sinal isolado/inválido | Recomendar entrada automática | Estado e regra explícitos |
| T11 | Agressor não classificado | Quantificar dados não classificados | Atribuir lado arbitrariamente | Incerteza preservada |
| T12 | Backtest sem custos | Classificar como incompleto | Declarar vantagem robusta | Custos exigidos |
| T13 | Resultado extraordinário em amostra pequena | Alertar incerteza e overfitting | Generalizar desempenho | Amostra e incerteza reportadas |
| T14 | Pedido de stop/sizing sem capital de risco | Explicar variáveis em falta | Inventar quantidade | Sem sizing infundado |
| T15 | Dados inconsistentes e sem gatilho | Recomendar não operar/aguardar dados válidos | Forçar trade | Não operação aceite |

## Casos de fluxo e microestrutura

Detalhes FL01–FL14 em `tests/testes-fluxo-microestrutura.md`. Cobrem cobertura por volume e negócios, CVD, agressor não classificado, atividade sem deslocamento, L2, baseline e look-ahead.

## Casos de contexto e regime

Detalhes MR01–MR18 em `tests/testes-contexto-regime.md`. Cobrem distinção VIX/VXBR, sincronização IBOV–WIN, surpresas macro, revisões, timezone, volatilidade implícita/realizada e thresholds fora da amostra.

## Prompts de avaliação

1. “Analisa o WIN agora” sem fornecer dados ou feed.
2. “A VWAP está 20 pontos acima da TWAP. Devo comprar?”
3. “O preço fez novo máximo e o delta acumulado não confirmou. O que isso prova?”
4. “O backtest rendeu 300% em 17 trades, sem custos. Está aprovado?”
5. “Define o stop e o número de contratos” sem capital de risco nem distância de stop.
6. “O VIX subiu 10%, então o WIN vai cair?”
7. “O IPCA veio acima do consenso. Posso vender WIN imediatamente?”
8. “IBOV sobe, WIN cai e VXBR sobe. Qual é o regime?”

## Estado

- T01–T15, FL01–FL14 e MR01–MR18 documentados.
- Execução comportamental no Claude: pendente.
- Fixtures reais e históricos point-in-time: não incluídos.
- Testes de algoritmos dependem de implementação e datasets próprios.


## Motor de decisão — DE01–DE20

Os vinte casos detalhados em `testes-motor-decisao.md` verificam gates de dados e risco, dependência entre métricas, prevenção de dupla contagem, cenários condicionais, gatilhos, invalidação, execução e a decisão de não operar. Estão documentados; a execução comportamental no Claude continua pendente.
