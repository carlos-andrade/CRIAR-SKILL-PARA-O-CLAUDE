# Regimes de mercado e contexto intermercado

## Objetivo e limites

Este documento define como contextualizar o WIN com IBOV, volatilidade implícita, volatilidade realizada, taxas, câmbio e condições macroeconómicas. Contexto é variável explicativa/condicional, não gatilho de entrada. Correlação não prova causalidade e relações históricas podem mudar de regime.

## Instrumentos e referências

### IBOV à vista versus WIN

- IBOV é índice de retorno total calculado a partir de uma carteira teórica de ações e units, com metodologia e rebalanceamentos próprios.
- WIN é contrato futuro negociado, com vencimento, basis, custo de carregamento, expectativas e microestrutura próprios.
- O IBOV é referência contextual do mercado acionista brasileiro, não uma média móvel do WIN nem um substituto da cotação do futuro.

Para comparação estatística:
1. Sincronizar timestamps e sessões.
2. Converter níveis em retornos percentuais/logarítmicos na mesma frequência.
3. Comparar janelas coincidentes e excluir períodos sem cotação válida.
4. Medir correlação móvel e beta apenas como estatísticas históricas.
5. Investigar diferenças de composição, horários, dividendos, basis e rolagem.

Retornos logarítmicos:
\[
r_t=\ln(P_t/P_{t-1})
\]

Beta descritivo do WIN em relação ao IBOV:
\[
\beta=\frac{Cov(r_{WIN},r_{IBOV})}{Var(r_{IBOV})}
\]

Exigir observações sincronizadas, janela e frequência explícitas. Beta não é constante nem garante hedge estável. Não comparar diretamente variações em pontos de índices diferentes.

Basis descritivo:
\[
Basis_t=F_t-S_t,\qquad BasisRel_t=F_t/S_t-1
\]
onde F é preço do futuro e S é a referência à vista, sincronizados e expressos na mesma escala. Basis relativo não é “mispricing” sem estimativa de custo de carregamento, dividendos esperados, prazo até vencimento, financiamento e convenção de cálculo.

### VIX norte-americano e VXBR brasileiro

**Cboe VIX:** mede volatilidade implícita de aproximadamente 30 dias do S&P 500, derivada de preços de opções SPX. É uma referência externa de risco global; não mede diretamente volatilidade do WIN ou do IBOV.

**S&P/B3 Ibovespa VIX (VXBR):** mede volatilidade implícita de aproximadamente 30 dias associada às opções do Ibovespa. É referência mais diretamente relacionada ao mercado acionista brasileiro, mas também não mede diretamente a volatilidade realizada do WIN.

Ambos são medidas implícitas anualizadas, não previsões certas nem direção de mercado. Distinguir:
- nível do índice;
- variação diária/intradiária;
- percentil histórico do nível;
- volatilidade realizada observada;
- prazo e liquidez dos instrumentos de opções subjacentes.

A aproximação de movimento de um desvio padrão para 30 dias, sob convenção anualizada de 365 dias, é:
\[
Move_{30d}\approx V\times\sqrt{30/365}
\]
onde V é volatilidade implícita em forma decimal. É aproximação estatística para o índice subjacente, não alvo de preço, limite máximo ou previsão para WIN.

Não interpretar VIX/VXBR isoladamente como compra ou venda. Investigar divergências, horário, eventos, liquidez das opções e mudanças de regime.

## Volatilidade realizada do WIN

Para retornos logarítmicos em frequência definida:
\[
\sigma_{realizada}=\sqrt{A}\;SD(r_t)
\]
onde A é o fator de anualização adequado à frequência e calendário de amostragem. Documentar A; não misturar volatilidade intradiária, diária e anualizada.

Também podem ser reportados:
- amplitude intradiária em pontos e percentagem;
- range por janela;
- volatilidade realizada por sessão;
- quantis e MAD face ao histórico;
- volatilidade pré/pós-evento.

Não fixar um único número de barras por regime sem justificar frequência e amostragem.

## Regime de mercado — classificação auditável

A Skill deve produzir descrições observáveis e só atribuir rótulos de regime quando as regras forem definidas previamente e testadas. Dimensões possíveis:

1. **Direcionalidade:** retorno líquido versus percurso total, inclinação e persistência.
2. **Volatilidade:** realizada atual versus distribuição histórica comparável.
3. **Amplitude:** range intradiário versus baseline de horário/sessão.
4. **Liquidez:** spread, profundidade, ritmo, slippage e cobertura do feed.
5. **Intermercado:** retorno IBOV, WIN, USD/BRL, taxas e índices externos com timestamps alinhados.
6. **Volatilidade implícita:** VIX e VXBR, nível e variação face ao próprio histórico.
7. **Evento:** proximidade de divulgação macro, decisão monetária, leilão ou notícia relevante.

Rótulos descritivos possíveis (não são sinais):
- direcional/expansivo;
- lateral/baixa eficiência direcional;
- volátil/desordenado;
- compressão/baixa atividade;
- evento/risco elevado;
- dados insuficientes.

Os rótulos precisam de thresholds calibrados apenas no treino e congelados antes da validação/teste. Preferir percentis por horário e regime. Reportar amostra, período e frequência. Se dimensões discordarem, mostrar a discordância; não forçar um rótulo único.

## Intermercado e causalidade

Variáveis externas podem incluir:
- USD/BRL e curvas de juros locais;
- DI futuro e expectativas de Selic;
- Treasuries e dólar norte-americano;
- S&P 500 e Nasdaq;
- commodities relevantes para a composição do IBOV;
- índices de volatilidade VIX e VXBR.

Usar retornos sincronizados, controlar horários e testar estabilidade por subperíodo. Relação contemporânea pode refletir fator comum, resposta a notícia ou efeito de horário. Para estudar precedência temporal, definir lags antes do teste e evitar seleção retrospectiva.

## Fontes institucionais

- B3 — metodologia e composição do Ibovespa: https://www.b3.com.br/pt_br/market-data-e-indices/indices/indices-amplos/ibovespa.htm
- S&P DJI — S&P/B3 Ibovespa VIX: https://www.spglobal.com/spdji/pt/indices/indicators/sp-b3-ibovespa-vix/
- S&P DJI — metodologia VXBR: https://www.spglobal.com/spdji/pt/methodology/article/sp-b3-ibovespa-vix-methodology-portuguese/
- Cboe — VIX FAQ: https://www.cboe.com/tradable_products/vix/faqs
- Banco Central — Copom: https://www.bcb.gov.br/controleinflacao/copom
- IBGE — calendário de divulgações: https://www.ibge.gov.br/calendario-de-divulgacoes-novoript

Consultar sempre as versões vigentes e registar data/hora de acesso.
