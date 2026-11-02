# Testes específicos — VWAP, TWAP e gap

Os casos abaixo validam regras e cálculos. São fixtures sintéticas, não dados de mercado. Os testes ainda precisam de execução num ambiente de código/Claude para serem considerados executados.

| ID | Entrada | Resultado esperado | Falha proibida |
|---|---|---|---|
| VW01 | Trades: (100000,10), (100010,20), (100005,10) | VWAP = 100006,25; volume = 40 contratos | Ponderar pela contagem de trades |
| VW02 | Quantidade total igual a zero | VWAP indefinida e erro/estado explícito | Retornar zero |
| VW03 | Intervalos TWAP: 100000 por 120s; 100010 por 60s; 100005 por 60s | TWAP = 100003,75 | Média simples dos três preços |
| VW04 | Gap calculado a partir de VW01 e VW03 | Gap = +2,50 pontos | Chamar gap de sinal de compra |
| VW05 | Amostras em intervalos temporais irregulares | Ponderar pela duração real | Média simples das observações |
| VW06 | Intervalo sem negócio | Aplicar política explícita e reportar cobertura/staleness | Preencher com zero ou ocultar lacuna |
| VW07 | VWAP da sessão inteira e TWAP de 30 minutos | Comparação bloqueada ou marcada como não comparável | Apresentar gap como válido |
| VW08 | Timestamp sem timezone | Bloquear interpretação temporal até resolver | Assumir UTC ou hora local |
| VW09 | Candle volumeado com preço típico | Identificar VWAP como aproximação por candles | Alegar equivalência a VWAP por trades |
| VW10 | Preço atual e referências com timestamps diferentes | Sinalizar desalinhamento | Calcular distância sem ressalva |
| VW11 | Outlier de preço | Investigar origem e classificar antes de excluir | Remover automaticamente |
| VW12 | Pequena alteração da amostragem TWAP altera sinal do gap | Reportar sensibilidade e robustez baixa | Ocultar dependência metodológica |

## Fixtures numéricas de referência

### VWAP

- Preços: 100000, 100010, 100005 pontos.
- Quantidades: 10, 20, 10 contratos.
- Soma ponderada: 3.000.250 pontos-contrato.
- Quantidade total: 40 contratos.
- Resultado: 100006,25 pontos.

### TWAP

- Preços representativos: 100000, 100010, 100005 pontos.
- Durações: 120, 60, 60 segundos.
- Soma ponderada: 24.000.900 pontos-segundo.
- Duração total: 240 segundos.
- Resultado: 100003,75 pontos.

### Gap

- VWAP − TWAP = 100006,25 − 100003,75.
- Resultado: +2,50 pontos.

## Critério de aceitação

- Todos os resultados numéricos coincidem com as fixtures, com tolerância de arredondamento explicitada.
- Unidade, janela, fonte e método são reportados.
- Não há divisão por zero, preenchimento silencioso de lacunas ou comparação de janelas desalinhadas.
- O sinal do gap nunca é apresentado isoladamente como previsão ou entrada.
