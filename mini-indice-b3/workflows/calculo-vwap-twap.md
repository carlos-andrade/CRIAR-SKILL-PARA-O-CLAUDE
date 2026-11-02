# Workflow — cálculo reproduzível de VWAP, TWAP e gap

## Objetivo

Produzir VWAP, TWAP, gap, distância, inclinação e dispersão com parâmetros auditáveis. Seguir `references/vwap-twap-especificacao-matematica.md`.

## Pré-condições

1. Confirmar ticker completo, vencimento e sessão.
2. Confirmar timezone de origem; converter para uma base temporal consistente sem descartar o timestamp original.
3. Delimitar janela [t0,t1), com início inclusivo e fim exclusivo, ou declarar outra convenção.
4. Definir preço e volume para VWAP.
5. Definir preço representativo e política de intervalos sem negócio para TWAP.
6. Confirmar que as duas métricas usam o mesmo instrumento e janela.
7. Verificar integridade e cobertura.

## Procedimento

1. Ordenar dados por timestamp e identificador de negócio, quando disponível.
2. Validar duplicados, lacunas, correções, valores ausentes e unidades.
3. Calcular VWAP por negócios com quantidade executada como ponderador. Se só houver candles, identificar o resultado como aproximação.
4. Construir intervalos temporais não sobrepostos para TWAP. Calcular Δt real, não assumir espaçamento uniforme sem validação.
5. Aplicar a política declarada para períodos sem negócio e medir cobertura/staleness.
6. Calcular Gap = VWAP − TWAP.
7. Calcular D_vwap e D_twap com referência de preço e timestamp explícitos.
8. Calcular inclinação em janela definida e dispersão ponderada, se houver dados suficientes.
9. Repetir com frequência de amostragem alternativa e, se pertinente, preço representativo alternativo.
10. Comparar sensibilidade. Se a conclusão mudar materialmente com pequenas alterações metodológicas, declarar baixa robustez.
11. Guardar parâmetros, versão do algoritmo, contagens e resultados para reprodução.

## Esquema mínimo de saída

- instrumento, vencimento, sessão;
- janela e timezone;
- fonte, granularidade e timestamp de atualização;
- método VWAP e unidade do volume;
- método TWAP, preço e política de intervalos sem negócio;
- cobertura temporal e duração sem observação;
- VWAP, TWAP e gap em pontos;
- preço de referência, D_vwap e D_twap;
- inclinação e unidade;
- dispersão e método;
- quantidade de negócios, contratos e observações;
- limitações e resultado do teste de sensibilidade.

## Regras de bloqueio

Não apresentar número como válido quando denominador for zero, janela estiver desalinhada, timestamps não puderem ser interpretados ou integridade estiver comprometida. Não substituir dados ausentes por zeros. Não converter o sinal do gap em ordem ou recomendação automática.
