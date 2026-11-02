# Especificação matemática — VWAP, TWAP e gap

## 1. Objetivo e contrato de cálculo

Este documento define convenções reproduzíveis para calcular VWAP, TWAP, inclinação, dispersão, distância ao preço e gap VWAP–TWAP. O resultado só é comparável quando símbolo, sessão, janela, fuso, fonte, preço de referência e política de dados são compatíveis.

Cada execução deve registar:
- instrumento e contrato/vencimento;
- data da sessão e identificador da janela;
- timestamp inicial e final, com fuso;
- fornecedor, tipo de feed e granularidade;
- preço usado e unidade;
- definição de volume e unidade;
- política de leilões, negócios especiais, correções e intervalos sem negócio;
- versão do algoritmo e parâmetros.

## 2. VWAP por negócios

Para negócios válidos i, com preço p_i e quantidade executada q_i:

VWAP = Σ(p_i q_i) / Σq_i.

- p_i: pontos de índice por contrato.
- q_i: contratos executados.
- Σq_i: contratos executados na janela.
- VWAP: pontos de índice.

Não usar contagem de negócios como ponderador. Um negócio de 1 contrato e um negócio de 50 contratos não têm o mesmo peso.

A quantidade deve ser estritamente positiva e o denominador Σq_i maior que zero. Se não houver negócios válidos, VWAP é indefinida, não zero.

### Exemplo auditável

| Negócio | Preço (pontos) | Quantidade (contratos) | p × q |
|---|---:|---:|---:|
| 1 | 100.000 | 10 | 1.000.000 |
| 2 | 100.010 | 20 | 2.000.200 |
| 3 | 100.005 | 10 | 1.000.050 |
| Total | — | 40 | 4.000.250 |

VWAP = 4.000.250 / 40 = **100.006,25 pontos**.

Os números são ilustrativos e não representam cotação real do WIN.

## 3. VWAP aproximada por candles

Quando só existem candles, pode-se estimar:

VWAP_aprox = Σ(P*_k V_k) / ΣV_k.

P*_k pode ser close, (high + low + close)/3 ou outra convenção declarada. V_k deve ser volume em contratos, se o objetivo for VWAP ponderada por contratos.

Esta aproximação não é idêntica à VWAP por negócios, pois perde a distribuição intrabar de preços e quantidades. Não misturar fontes ou convenções na mesma série sem identificar a quebra metodológica.

## 4. TWAP por tempo

A TWAP deve ponderar o preço pela duração temporal representada, e não pelo número de observações.

Para uma função de preço p(t) definida numa janela [t0,t1]:

TWAP = (1 / (t1 − t0)) × integral[p(t) dt].

Em dados discretizados por intervalos não sobrepostos:

TWAP = Σ(P_j Δt_j) / ΣΔt_j.

- P_j: preço representativo do intervalo (declarar se é mid, último negócio, close ou outro).
- Δt_j: duração do intervalo em segundos ou milissegundos.
- TWAP: pontos de índice.

### Exemplo auditável

| Intervalo | Preço representativo | Duração |
|---|---:|---:|
| 09:00–09:02 | 100.000 | 120 s |
| 09:02–09:03 | 100.010 | 60 s |
| 09:03–09:04 | 100.005 | 60 s |

TWAP = (100.000×120 + 100.010×60 + 100.005×60) / 240 = **100.003,75 pontos**.

O exemplo assume preço constante dentro de cada intervalo. É uma aproximação de integração, não reconstrução perfeita do caminho intraintervalo.

## 5. Intervalos sem negócio e amostragem

A ausência de negócio não significa preço igual a zero. Definir previamente uma política:
- **Last observation carried forward (LOCF):** mantém o último preço observado durante o intervalo; pode representar stale pricing.
- **Midquote:** usa o ponto médio bid/ask, se livro e timestamps forem fiáveis.
- **Excluir intervalo:** altera o domínio temporal da média e deixa de representar a janela completa.
- **Outra regra:** documentar e testar.

Não preencher silenciosamente lacunas. Registar duração total sem observação, percentagem da janela coberta e idade da última observação.

Se os intervalos forem irregulares, ponderar pela duração real. Uma média aritmética de amostras com espaçamento irregular sobrepondera períodos com mais observações.

## 6. Gap VWAP–TWAP

Convenção adotada:

Gap = VWAP − TWAP.

- Gap > 0: VWAP calculada acima da TWAP.
- Gap < 0: VWAP calculada abaixo da TWAP.
- Gap = 0: valores iguais à precisão numérica adotada.

O sinal não define direção futura, pressão compradora/vendedora, manipulação ou intenção institucional.

### Exemplo conjunto

VWAP = 100.006,25; TWAP = 100.003,75.

Gap = **+2,50 pontos**.

A leitura estritamente permitida é: nesta janela e sob estas convenções, o preço médio ponderado por contratos foi 2,50 pontos superior ao preço médio ponderado pelo tempo.

## 7. Normalização

Para comparar gaps em diferentes regimes, pode-se usar:

Gap_z = Gap / σ_ref,

onde σ_ref é uma medida de dispersão de preço calculada numa janela de referência definida, na mesma unidade de pontos. Alternativamente, usar ATR ou outra escala de volatilidade, desde que janela, método e unidade sejam declarados.

Não chamar Gap_z de z-score estatístico padrão se o numerador não estiver centrado por média e desvio-padrão de uma distribuição histórica de gaps. Para z-score histórico:

Z_gap = (Gap_t − média(Gap_hist)) / desvio_padrão(Gap_hist).

Estimar média e desvio apenas com observações disponíveis até t, evitando look-ahead. Verificar estabilidade por horário e regime.

## 8. Distância do preço e inclinação

Distância ao preço de referência:

D_vwap = Preço_atual − VWAP.
D_twap = Preço_atual − TWAP.

Expressar em pontos e, opcionalmente, ticks, usando o tick vigente confirmado. Indicar qual preço atual foi usado (último negócio, mid ou close) e o timestamp.

Inclinação pode ser estimada por:
- diferença entre valor atual e valor de k períodos atrás, dividida pelo tempo decorrido; ou
- coeficiente angular de regressão linear da referência contra tempo.

Declarar unidade (pontos/minuto, por exemplo), janela e método. Não inferir aceleração sem estimar a variação da inclinação.

## 9. Dispersão ponderada em torno da VWAP

Uma medida de dispersão dos preços negociados:

Var_w = Σ[q_i (p_i − VWAP)^2] / Σq_i.
DP_w = sqrt(Var_w).

DP_w está em pontos. É desvio-padrão ponderado por contratos da distribuição dos preços negociados na janela. Não é, por si só, volatilidade futura nem banda de probabilidade.

Para dados por candle, o resultado é aproximação e depende do preço representativo usado.

## 10. Controles de integridade

Rejeitar ou sinalizar:
- timestamps fora da janela ou fora de ordem;
- timestamps sem fuso conhecido;
- quantidade negativa ou nula em negócio que deveria representar execução;
- preço não numérico ou fora de limites plausíveis;
- duplicações sem identificador que permita distinguir correção de novo negócio;
- volume zero com negócios reportados;
- denominador zero;
- janelas VWAP e TWAP desalinhadas;
- gaps de feed e cobertura temporal insuficiente.

Não remover outliers automaticamente. Primeiro classificar se são erro, leilão, negócio válido ou evento extremo.

## 11. Regras de interpretação

1. Descrever o cálculo antes de interpretar.
2. Comparar VWAP e TWAP apenas em janelas e instrumentos compatíveis.
3. Analisar preço, volume, distribuição temporal, volatilidade e liquidez em conjunto.
4. Testar sensibilidade à amostragem do TWAP e à escolha de preço representativo.
5. Tratar gap como estatística descritiva, não como previsão.
6. Não chamar VWAP–TWAP de fluxo institucional sem evidência independente.
7. Se faltar volume por negócio, livro ou timestamps, limitar a conclusão ao nível permitido pelos dados.
