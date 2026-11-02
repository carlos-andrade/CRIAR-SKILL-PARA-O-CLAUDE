# Checklist de validação e aceitação

## Formato
- [ ] Frontmatter YAML válido.
- [ ] `name` dentro das regras de caracteres e comprimento.
- [ ] `description` não vazia e com intenção de acionamento clara.
- [ ] `SKILL.md` abaixo de 500 linhas.
- [ ] Pasta da Skill coincide com o nome técnico adotado.

## Estrutura
- [ ] Todos os links relativos existem.
- [ ] Sem referências circulares.
- [ ] Cada referência tem finalidade distinta.
- [ ] README explica instalação e limitações.

## Conteúdo
- [ ] WIN e IBOV são diferenciados.
- [ ] Preço, pontos, tick, contratos, negócios e volume financeiro não se confundem.
- [x] VWAP/TWAP têm janela, unidade e método documentados.
- [x] Gap, dispersão, inclinação, dados ausentes e sensibilidade metodológica especificados.
- [x] Workflow e fixtures matemáticas VWAP/TWAP documentados.
- [ ] Executar testes VW01–VW12 em implementação de cálculo.
- [x] Delta documenta classificação e volume não classificado.
- [x] CVD e imbalance normalizado têm fórmulas e reset definidos.
- [x] Cobertura por volume e por negócios são métricas separadas.
- [x] Atividade versus deslocamento tem janela, unidade e limitações.
- [x] Absorção é hipótese com deteção, confirmação e invalidação separadas.
- [x] Ritmo de negócios e contratos não são confundidos.
- [ ] Executar testes FL01–FL14 numa implementação de cálculo.
- [ ] FVG tem regras de identificação e invalidação.
- [ ] VIX contextualizado como mercado norte-americano.
- [ ] Risco inclui custo, slippage e execução.
- [ ] Backtest inclui validação fora da amostra e vieses.
- [ ] Factos, inferências, hipóteses e desconhecidos são separados.

## Evidência de validação — versão 0.3.0
- [x] Referências de microestrutura e delta atualizadas no repositório.
- [x] Workflow de análise de fluxo criado.
- [x] Matriz FL01–FL14 documentada.
- [x] Aritmética das fixtures FL01, FL03 e FL04 verificável por cálculo direto.
- [ ] Execução automatizada dos testes de cálculo.
- [ ] Execução dos prompts comportamentais em Claude Haiku/Sonnet/Opus.
- [ ] Teste de instalação real em Claude Code.
- [ ] Geração e validação do ZIP para claude.ai.
- [ ] Testes quantitativos com dataset real de trades/quotes/L2 e custos.

**Status:** documentação e especificação de fluxo ampliadas. A aritmética de referência foi verificada; execução automatizada, validação comportamental, instalação e pesquisa com dados reais permanecem pendentes.
