# IBOV, VIX, VXBR e contexto macroeconómico

## IBOV e WIN

IBOV é o índice à vista de ações da B3; WIN é contrato futuro. O Ibovespa resulta de uma carteira teórica de ações e units, com critérios de negociabilidade, ponderação e rebalanceamento definidos pela metodologia B3. WIN incorpora prazo, basis, custo de carregamento, dividendos esperados, expectativas e microestrutura própria.

IBOV pode servir de referência contextual para direção e amplitude do mercado acionista brasileiro, mas não é média móvel do WIN nem substituto do preço negociado no contrato. Para comparação quantitativa, sincronizar timestamps e comparar retornos percentuais/logarítmicos, não variações brutas em pontos. Consultar `references/regimes-mercado.md` para basis, beta e correlação.

Fonte: B3 — https://www.b3.com.br/pt_br/market-data-e-indices/indices/indices-amplos/ibovespa.htm

## VIX Cboe e S&P/B3 Ibovespa VIX (VXBR)

Não usar “VIX” como designação genérica de volatilidade brasileira.

- **Cboe VIX:** mede volatilidade implícita de aproximadamente 30 dias do S&P 500, calculada a partir de opções SPX. É uma referência externa de risco global, não volatilidade direta do WIN.
- **S&P/B3 Ibovespa VIX (VXBR):** procura medir a volatilidade implícita de 30 dias do mercado acionista brasileiro, usando opções sobre o Ibovespa. É mais diretamente relacionado ao mercado brasileiro, mas não mede a volatilidade realizada do WIN.

Ambos são medidas implícitas e anualizadas. Nível elevado não determina direção; nível baixo não elimina risco. Distinguir volatilidade implícita, realizada e amplitude observada. Não converter o nível de nenhum dos índices em pontos de WIN.

Fontes:
- Cboe VIX FAQ: https://www.cboe.com/tradable_products/vix/faqs
- S&P/B3 Ibovespa VIX: https://www.spglobal.com/spdji/pt/indices/indicators/sp-b3-ibovespa-vix/
- Metodologia VXBR: https://www.spglobal.com/spdji/pt/methodology/article/sp-b3-ibovespa-vix-methodology-portuguese/

## Calendário económico e vintages

Para cada evento, registar:
- indicador, país e entidade responsável;
- data/hora prevista e efetiva, timezone original e fonte;
- período de referência e unidade;
- consenso disponível antes da divulgação;
- valor anterior e revisão;
- valor realizado e timestamp de publicação;
- surpresa simples e, quando possível, padronizada;
- versão/snapshot da informação conhecida à hora da decisão.

Surpresa simples:
`Surpresa = Realizado − Consenso`.

A surpresa padronizada só é válida com distribuição histórica comparável e estimada sem informação futura. Não calcular quando consenso e realizado tiverem unidades/períodos diferentes.

Não inferir direção do WIN apenas pelo sinal da surpresa. O significado depende do indicador, função de reação do banco central, posicionamento, revisões, expectativas já incorporadas e reação de juros/câmbio.

## Eventos relevantes

- **Banco Central do Brasil:** Copom, Selic, atas, Relatório de Política Monetária, Focus e comunicação oficial.
- **IBGE:** IPCA, INPC, PIB, PNAD Contínua e indicadores de atividade.
- **FGV:** indicadores sob responsabilidade da instituição.
- **Estados Unidos:** Federal Reserve, inflação, emprego, PIB e atividade publicados pelos órgãos oficiais.
- **Outros:** decisões fiscais, leilões, eventos geopolíticos e divulgações relevantes para commodities/câmbio.

Calendário previsto não prova que a divulgação ocorreu no horário anunciado. Confirmar publicação efetiva na fonte primária.

Fontes institucionais:
- BCB — Copom: https://www.bcb.gov.br/controleinflacao/copom
- BCB — Focus: https://www.bcb.gov.br/controleinflacao/relatoriofocus
- IBGE — calendário de divulgações: https://www.ibge.gov.br/calendario-de-divulgacoes-novoript

O Focus resume expectativas reportadas ao Banco Central; não representa previsão ou compromisso do próprio BC. O calendário do IBGE é referência para datas oficiais, mas a hora efetiva deve ser confirmada na publicação.

## Fuso horário

Guardar timezone IANA, não apenas offset numérico. Para eventos brasileiros, usar `America/Sao_Paulo`; para séries norte-americanas, usar timezone da fonte (por exemplo, `America/New_York`). Converter para UTC para alinhamento computacional e preservar timestamp original. Considerar mudanças históricas de horário de verão.

## Interpretação operacional

Próximo de eventos, avaliar spread, profundidade, slippage, volatilidade e risco de gaps. A janela de cautela deve ser parametrizada e validada por evento/instrumento; não inventar um intervalo universal.

O contexto macro altera a confiança e o risco da leitura técnica, não substitui gatilho, invalidação ou gestão de risco. Quando faltarem consenso point-in-time, timestamps ou fonte primária, declarar a limitação e não fabricar surpresa.
