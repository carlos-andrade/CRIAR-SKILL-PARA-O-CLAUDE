# FVG e conceitos ICT

## Regra objetiva de FVG de três candles

Considere candles consecutivos A, B e C, na mesma escala temporal:

- **Bullish FVG:** mínima de C > máxima de A. Zona: [máxima de A, mínima de C].
- **Bearish FVG:** máxima de C < mínima de A. Zona: [máxima de C, mínima de A].

O candle B é o candle de deslocamento no modelo clássico de três candles, mas a existência da zona não demonstra causa institucional nem intenção de um participante específico.

## Metadados obrigatórios

Guardar símbolo/contrato, timeframe, horário, extremos da zona, direção, tamanho em pontos/ticks, candles de origem, regra de sessão, contexto e fonte dos dados.

## Estados operacionais

Uma implementação deve definir objetivamente:
- identificado;
- não mitigado;
- parcialmente mitigado;
- totalmente preenchido (conforme regra escolhida);
- invalidado;
- expirado por regra temporal.

Não misturar “mitigação” e “preenchimento total”. Regras de toque, entrada na zona, midpoint e fechamento além da zona são alternativas metodológicas; escolher uma antes do teste.

## Contexto e limitações

Avaliar estrutura, deslocamento, volatilidade, liquidez e localização relativa a níveis observáveis. FVG não é entrada automática, não garante suporte/resistência e não prova presença de ordem institucional.

Evitar repaint/look-ahead: uma zona só pode ser reconhecida depois de o candle C estar fechado, se a regra depender do seu extremo final. Para backtest intrabar, modelar sequência e execução disponíveis; não assumir toque e fill sem dados compatíveis.
