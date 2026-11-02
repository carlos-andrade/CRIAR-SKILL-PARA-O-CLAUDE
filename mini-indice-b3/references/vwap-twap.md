# VWAP, TWAP e gap VWAP–TWAP

## Referência normativa interna

As convenções detalhadas, exemplos numéricos, validações e regras de sensibilidade estão em `vwap-twap-especificacao-matematica.md`. Este ficheiro resume os conceitos. Em caso de divergência, rever ambos e manter uma única convenção explícita no cálculo.

## VWAP

Para negócios i com preço p_i e volume/quantidade q_i numa janela definida:

VWAP = Σ(p_i × q_i) / Σq_i.

Definir se q_i representa contratos, lotes ou volume financeiro; manter unidade coerente. Em candles, aproximações (por exemplo, preço típico × volume) não equivalem à VWAP calculada com todos os negócios.

Especificar:
- janela e âncora (sessão, dia, semana, evento);
- instante de reinício;
- fonte e definição de volume;
- tratamento de leilões, negócios especiais e correções;
- granularidade e dados ausentes.

A inclinação pode ser calculada como variação da VWAP por unidade de tempo ou regressão numa janela. Distância preço–VWAP pode ser expressa em pontos, ticks ou unidades de volatilidade; declarar a normalização.

## TWAP

Para observações de preço p_j amostradas em tempos t_j, TWAP simples é média temporal dos preços. Para intervalos irregulares, uma média ponderada pelo tempo é mais apropriada:

TWAP = Σ(p_j × Δt_j) / ΣΔt_j.

Explicitar preço usado (mid, último, close ou outro), frequência de amostragem, tratamento de intervalos sem negócio e janela. Amostragem regular de último negócio pode distorcer períodos sem execução.

## Gap

Gap = VWAP − TWAP (ou sinal invertido, desde que declarado).

Relatar também gap em pontos/ticks e, quando útil, normalização por volatilidade. O sinal indica apenas diferença entre duas estimativas dependentes das suas definições. Não implica, por si só, direção futura, desequilíbrio institucional, manipulação ou ponto de entrada.

Interpretação depende de:
- composição do volume e distribuição temporal dos negócios;
- janela comum e sincronização;
- tendência e volatilidade;
- períodos sem negócio e qualidade dos dados;
- comportamento do preço em torno das referências.

## Verificações

1. Usar janelas alinhadas.
2. Confirmar denominador positivo.
3. Verificar timestamps ordenados e sem duplicações.
4. Avaliar sensibilidade à frequência de amostragem do TWAP.
5. Comparar estimativa por trades com aproximação por candles.
6. Não comparar VWAP intradiária com TWAP de janela diferente sem avisar.

## Exemplo ilustrativo

VWAP de 128.450 e TWAP de 128.430 produzem gap de +20 pontos. Isso significa somente que a VWAP calculada é 20 pontos superior à TWAP para as definições usadas. Sem contexto e evidência adicional, não se conclui que o mercado deva subir ou cair.
