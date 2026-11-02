# Microestrutura e fluxo

## Conceitos e granularidade

- **Tick de preço:** incremento mínimo permitido de cotação. No WIN, a página B3 consultada informa tick de 5 pontos; reconfirmar a regra vigente.
- **Trade/negócio:** execução entre participantes. Um negócio pode envolver quantidade variável de contratos.
- **Quantidade de negócios:** contagem de execuções, não contratos.
- **Volume em contratos:** soma da quantidade executada.
- **Volume financeiro:** valor monetário negociado segundo convenção explicitada.
- **Tick chart:** gráfico que agrega dados após número definido de eventos/negócios, conforme implementação da plataforma; não é sinónimo de tick de preço.

## Agressão e classificação

A classificação do agressor procura identificar o lado que iniciou a execução. Com cotações confiáveis, negócios no ask são normalmente classificados como compra agressora e negócios no bid como venda agressora. Negócios entre bid e ask, quotes desatualizadas, mudanças concorrentes e feeds sem sequência consistente podem ficar ambíguos.

Métodos baseados apenas em uptick/downtick são aproximações e não recuperam necessariamente a intenção do participante. Não presumir que dois fornecedores usam o mesmo algoritmo.

Para cada amostra, registar:
- fonte/feed, método e versão do classificador;
- timestamp e regra de sincronização entre trades e quotes;
- volume classificado como compra e venda agressora;
- volume e número de negócios não classificados;
- cobertura por volume e por número de negócios;
- política para negócios corrigidos, cancelados, cruzados ou fora da sessão, quando esses campos existirem.

Definições de cobertura:
- cobertura por volume = volume classificado / volume total elegível;
- cobertura por negócios = negócios classificados / negócios totais elegíveis.

As duas coberturas não são intercambiáveis. Um pequeno número de negócios grandes não classificados pode degradar mais a cobertura por volume do que a cobertura por contagem.

## Spread, liquidez e ritmo

Spread = melhor ask − melhor bid, medido em pontos ou ticks. Profundidade visível, reposição/cancelamento de ofertas, tamanho executado e frequência de negócios contextualizam a liquidez. O livro visível não revela toda a liquidez latente e pode mudar antes da execução.

Medir separadamente:
- negócios por segundo/minuto;
- contratos por segundo/minuto;
- tamanho médio e mediano por negócio;
- spread médio, mediano e percentis;
- profundidade disponível por nível, se houver dados L2;
- proporção de tempo com quote válida e sincronizada.

Ritmo elevado de negócios não significa necessariamente grande volume; volume elevado não significa necessariamente elevada contagem de negócios.

## Atividade versus deslocamento

Uma leitura de “atividade sem deslocamento” deve comparar a atividade executada com a mudança efetiva do preço numa janela definida. No mínimo, declarar:
- janela temporal e critério de inclusão;
- volume agressor comprador/vendedor e não classificado;
- preço de referência inicial/final (preferencialmente mid válido; caso contrário, indicar preço de negócio);
- deslocamento absoluto em pontos e ticks;
- excursão máxima favorável/adversa dentro da janela;
- baseline comparável, idealmente mesma faixa horária e regime.

Métrica descritiva possível:
- eficiência direcional = |preço_final − preço_inicial| / soma(|variações sucessivas do preço|).

A métrica fica entre 0 e 1 quando a série e a amostragem são consistentes; valores baixos indicam percurso pouco direcional, não absorção. Se o denominador for zero, a métrica é indefinida. Outra medida, volume por tick de deslocamento, é instável quando o deslocamento é zero; nesse caso reportar “sem deslocamento observado”, não dividir por zero.

Não usar thresholds universais. Comparar com distribuição histórica de janelas equivalentes, mediana, quantis ou desvio absoluto mediano (MAD), com tamanho de amostra declarado.

## Hipótese de absorção

Um candidato a absorção pode ser investigado quando há agressão executada elevada relativamente ao baseline, deslocamento reduzido na direção da agressão e resposta de preço compatível com defesa/rejeição. Evidência de reposição persistente no livro pode reforçar a hipótese, mas exige dados L2 adequados.

Sem sequência de quotes/profundidade, a leitura é apenas “atividade agressora elevada com deslocamento limitado”; não afirmar absorção observada. Mesmo com L2, não inferir identidade, intenção ou caráter institucional do participante.

Para evitar circularidade, separar:
1. **Deteção:** janela que satisfaz critérios quantitativos definidos antes do teste.
2. **Confirmação:** comportamento posterior do preço dentro de horizonte predefinido.
3. **Invalidação:** deslocamento sustentado contra a hipótese ou perda do nível/contexto definido.
4. **Avaliação:** frequência, payoff e falsos positivos em amostra fora do período de desenho.

Não usar a reação posterior para retroativamente escolher a janela de deteção.

## Limitações

- Agregação em candles perde a sequência intrabar.
- Feed de negócios sem livro limita classificação do agressor.
- Feed consolidado pode ter latência, correções ou omissões.
- Cumulative Delta depende do algoritmo e reinício.
- Ausência de agressor classificado não equivale a ausência de fluxo.
- Livro visível não representa toda a liquidez nem garante execução.
- Nenhuma métrica isolada prova absorção, exaustão ou atuação institucional.

## Leitura disciplinada

Descreva observação, hipótese e confirmação separadamente. Exemplo: “Houve volume agressor comprador acima do percentil 90 das janelas comparáveis e o mid deslocou apenas 1 tick” é uma observação calculada; “pode existir oferta passiva a limitar o avanço” é hipótese; a confirmação depende de critérios posteriores predefinidos.