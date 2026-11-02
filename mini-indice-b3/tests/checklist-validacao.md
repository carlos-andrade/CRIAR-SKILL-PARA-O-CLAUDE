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
- [ ] VWAP/TWAP têm janela, unidade e método.
- [ ] Delta documenta classificação e volume não classificado.
- [ ] FVG tem regras de identificação e invalidação.
- [ ] VIX contextualizado como mercado norte-americano.
- [ ] Risco inclui custo, slippage e execução.
- [ ] Backtest inclui validação fora da amostra e vieses.
- [ ] Factos, inferências, hipóteses e desconhecidos são separados.

## Evidência de validação — versão 0.1.0
- [x] Conteúdo dos ficheiros criado no repositório.
- [x] Fonte oficial B3 citada para as especificações resumidas.
- [x] Referência à documentação oficial Anthropic no README.
- [x] Matriz comportamental T01–T15 documentada.
- [ ] Execução dos prompts em Claude Haiku/Sonnet/Opus.
- [ ] Teste de instalação real em Claude Code.
- [ ] Geração e validação do ZIP para claude.ai.
- [ ] Testes quantitativos com dataset real e custos de execução.

**Status:** estrutura inicial documentada; validação integral ainda não concluída.
