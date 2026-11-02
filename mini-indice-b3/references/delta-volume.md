# Delta acumulado e volume

## Delta

Delta de uma janela = volume classificado como agressão compradora menos volume classificado como agressão vendedora:

Delta_t = BuyAgg_t − SellAgg_t.

Delta acumulado no intervalo:

CVD_t = CVD_(t−1) + Delta_t.

Definir unidade (contratos, não número de trades), sessão/reset, fonte e método de classificação. Reportar volume sem agressor classificado. Reinício por sessão, dia ou período deve ser explícito.

## Divergência, absorção e exaustão

Preço em alta com delta fraco/negativo, ou preço em baixa com delta forte/positivo, pode ser uma divergência. É hipótese de desacoplamento entre preço e agressão classificada, não prova de absorção nem reversão.

Absorção exige evidência contextual de volume/agressão executada sem deslocamento proporcional e resposta posterior do preço. Exaustão requer sinais de perda de atividade/continuidade; não pode ser inferida apenas por candle ou delta.

## Volume por dimensão

Manter separados:
- quantidade de negócios;
- volume em contratos;
- volume financeiro;
- volume por preço;
- ritmo (contratos ou negócios por tempo).

Volume financeiro pode ser calculado segundo convenção de preço × quantidade × multiplicador contratual, mas é necessário declarar se corresponde a nocional negociado, fluxo de caixa ou outra medida. Não tratar volume financeiro como dinheiro líquido que entrou no mercado.

## Expansão e contração

Comparar volume com baseline apropriado: mesma faixa horária, sessão, dia da semana ou regime. Valores absolutos sem sazonalidade intradiária podem induzir erro.

Volume elevado sem deslocamento relevante pode ser compatível com negociação bilateral intensa, absorção ou equilíbrio; não distingue sozinho essas hipóteses. Rompimento com volume reduzido pode ser vulnerável, mas precisa de contexto de liquidez, spread e continuidade.

## Anomalias e qualidade

Identificar picos, zeros inesperados, dados repetidos, mudanças de feed e intervalos sem atualização. Não declarar “volume institucional” sem fonte que identifique participantes — e normalmente dados públicos não o fazem.
