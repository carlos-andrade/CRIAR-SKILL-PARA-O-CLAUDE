# Testes — contexto macro e regime de mercado

Estes casos são especificações. A execução real exige fixtures point-in-time, timestamps e séries de mercado. Não declarar testes executados por estarem apenas descritos.

| ID | Entrada/cenário | Esperado | Proibido | Critério |
|---|---|---|---|---|
| MR01 | VIX Cboe sobe e WIN sobe | Explicar que VIX mede opções do S&P 500; investigar fator comum/horário | Dizer que VIX mede volatilidade do WIN | Instrumentos distinguidos |
| MR02 | VXBR sobe e IBOV sobe | Relatar coexistência possível entre retorno e volatilidade implícita | Tratar como impossibilidade ou erro | Sem causalidade automática |
| MR03 | Usuário diz “VIX brasileiro” sem ticker | Perguntar/identificar se é VXBR | Assumir VIX Cboe | Ambiguidade resolvida |
| MR04 | IBOV e WIN em timestamps diferentes | Sinalizar dessincronização e bloquear correlação imediata | Calcular relação sem ressalva | Timestamps alinhados |
| MR05 | WIN e IBOV divergem | Investigar basis, vencimento, carry, sessão e composição | Tratar IBOV como média móvel do WIN | Instrumentos diferenciados |
| MR06 | Surpresa de inflação positiva | Calcular realizado−consenso e contextualizar regime de política | Chamar automaticamente bullish/bearish | Sinal numérico não vira direção |
| MR07 | Consenso revisto após divulgação | Usar snapshot disponível antes do evento | Usar consenso revisto como se fosse conhecido ex ante | Sem look-ahead |
| MR08 | Evento sem consenso comparável | Reportar realizado e anterior/revisão, sem surpresa padronizada | Inventar consenso | Lacuna explícita |
| MR09 | Fuso da divulgação ausente | Consultar fonte/solicitar fuso; não inferir silenciosamente | Assumir horário local do utilizador | Fuso explícito |
| MR10 | VIX=20 | Explicar escala anualizada e mercado subjacente | Converter para pontos WIN | Unidade preservada |
| MR11 | VXBR e VIX têm valores diferentes | Não comparar níveis como se fossem a mesma série | Concluir inconsistência | Universo e método distinguidos |
| MR12 | Volatilidade realizada acima do percentil 95 histórico | Descrever regime de volatilidade elevada para a janela definida | Garantir reversão/continuação | Baseline e amostra explícitos |
| MR13 | Correlação móvel muda de sinal | Relatar instabilidade por subperíodo | Tratar correlação como constante | Estabilidade testada |
| MR14 | Índices externos fora do horário do WIN | Usar último valor com stale flag ou excluir | Tratar cotação antiga como simultânea | Freshness explícita |
| MR15 | Calendário aponta evento iminente, mas hora efetiva não confirmada | Tratar como evento agendado e verificar fonte | Afirmar divulgação já ocorrida | Previsto versus realizado |
| MR16 | Regime classificado com thresholds definidos após ver o teste | Rejeitar como desenho contaminado | Apresentar performance fora da amostra | Threshold congelado |
| MR17 | IBOV em alta, VXBR em alta e WIN lateral | Mostrar dimensões discordantes e hipótese de risco/preço não confirmado | Forçar rótulo direcional | Regime misto aceite |
| MR18 | Falta série histórica para percentil | Reportar nível sem percentil | Inventar posição histórica | Ausência preservada |

## Fixtures aritméticas

1. Surpresa simples: realizado 4,8; consenso 4,5 → +0,3 unidade do indicador. O sinal económico depende do indicador e do contexto.
2. Retorno logarítmico: preço anterior 100 e atual 101 → ln(1,01) ≈ 0,0099503 (0,9950%).
3. Movimento aproximado 30 dias: volatilidade anualizada 20% → 0,20 × sqrt(30/365) ≈ 5,73% como desvio-padrão aproximado do índice subjacente, não do WIN.

## Critérios globais

- VIX Cboe e VXBR sempre identificados separadamente.
- IBOV não é substituto do WIN.
- Dados sincronizados e point-in-time.
- Consenso, realizado, anterior e revisão preservados.
- Surpresa não implica direção automática.
- Thresholds definidos no treino e congelados antes do teste.
- Sem feed ou calendário verificável, declarar a limitação.
- Não operar é resultado admissível.

## Estado

- MR01–MR18 especificados.
- Fixtures aritméticas documentadas; execução automatizada pendente.
- Testes com calendários e consensos históricos point-in-time pendentes.
- Validação comportamental no Claude pendente.
