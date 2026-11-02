# Workflow — análise intradiária do WIN

## Entrada mínima

Solicitar ou identificar dados de preço, timeframe, contrato/vencimento, timestamp/fuso, fonte e sessão. Para fluxo, requerer negócios e/ou livro com campos compatíveis. Para volume, identificar unidade.

## Procedimento

1. Validar o contrato e a sessão com `references/contrato-win.md`.
2. Auditar timestamps, ordenação, duplicados, lacunas, granularidade e latência.
3. Consultar calendário macro e eventos relevantes; distinguir consenso, realizado e revisão.
4. Mapear estrutura de preço e níveis observáveis.
5. Calcular VWAP e TWAP em janelas alinhadas; declarar convenções e gap.
6. Examinar delta, volume e atividade segundo `references/delta-volume.md`.
7. Avaliar spread/liquidez e qualidade da agressão, se disponíveis.
8. Verificar FVG apenas após confirmação dos candles e com regra de invalidação.
9. Confrontar IBOV e VIX como contexto, não como triggers.
10. Construir cenários condicionais, riscos, invalidação e caso de não operação.

## Saída

Apresentar dados utilizados, observações, interpretações, cenários e riscos. Não fornecer preço atual se não tiver feed atual. Não inventar gatilho nem stop com base em dados ausentes.
