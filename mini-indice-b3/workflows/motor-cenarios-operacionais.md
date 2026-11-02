# Workflow — motor de decisão e cenários operacionais

## Objetivo

Produzir uma leitura condicional e auditável do WIN: cenário comprador, vendedor e/ou não operar. O workflow não emite ordens e não força uma direção.

## Entradas necessárias

- Contrato/vencimento, sessão, timeframe, fonte, timestamp e timezone.
- Série de preços e estrutura observável.
- VWAP/TWAP com janela, método e volume definidos.
- Negócios/fluxo: agressor, quantidade, timestamps e política de não classificados; livro L2 se disponível.
- Volume por unidade e baseline comparável.
- Estado de FVG, se aplicável, com candles de origem e regra de invalidação.
- Contexto macro/intermercado com fonte, consenso point-in-time e timestamps.
- Parâmetros de risco: capital de risco, limite por operação/dia, multiplicador vigente, custos, stop e condições de execução.

Dados não fornecidos devem ser marcados como ausentes; não preencher por inferência.

## Procedimento

### Etapa 1 — Gate de dados

Validar instrumento, vencimento, sessão, timezone, ordenação, duplicados, lacunas, granularidade, latência, sincronização e cobertura. Identificar aproximações e dados não classificados.

**Falha:** parar a análise direcional. Resultado: dados insuficientes / não operar até corrigir.

### Etapa 2 — Gate operacional e de risco

Verificar calendário/eventos, estado da plataforma, spread, profundidade, slippage, custos, limites de perda e possibilidade de dimensionar a posição. Confirmar multiplicador e tick na fonte oficial vigente.

**Falha:** não operar; explicar o gate que falhou.

### Etapa 3 — Regime e contexto

Classificar dimensões separadamente. Não forçar rótulo único quando houver divergência. Comparar IBOV e WIN por retornos sincronizados; distinguir VIX Cboe de VXBR. Contexto macro não determina direção automática.

### Etapa 4 — Hipóteses direcionais

Definir separadamente hipótese compradora e vendedora a partir de estrutura de preço e níveis observáveis. A hipótese precisa de:
- condição de ativação;
- janela/timeframe;
- condição de invalidação;
- evidência que a contradiz.

Não derivar hipótese apenas do sinal do gap VWAP–TWAP, delta, VIX, IBOV ou FVG.

### Etapa 5 — Evidências condicionais

Para cada hipótese, preencher matriz favorável/contrária/qualidade:
- preço/estrutura;
- regime;
- VWAP/TWAP;
- fluxo e cobertura;
- atividade, volume e liquidez;
- FVG;
- macro/intermercado.

Agrupar variáveis que usam os mesmos dados. Explicitar dependências e impedir dupla contagem. Ausência de dado não equivale a confirmação neutra.

### Etapa 6 — Construção dos cenários

Apresentar:
1. **Comprador:** apenas se critérios mínimos forem satisfeitos; se faltar gatilho, “condicional — aguardar”.
2. **Vendedor:** critérios equivalentes, avaliados independentemente.
3. **Não operar:** gates falhados, conflito material, evidência insuficiente ou execução inadequada.

Os cenários podem coexistir como alternativas condicionais, mas não podem ser apresentados como simultaneamente executáveis. Definir qual evento ativa cada um e qual cancela os restantes.

### Etapa 7 — Plano e dimensão

Só quantificar entrada, stop, objetivo ou contratos quando preços, multiplicador, capital de risco, custos e execução forem conhecidos. Estimar risco incluindo slippage e custos. Não assumir que stop garante preço de execução.

### Etapa 8 — Conclusão auditável

Reportar:
- decisão atual: comprador condicional / vendedor condicional / não operar;
- factos e cálculos;
- evidências favoráveis e contrárias;
- dependências entre variáveis;
- gatilho e invalidação;
- risco e execução;
- dados ausentes e condição que mudaria a decisão.

## Modelo de saída

### Estado dos gates
- Dados: aprovado/reprovado/indeterminado — evidência.
- Risco/execução: aprovado/reprovado/indeterminado — evidência.

### Contexto
Regime por dimensão, eventos e alinhamento temporal.

### Cenários
| Cenário | Gatilho | Evidência favorável | Contradições | Invalidação |
|---|---|---|---|---|
| Comprador | condição observável | factos/cálculos | riscos | condição objetiva |
| Vendedor | condição observável | factos/cálculos | riscos | condição objetiva |
| Não operar | gate/condição | motivo | o que falta | condição para reavaliar |

### Plano de risco
Parâmetros confirmados, risco bruto/líquido estimado, custos, slippage e limites. Se não quantificável, declarar porquê.

### Classificação epistemológica
Separar factos, cálculos, inferências, hipóteses e desconhecidos.

## Restrições

- Não produzir sinal baseado em score ou soma de indicadores.
- Não tratar indicadores correlacionados como confirmações independentes.
- Não chamar intenção institucional a padrões agregados.
- Não inventar feed, preço, evento, consenso, multiplicador, stop ou quantidade.
- Não usar informação futura para confirmar gatilhos passados.
- Não declarar vantagem estatística sem validação fora da amostra e custos.
