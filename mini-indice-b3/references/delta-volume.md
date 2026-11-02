# Delta acumulado, volume e atividade

## Delta por janela

Para negócios elegíveis com agressor classificado:

\[
BuyAgg_t = \sum_i q_i\,1(a_i=buy),\quad
SellAgg_t = \sum_i q_i\,1(a_i=sell)
\]

\[
Delta_t = BuyAgg_t - SellAgg_t
\]

A unidade é contratos. Negócios sem agressor classificado não entram arbitrariamente em nenhum dos lados; devem ser reportados à parte. Se o fornecedor disponibilizar correções/cancelamentos, aplicar a política documentada antes da agregação.

Imbalance normalizado:

\[
I_t = \frac{BuyAgg_t-SellAgg_t}{BuyAgg_t+SellAgg_t}
\]

I_t pertence a [-1,1] quando o denominador é positivo. Se não houver volume classificado, o valor é indefinido, não zero.

## Cumulative Volume Delta (CVD)

\[
CVD_t = CVD_{t-1}+Delta_t
\]

Definir unidade, sessão/reset, fonte, método de agressão e tratamento de dados atrasados. O CVD é dependente do ponto de reinício: comparar séries com resets diferentes pode ser enganador. Para comparar janelas, usar também delta incremental e imbalance normalizado.

Reportar cobertura:
- cobertura por volume = volume classificado / volume elegível;
- cobertura por negócios = negócios classificados / negócios elegíveis.

Não assumir que cobertura elevada garante classificação correta; verificar sincronização, latência e método do fornecedor.

## Divergência preço–delta

Preço em alta com delta fraco/negativo, ou preço em baixa com delta forte/positivo, pode ser uma divergência. Formalizar:
- extremos de preço e CVD dentro da mesma janela;
- método de comparação (máximos/mínimos locais, regressão ou variação);
- horizonte temporal e tolerância;
- cobertura mínima definida antes do teste.

É uma observação de desacoplamento entre preço e agressão classificada, não prova de absorção nem reversão. Pode ocorrer por liquidez passiva, mudança de composição dos negócios, classificação errada, diferenças de janela ou outros mecanismos.

## Volume por dimensão

Manter separados:
- quantidade de negócios;
- volume em contratos;
- volume financeiro;
- volume por preço;
- ritmo (contratos ou negócios por tempo).

Volume financeiro pode ser calculado segundo convenção de preço × quantidade × multiplicador contratual, mas é necessário declarar se corresponde a nocional negociado, fluxo de caixa ou outra medida. Não tratar volume financeiro como dinheiro líquido que entrou no mercado.

## Expansão, contração e baseline

Comparar atividade com baseline apropriado: mesma faixa horária, sessão, dia da semana ou regime. Valores absolutos sem sazonalidade intradiária podem induzir erro.

Usar medidas robustas (mediana, quantis, MAD) e declarar período de referência, número de observações e tratamento de eventos extremos. Não escolher baseline após observar o resultado.

Volume elevado sem deslocamento relevante pode ser compatível com negociação bilateral intensa, absorção, equilíbrio, reposição de liquidez ou dados defeituosos. Não distingue sozinho essas hipóteses. Rompimento com volume reduzido pode ser vulnerável, mas precisa de contexto de liquidez, spread e continuidade.

## Relação atividade–deslocamento

Definir uma janela e preço de referência inicial/final. Reportar atividade compradora/vendedora, volume não classificado, deslocamento em pontos/ticks, excursões intrajanela e eficiência direcional:

\[
E = \frac{|P_f-P_i|}{\sum_{k=1}^{n}|P_k-P_{k-1}|}
\]

E é indefinida se o denominador for zero. Valores baixos indicam percurso pouco direcional, não absorção. Volume dividido por deslocamento é instável quando o deslocamento se aproxima de zero; não calcular como infinito nem atribuir significado direcional.

## Candidato a absorção — requisitos mínimos

Uma hipótese de absorção exige, no mínimo:
1. agressão classificada elevada relativamente a janelas comparáveis;
2. deslocamento reduzido na direção dessa agressão;
3. cobertura e qualidade do feed aceitáveis;
4. resposta posterior do preço coerente com defesa/rejeição, avaliada num horizonte definido previamente.

Dados L2 com reposição de oferta podem reforçar a leitura, mas não provam identidade nem intenção institucional. Sem L2, descrever apenas atividade agressora elevada com deslocamento limitado. Definir antecipadamente deteção, confirmação, invalidação e horizonte; medir falsos positivos fora da amostra.

## Anomalias e qualidade

Identificar picos, zeros inesperados, dados repetidos, mudanças de feed, timestamps fora de ordem e intervalos sem atualização. Não declarar “volume institucional” sem fonte que identifique participantes — dados públicos agregados normalmente não o fazem.