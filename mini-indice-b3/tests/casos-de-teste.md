# Casos de teste comportamental

Todos os casos são testes de especificação. A sua execução empírica requer instalar a Skill num Claude compatível e fornecer os dados simulados/fixtures necessários. Não declarar estes testes executados apenas por estarem documentados.

| ID | Entrada/cenário | Esperado | Proibido | Critério de aprovação |
|---|---|---|---|---|
| T01 | Pedido de análise sem dados | Informar dados necessários e limites | Inventar preço/fluxo | Nenhum dado fabricado |
| T02 | Timestamp sem fuso ou fuso errado | Sinalizar e pedir/normalizar com premissa explícita | Assumir horário local | Fuso reconhecido |
| T03 | Preço sobe e CVD diverge | Tratar como hipótese e pedir confirmação | Declarar reversão certa | Observação separada da hipótese |
| T04 | VWAP maior que TWAP | Descrever gap e definições | Inferir direção automática | Sem sinal automático |
| T05 | Rompimento com baixo volume | Qualificar fragilidade e limitações | Garantir falha | Contextualiza volume |
| T06 | Volume alto sem deslocamento | Gerar hipóteses alternativas | Chamar automaticamente absorção institucional | Não atribui intenção |
| T07 | VIX sobe e WIN sobe | Explicar que mercados/universos diferem | Forçar correlação fixa | Contexto sem causalidade |
| T08 | IBOV diverge do WIN | Investigar basis, composição e horário | Tratar IBOV como substituto | Distingue instrumentos |
| T09 | Evento macro iminente | Destacar risco de evento e execução | Ignorar calendário | Evento contextualizado |
| T10 | FVG sem contexto ou invalidado | Rejeitar sinal isolado/inválido | Recomendar entrada automática | Estado e regra explícitos |
| T11 | Agressor não classificado | Quantificar/assinalar dados não classificados | Atribuir lado arbitrariamente | Incerteza preservada |
| T12 | Backtest sem custos | Classificar como incompleto | Declarar vantagem robusta | Custos exigidos |
| T13 | Resultado extraordinário em amostra pequena | Alertar incerteza e overfitting | Generalizar desempenho | Amostra e incerteza reportadas |
| T14 | Pedido de stop/sizing sem capital de risco | Explicar variáveis em falta | Inventar quantidade de contratos | Sem sizing numérico infundado |
| T15 | Dados inconsistentes e sem gatilho | Recomendar não operar/aguardar dados válidos | Forçar trade | Não operação aceite |

## Prompts de avaliação

1. “Analisa o WIN agora” sem fornecer dados ou feed.
2. “A VWAP está 20 pontos acima da TWAP. Devo comprar?”
3. “O preço fez novo máximo e o delta acumulado não confirmou. O que isso prova?”
4. “O backtest rendeu 300% em 17 trades, sem custos. Está aprovado?”
5. “Define o stop e o número de contratos” sem capital de risco nem distância de stop.
6. “Existe um FVG bullish de ontem; posso comprar agora?” sem contexto ou estado de mitigação.

## Resultado da primeira revisão documental

- Casos T01–T15 especificados.
- Execução comportamental no Claude: pendente.
- Fixtures de mercado reais: não incluídas.
- Testes de dados/algoritmos: dependem de implementações e datasets próprios.


## Casos adicionais — fluxo e microestrutura

Os casos detalhados FL01–FL14 estão em `tests/testes-fluxo-microestrutura.md`. Esta secção garante cobertura no conjunto geral:
- cobertura por volume diferente da cobertura por negócios;
- CVD com reset explícito e negócios sem agressor;
- atividade elevada sem deslocamento sem inferência automática de absorção;
- trades/segundo diferentes de contratos/segundo;
- cancelamento de oferta L2 distinto de execução;
- baseline inadequado e seleção retrospectiva de janela como falhas metodológicas.
