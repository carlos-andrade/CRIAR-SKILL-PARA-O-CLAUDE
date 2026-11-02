# Gestão de risco e execução

## Risco por operação

Definir capital de risco disponível, perda máxima por operação, limite diário, limite semanal, exposição correlacionada e risco de ruína tolerado. Não presumir que saldo total da conta equivale a capital que pode ser arriscado.

Para stop de D pontos, multiplicador M R$/ponto/contrato, N contratos:

Risco bruto estimado = D × M × N.

Adicionar custos, slippage e risco de execução. O valor de M precisa ser confirmado na especificação vigente do contrato.

Dimensionamento teórico:

N = floor(orçamento_de_risco / (distância_stop × multiplicador + custos_estimados_por_contrato)).

Se parâmetros estiverem ausentes, não sugerir quantidade numérica. Aplicar limites adicionais de margem, liquidez e concentração.

## Execução

Considerar:
- spread e profundidade disponível;
- slippage em condições normais e de stress;
- ordens limitadas, a mercado e execução parcial;
- latência e rejeição/cancelamento;
- leilões, gaps, interrupções e falhas de conexão;
- custos de bolsa, corretora, impostos e financiamento aplicáveis;
- diferenças entre preço teórico, preço de sinal e preço efetivo.

Stop não garante execução ao preço definido em mercado rápido.

## Limites e não operação

Não operar quando dados forem inválidos, feed estiver atrasado, spread/liquidez forem inadequados, evento iminente aumentar risco não modelado, limite diário tiver sido atingido ou a tese não tiver gatilho/invalidação objetivos.

Toda sugestão deve ser condicional, nunca uma ordem de execução. A decisão final e a execução pertencem ao utilizador.
