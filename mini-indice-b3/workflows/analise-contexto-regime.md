# Workflow — contexto macro e regime de mercado do WIN

## 1. Identificação e relógio

Registar:
- contrato WIN e vencimento;
- data, sessão e timezone IANA;
- timestamp do mercado e da receção;
- fonte, frequência, latência e disponibilidade;
- séries comparadas: IBOV, VXBR, VIX, USD/BRL, juros e índices externos.

Converter timestamps para uma base comum, preservando timezone original. Usar America/Sao_Paulo para o calendário brasileiro e timezone da fonte para séries externas. Não assumir que UTC, hora de Portugal e hora de Brasília coincidem.

## 2. Calendário e eventos

Antes de interpretar:
1. Consultar calendários oficiais relevantes.
2. Registar evento, país, entidade, hora prevista e hora efetiva.
3. Capturar consenso disponível antes da divulgação, valor anterior e respetiva revisão, realizado e timestamp da publicação.
4. Registar unidade e período de referência.
5. Calcular surpresa apenas quando consenso e realizado forem comparáveis.

Surpresa simples:
\[
Surpresa=Realizado-Consenso
\]

Surpresa padronizada:
\[
Surpresa_z=\frac{Realizado-Consenso}{SD(Realizado-Consenso)}
\]
O desvio-padrão deve ser estimado com histórico comparável e sem usar informação futura. Se a amostra for insuficiente, reportar apenas diferença absoluta ou classificar como não padronizada.

Não assumir que surpresa positiva é bullish ou bearish. O significado depende do indicador, reação esperada de política monetária, revisões, posicionamento e regime. Uma inflação acima do consenso pode ter interpretação diferente consoante a função de reação do banco central e o que já estava precificado.

## 3. IBOV versus WIN

- Sincronizar cotações e converter para retornos.
- Comparar retorno percentual, amplitude e direção em janelas idênticas.
- Calcular basis apenas com preço à vista e futuro contemporâneos.
- Registar vencimento e dias até expiração.
- Em série contínua, identificar método de rolagem e não tratar preço ajustado como executável.

Divergência é objeto de investigação, não sinal. Verificar diferenças de sessão, composição, dividendos, juros, basis e liquidez.

## 4. VIX e VXBR

Identificar explicitamente qual índice foi fornecido:
- VIX Cboe: opções do S&P 500, risco implícito dos EUA.
- VXBR: opções do Ibovespa, risco implícito do Brasil.

Para cada um, obter nível, variação, timestamp, fonte, percentil histórico e qualidade da cotação. Comparar apenas períodos com dados disponíveis e horários sobrepostos. Não transportar a escala do VIX para WIN nem confundir volatilidade implícita com realizada.

## 5. Volatilidade e regime

Calcular volatilidade realizada e range do WIN em janelas definidas. Comparar com baseline histórico por faixa horária e sessão. Construir uma matriz de dimensões:

| Dimensão | Métricas possíveis |
|---|---|
| Direcionalidade | retorno líquido, eficiência direcional, persistência |
| Volatilidade | desvio-padrão realizado, range, percentis |
| Liquidez | spread, profundidade, slippage, cobertura |
| Intermercado | retornos sincronizados, beta e correlação móvel |
| Implícita | nível/variação/percentil VIX e VXBR |
| Evento | tempo até evento, surpresa, revisão e reação |

Classificar regime somente com regras previamente definidas. Se os dados discordarem ou faltarem, apresentar dimensões separadas e declarar “misto” ou “insuficiente”.

## 6. Tradução para a análise do WIN

Contextualizar VWAP/TWAP, delta, volume e FVG à luz do regime:
- em expansão, exigir atenção a slippage e continuação;
- em baixa eficiência direcional, evitar extrapolar rompimentos sem confirmação;
- perto de evento, reconhecer risco de salto, spread e alteração de liquidez;
- em dados externos divergentes, não selecionar apenas a variável que confirma a hipótese.

Estas observações não são regras de trade. Gatilho, invalidação e risco continuam a exigir critérios próprios e dados do contrato negociado.

## 7. Cenários

Produzir:
- cenário base com evidências e condições;
- cenário alternativo com evidências contrárias;
- cenário de evento/volatilidade;
- não operação quando calendário, dados, liquidez ou risco tornarem a inferência frágil.

Não prever direção a partir de uma leitura isolada de VIX, IBOV ou surpresa macro.

## 8. Auditoria

Guardar snapshots das fontes e versões de consenso disponíveis no momento. Evitar usar consenso revisto ou dado corrigido que não estava disponível à hora da decisão (look-ahead). No backtest, usar dados point-in-time e calendário conhecido ex ante.

Reportar frequência, janela, universo, amostra, thresholds, período de treino/validação/teste e custos. Testar estabilidade em diferentes subperíodos e eventos.

## 9. Saída mínima

| Campo | Conteúdo |
|---|---|
| Timestamp e fuso | Mercado e receção |
| WIN | Contrato, vencimento, sessão |
| IBOV | Nível/retorno e timestamp |
| VIX | Cboe ou outro, fonte e timestamp |
| VXBR | Nível/retorno e timestamp |
| Macro | Evento, consenso, anterior, revisão, realizado |
| Surpresa | Valor, unidade e convenção |
| Volatilidade | Realizada e percentil |
| Regime | Rótulo e dimensões que o sustentam |
| Evidência contrária | Dados discordantes |
| Risco | Evento, liquidez, slippage |
| Limitações | Lacunas e dados não sincronizados |
