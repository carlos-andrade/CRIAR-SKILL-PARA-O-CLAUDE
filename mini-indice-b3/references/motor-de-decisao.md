# Motor de decisão e hierarquia de evidências

## Finalidade

Converter observações validadas em cenários condicionais — comprador, vendedor ou não operar — sem transformar indicadores numa votação nem produzir sinais automáticos. O motor organiza evidência, dependências, contradições, condições de execução e invalidação. Não estima probabilidade de lucro sem modelo calibrado e validado.

## Precedência e gates

A decisão é sequencial. Uma camada posterior não compensa a falha de uma anterior.

1. **Integridade dos dados (gate obrigatório):** contrato/série, sessão, timezone, timestamps, latência, granularidade, consistência, cobertura e fonte.
2. **Segurança operacional (gate obrigatório):** evento iminente, estado da plataforma, spread, profundidade, slippage, limites de risco e possibilidade de execução.
3. **Contexto/regime:** direcionalidade, volatilidade, amplitude, liquidez, intermercado e eventos. Descreve o ambiente; não determina direção.
4. **Estrutura e localização do preço:** tendência/rotação, extremos, rompimento/rejeição, níveis e sequência temporal, definidos por regras observáveis.
5. **Referências:** VWAP/TWAP, gap, inclinação, distância e dispersão; janelas sincronizadas.
6. **Fluxo e atividade:** agressão, delta/CVD, cobertura, volume, trades, ritmo, spread e deslocamento.
7. **Padrões contextuais:** FVG/ICT somente se identificado sem look-ahead, ativo e não invalidado.
8. **Plano condicional:** gatilho, invalidação, stop, objetivos, dimensionamento e custos. Sem plano executável, não operar.

A precedência não declara que uma métrica de mercado é universalmente superior a outra. Significa que não há leitura direcional antes dos gates de dados e risco.

## Dependência e dupla contagem

Não somar variáveis correlacionadas como votos independentes:
- VWAP, TWAP e gap podem derivar da mesma série de preços/negócios.
- Delta, CVD, agressão e volume classificado partilham negócios e classificação do agressor.
- Range, ATR e volatilidade realizada podem medir aspetos sobrepostos.
- IBOV, WIN, VXBR e índices externos podem reagir ao mesmo fator macro.
- FVG é transformação de OHLC, não evidência independente de fluxo.

Registar para cada variável a fonte, dados de origem, janela, transformação e dependências. Agrupar evidências por família. Uma variável só acrescenta confirmação se demonstrar informação condicional incremental fora da amostra.

## Matriz de evidência

Para cada hipótese compradora e vendedora, registar evidência favorável, contrária e qualidade/limitação nas dimensões: estrutura/preço; regime; VWAP/TWAP; fluxo/cobertura; atividade/liquidez; FVG; macro/intermercado. Esta matriz é um registo auditável, não um score. Ausência de dado não equivale a confirmação neutra.

## Regras de saída

### Comprador

Exige gates aprovados, estrutura objetiva, gatilho observável, invalidação verificável, risco dimensionável com parâmetros confirmados e contradições explicitadas. Se o gatilho ainda não ocorreu, escrever **condicional — aguardar gatilho**, nunca “entrada agora”.

### Vendedor

Aplicam-se os mesmos requisitos, avaliados independentemente. Não presumir simetria estatística entre compras e vendas.

### Não operar / aguardar

É a saída obrigatória perante dados inválidos, stale ou desalinhados; gate de risco/execução reprovado; evento iminente não modelado; ausência de estrutura, gatilho ou invalidação; sizing impossível por falta de parâmetros; conflito material sem regra prévia; liquidez inadequada; ou limite operacional atingido. Não operar é decisão válida, não falha do motor.

## Gatilho, invalidação e risco

Todo cenário direcional deve declarar condição e timeframe do gatilho, momento em que fica conhecido, condição de invalidação, stop operacional, objetivos, capital de risco, multiplicador vigente, contratos, custos, slippage, spread, liquidez, execução parcial e limite diário. Se faltar parâmetro essencial, não inventar preço, stop ou quantidade. Stop não garante execução ao preço definido.

## Linguagem epistemológica

Distinguir facto observado, cálculo reproduzível, inferência, hipótese e desconhecido. Não declarar “institucional”, “absorção”, “manipulação” ou “intenção” como facto sem evidência específica. Não fornecer confiança percentual subjetiva. Probabilidades exigem evento e horizonte definidos, amostra, validação e calibração fora da amostra.

## Avaliação

Congelar regras no treino; avaliar compra e venda separadamente; usar validação walk-forward e teste final intocado; comparar com baseline simples e política de não operar; medir frequência de cenários, falsos positivos, expectativa líquida, payoff, fator de lucro, drawdown e custos; segmentar por regime, horário, vencimento e lado; executar ablação por família e sensibilidade a thresholds, latência, slippage e execução. Só considerar valor incremental se superar baselines fora da amostra após custos. Backtest não equivale a paper trading nem execução real.
