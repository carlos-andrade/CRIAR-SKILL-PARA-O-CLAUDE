# Workflow — análise de fluxo e microestrutura

## Objetivo

Avaliar se a atividade negociada, a agressão classificada e a resposta do preço são compatíveis com continuidade, equilíbrio ou possível absorção. O procedimento não presume intenção institucional e não gera entrada automática.

## 1. Contrato e qualidade dos dados

Registar:
- símbolo e vencimento WIN, data e sessão;
- timezone, fonte, timestamp de receção e timestamp de mercado;
- granularidade (trades, quotes L1, livro L2 ou candles);
- latência conhecida, lacunas, duplicados, correções e ordenação;
- unidade de quantidade e convenção de preço;
- política de negócios especiais e fora de sessão.

Não avançar para leitura de agressão se trades e quotes não puderem ser sincronizados de forma defensável. Se houver apenas candles, declarar que a sequência intrabar e a classificação do agressor não são observáveis.

## 2. Classificação do agressor

Para cada negócio elegível, guardar preço, quantidade, timestamp, bid/ask de referência e classificação:
- compra agressora;
- venda agressora;
- não classificado.

Documentar algoritmo e regra de sincronização. Não converter automaticamente negócios ambíguos em compra ou venda.

Calcular cobertura por volume e por negócios. Definir previamente o mínimo aceitável para o estudo; não existe um limiar universal. Se a cobertura cair abaixo do critério definido, reduzir o grau de confiança ou invalidar a janela.

## 3. Delta e CVD

Por janela:
- BuyAgg = soma dos contratos classificados como compra agressora;
- SellAgg = soma dos contratos classificados como venda agressora;
- Delta = BuyAgg − SellAgg;
- Imbalance = Delta / (BuyAgg + SellAgg), se o denominador for positivo;
- CVD = acumulação do delta desde reset explícito.

Reportar sempre volume não classificado. Não comparar níveis absolutos de CVD entre sessões com resets distintos. Para comparar janelas, priorizar delta incremental e imbalance, com cobertura semelhante.

## 4. Atividade versus deslocamento

Escolher uma janela fixa antes de observar o resultado (por exemplo, 1, 3 ou 5 minutos, conforme a granularidade e objetivo do estudo). Usar mid-price sincronizado quando disponível; caso contrário, usar preço de negócio e declarar a limitação.

Calcular:
- deslocamento líquido = preço final − preço inicial;
- deslocamento absoluto em pontos e ticks;
- excursão máxima favorável e adversa;
- contratos agressivos por lado e volume não classificado;
- negócios por unidade de tempo;
- contratos por unidade de tempo;
- eficiência direcional = |Pf − Pi| / soma das variações absolutas sucessivas.

Se a soma das variações absolutas for zero, eficiência é indefinida. Não calcular volume/deslocamento quando deslocamento for zero; reportar a condição diretamente.

## 5. Baseline

Comparar com janelas históricas equivalentes:
- mesma faixa horária/sessão;
- mesma duração e método de amostragem;
- regime ou volatilidade comparável, se disponível.

Apresentar tamanho da amostra, mediana, quantis e/ou MAD. Os thresholds de atividade elevada e deslocamento reduzido devem ser escolhidos no conjunto de treino e congelados antes da validação/teste. Não selecionar percentis depois de ver o trade ou a reação.

## 6. Classificação descritiva

Usar rótulos condicionais, nunca sinais automáticos:

- **Atividade baixa:** volume/ritmo abaixo do baseline definido.
- **Atividade elevada com deslocamento:** atividade acima do baseline e deslocamento relevante.
- **Atividade elevada sem deslocamento proporcional:** atividade acima do baseline e deslocamento abaixo do critério pré-definido.
- **Dados inconclusivos:** cobertura, sincronização ou qualidade insuficientes.

A última condição não é neutra: impede inferências fortes.

## 7. Candidato a absorção

Só classificar como candidato quando, simultaneamente:
1. agressão de um lado é elevada contra baseline comparável;
2. deslocamento na direção dessa agressão é reduzido;
3. cobertura e sincronização satisfazem critérios de qualidade;
4. a janela e thresholds foram definidos antes da avaliação.

Se houver L2, observar reposição persistente de liquidez passiva no preço relevante, sem confundir cancelamentos com execução. Sem L2, não alegar reposição/absorção observada.

A deteção não é confirmação. Definir antecipadamente um horizonte posterior H e uma regra de confirmação (por exemplo, rejeição/retorno além de nível ou ausência de continuação, com distância e tempo definidos). Definir também invalidação. Não usar o futuro para escolher retrospectivamente a janela.

## 8. Cenários e decisão

Produzir:
- observação e cálculo;
- hipótese principal e hipótese alternativa;
- evidência que favorece e contraria cada uma;
- evento que confirmaria ou invalidaria a hipótese;
- condição de não operação quando feed, cobertura, spread, liquidez ou risco forem inadequados.

Uma hipótese de absorção não é por si só gatilho de entrada. A execução exige setup completo, risco dimensionado e custos plausíveis.

## 9. Auditoria e pesquisa

Guardar parâmetros, janelas, baseline, filtros, versão do classificador e regras de confirmação. Testar fora da amostra, incluir custos/slippage e reportar número de candidatos, confirmações, falsos positivos, taxa-base e incerteza. Evitar look-ahead: nenhuma variável posterior pode participar na deteção.

## 10. Saída mínima

| Campo | Resultado |
|---|---|
| Contrato/sessão/fuso | Identificação |
| Fonte/granularidade/latência | Proveniência |
| Cobertura por volume/negócios | Qualidade |
| BuyAgg/SellAgg/Delta/CVD | Contratos |
| Volume não classificado | Contratos e negócios |
| Atividade | Negócios e contratos por tempo |
| Preço inicial/final | Pontos |
| Deslocamento/excursões | Pontos e ticks |
| Baseline | Janela, amostra, quantis |
| Classificação | Descritiva e condicional |
| Hipótese | Evidência favorável/contrária |
| Confirmação/invalidação | Regras e horizonte |
| Limitações | Dados ausentes e incerteza |
