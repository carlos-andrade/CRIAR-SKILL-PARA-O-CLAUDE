# Microestrutura e fluxo

## Conceitos e granularidade

- **Tick de preço:** incremento mínimo permitido de cotação. No WIN, a página B3 consultada informa tick de 5 pontos; reconfirmar a regra vigente.
- **Trade/negócio:** execução entre participantes. Um negócio pode envolver quantidade variável de contratos.
- **Quantidade de negócios:** contagem de execuções, não contratos.
- **Volume em contratos:** soma da quantidade executada.
- **Volume financeiro:** valor monetário negociado segundo convenção explicitada.
- **Tick chart:** gráfico que agrega dados após número definido de eventos/negócios, conforme implementação da plataforma; não é sinónimo de tick de preço.

## Agressão

A classificação do agressor procura identificar o lado que iniciou a execução (comprador ou vendedor agressor), em geral com base na interação com bid/ask observados. O método depende do feed, sequência de atualizações, condições de mercado e política do fornecedor.

Quando bid/ask ou ordenação não são confiáveis, a classificação pode ser ambígua. O método uptick/downtick ou inferências baseadas no preço têm limitações e não recuperam necessariamente a intenção real do participante.

Sempre reportar:
- método de classificação e fornecedor;
- proporção de volume/negócios classificados;
- proporção não classificada;
- tratamento de negócios fora de mercado regular, cruzamentos ou correções, se aplicável.

## Spread, liquidez e ritmo

Spread é a diferença entre melhor oferta de venda e melhor oferta de compra. Profundidade, reposição/cancelamento de ofertas, tamanho executado e frequência de negócios contextualizam a liquidez, mas livro visível não revela toda a liquidez latente.

Ritmo pode ser descrito por negócios por unidade de tempo, contratos por unidade de tempo e tamanho médio/mediano por negócio. Não substituir estas métricas umas pelas outras.

## Limitações

- Agregação em candles perde a sequência intrabar.
- Feed de negócios sem livro limita classificação do agressor.
- Feed consolidado pode ter latência, correções ou omissões.
- Cumulative delta depende do algoritmo e reinício.
- Ausência de agressor classificado não equivale a ausência de fluxo.
- Nenhuma métrica isolada prova absorção, exaustão ou atuação institucional.

## Leitura disciplinada

Descreva observação, hipótese e confirmação separadamente. Exemplo: “O preço avançou, mas o delta não acompanhou” é observação; “pode haver perda de pressão compradora” é hipótese; confirmação requer reação subsequente, contexto de liquidez e dados adequados.
