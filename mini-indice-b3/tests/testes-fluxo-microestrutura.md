# Testes — fluxo e microestrutura

Estes casos são especificações de teste. Não representam execução real até serem executados contra uma implementação e/ou numa sessão Claude com fixtures controladas.

## Convenções

- Quantidades em contratos.
- BuyAgg e SellAgg incluem apenas agressor classificado.
- Não classificado é reportado separadamente.
- CVD reinicia no início da sessão de teste.
- Thresholds de baseline são fornecidos como parte da fixture; não devem ser inferidos depois do resultado.

## Casos

| ID | Fixture/entrada | Esperado | Proibido | Critério de aprovação |
|---|---|---|---|---|
| FL01 | 120 contratos buy, 80 sell, 10 não classificados | Delta +40; total elegível 210; cobertura por volume 200/210 = 95,24% | Incorporar os 10 como compra | Fórmulas e unidade corretas |
| FL02 | BuyAgg=0 e SellAgg=0 | Imbalance indefinido | Reportar 0 como se fosse equilíbrio observado | Denominador zero tratado |
| FL03 | Delta por barras +20, -5, +10 com reset inicial zero | CVD 20, 15, 25 | Misturar sessões | Acumulação correta |
| FL04 | 80% dos negócios classificados, mas só 40% do volume | Assinalar cobertura discrepante | Dizer que a cobertura é simplesmente 80% | Coberturas separadas |
| FL05 | Preço faz novo máximo; CVD não faz novo máximo | Divergência possível, não prova de reversão | Garantir reversão/absorção | Facto e hipótese separados |
| FL06 | Volume agressor elevado e deslocamento de 1 tick, baseline confirma extremos | Atividade elevada sem deslocamento proporcional; candidato apenas se os demais critérios forem satisfeitos | Chamar absorção confirmada sem resposta posterior/L2 | Linguagem condicional |
| FL07 | Volume alto, preço parado, agressor não classificado em grande proporção | Dados inconclusivos | Inferir lado agressor | Qualidade bloqueia inferência |
| FL08 | Ritmo de trades aumenta, contratos por minuto não aumentam | Distinguir contagem e volume | Chamar aumento de volume | Métricas separadas |
| FL09 | Livro L2 mostra oferta visível que é cancelada, não executada | Não contar cancelamento como absorção executada | Tratar cancelamento como negócio | Execução e cancelamento distintos |
| FL10 | Janela de deteção selecionada após observar rejeição posterior | Rejeitar desenho por look-ahead | Reportar desempenho válido | Temporalidade respeitada |
| FL11 | Feed sem quotes sincronizadas | Declarar limitação da classificação | Afirmar agressor com precisão | Limite do feed explícito |
| FL12 | Baseline de horários diferentes e amostra pequena | Alertar comparação inadequada/incerteza | Aplicar threshold como universal | Baseline auditável |
| FL13 | Volume financeiro aumenta por mudança de preço, contratos constantes | Separar efeito preço e quantidade | Dizer que entraram mais contratos | Unidades preservadas |
| FL14 | Eficiência direcional com percurso sem variação | Métrica indefinida | Divisão por zero | Tratamento matemático correto |

## Fixtures aritméticas de referência

1. BuyAgg=120, SellAgg=80:
   - Delta = +40 contratos.
   - Imbalance = 40/200 = 0,20.
2. Volume elegível=210 contratos, dos quais 200 classificados:
   - Cobertura por volume = 200/210 = 0,952380… (95,24%).
3. Deltas +20, −5, +10:
   - CVD desde zero = 20, 15, 25 contratos.

## Critérios globais

- Nenhum lado atribuído aos negócios não classificados.
- Nenhuma conclusão de absorção institucional baseada apenas em volume alto e preço parado.
- Deteção, confirmação e invalidação definidas separadamente.
- Baseline e thresholds estabelecidos antes do teste.
- Custos, slippage e execução considerados antes de qualquer conclusão de rentabilidade.
- Se a qualidade dos dados for insuficiente, a conclusão deve ser “inconclusivo” ou “não operar”, conforme o pedido.

## Estado

- Casos FL01–FL14 documentados.
- Aritmética das três fixtures de referência verificada diretamente.
- Execução automatizada do classificador/CVD: pendente.
- Teste comportamental no Claude: pendente.
- Validação com feed real de trades/quotes/L2: pendente.
