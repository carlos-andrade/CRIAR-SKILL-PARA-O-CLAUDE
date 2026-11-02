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
- [x] Delta, CVD, agressão e volume não classificado documentados.
- [x] Cobertura por volume e por negócios são métricas separadas.
- [x] Atividade versus deslocamento tem janela, unidade e limitações.
- [x] Absorção é hipótese com deteção, confirmação e invalidação separadas.
- [ ] Executar testes FL01–FL14 numa implementação de cálculo.
- [x] VIX Cboe e VXBR diferenciados por subjacente e metodologia.
- [x] IBOV versus WIN contextualizados com retornos sincronizados e basis.
- [x] Volatilidade implícita e realizada distinguidas.
- [x] Calendário macro inclui consenso, realizado, anterior, revisão e timezone.
- [x] Dados point-in-time e prevenção de look-ahead especificados.
- [x] Regimes exigem thresholds definidos no treino e avaliação fora da amostra.
- [ ] Executar testes MR01–MR18 com séries point-in-time.
- [ ] FVG tem regras de identificação e invalidação.
- [ ] Risco inclui custo, slippage e execução.
- [ ] Backtest inclui validação fora da amostra e vieses.
- [ ] Factos, inferências, hipóteses e desconhecidos são separados.

## Evidência documental — versão 0.4.0
- [x] Referência de regimes de mercado criada.
- [x] Workflow de contexto e regime criado.
- [x] Testes MR01–MR18 documentados.
- [x] Fontes institucionais B3, S&P DJI, Cboe, BCB e IBGE referenciadas.
- [x] Distinção VIX Cboe versus VXBR explicitada.
- [x] Fórmulas de surpresa, retorno, beta, basis e movimento aproximado de 30 dias documentadas.
- [ ] Execução automatizada das fixtures e testes.
- [ ] Execução dos prompts comportamentais em Claude.
- [ ] Teste de instalação real em Claude Code.
- [ ] Geração e validação do ZIP para claude.ai.
- [ ] Testes quantitativos com dados reais, custos e consensos point-in-time.

**Status:** módulo de contexto/regime especificado e documentado. Não há validação empírica de desempenho nem ligação a feed em tempo real.


## Motor de decisão — versão 0.5.0

- [x] Referência do motor de decisão criada.
- [x] Workflow de cenários operacionais criado.
- [x] Testes DE01–DE20 documentados.
- [x] Gates de dados e risco/execução especificados.
- [x] Dependências e prevenção de dupla contagem documentadas.
- [x] Cenários comprador, vendedor e não operar definidos.
- [ ] Executar DE01–DE20 em avaliação comportamental.
- [ ] Validar quantitativamente com dados point-in-time e custos.
- [ ] Testar instalação real em Claude Code e empacotamento para claude.ai.

**Status:** motor especificado e documentado. Sem validação empírica de desempenho, calibração, feed em tempo real ou execução real.
