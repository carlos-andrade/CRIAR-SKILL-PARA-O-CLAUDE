# Contrato futuro mini de Ibovespa (WIN)

## Identidade

WIN é o código de negociação do contrato futuro mini de Ibovespa. É derivativo listado; não é o índice à vista. O IBOV é o índice de referência do mercado acionário brasileiro; o WIN é um contrato futuro cujo preço incorpora condições de carregamento, expectativas e dinâmica própria do mercado futuro.

## Especificações publicadas pela B3

A página institucional consultada em 2026-11-02 apresenta:

| Campo | Especificação publicada |
|---|---|
| Objeto | Ibovespa |
| Código | WIN |
| Valor por ponto | R$ 0,20 por ponto por contrato |
| Cotação | Pontos de índice |
| Variação mínima (tick) | 5 pontos |
| Lote padrão | 1 contrato |
| Meses de vencimento | Meses pares |
| Vencimento | Quarta-feira mais próxima do dia 15 do mês de vencimento; se não houver sessão, próxima sessão |
| Liquidação | Financeira |

Fonte: [B3 — Futuro Mini de Ibovespa](https://www.b3.com.br/pt_br/produtos-e-servicos/negociacao/renda-variavel/futuro-mini-de-ibovespa.htm). Consulta: 2026-11-02.

**Atenção:** confirmar novamente a página, o manual e eventuais ofícios circulares antes de utilizar estes parâmetros em cálculo de risco ou execução. A B3 pode alterar características, calendário e horários. Custos, margem, limites e horários não são inferidos desta tabela.

## Conversão de pontos em reais

Para variação de preço em pontos:

Resultado antes de custos = variação_em_pontos × 0,20 R$ × quantidade_de_contratos.

Exemplo apenas ilustrativo: 100 pontos em 1 contrato correspondem a R$ 20,00 brutos, antes de custos e slippage. Um tick de 5 pontos equivale a R$ 1,00 por contrato, antes de custos.

A fórmula não substitui a confirmação do valor vigente nem inclui corretagem, emolumentos, impostos, ajustes ou custos de financiamento.

## Vencimento e rolagem

- Não confundir código do ativo com mês/ano de vencimento.
- Identificar o contrato negociado e a data efetiva da sessão.
- Série contínua é uma construção analítica; pode conter ajustes de rolagem e não representa um contrato executável.
- Na análise histórica, documentar método de rolagem: primeiro aviso/último dia, volume, interesse aberto, calendário ou regra fixa. Não misturar séries ajustadas e preços negociáveis sem explicação.
- Comparações através de rolagem exigem cuidado com gaps artificiais e continuidade estatística.

## Sessões e relógio

Não codificar horários de negociação neste arquivo como constantes permanentes. Consultar a grade oficial B3 vigente, feriados, sessões especiais, alterações temporárias e horário de verão de outras praças. Usar timestamps com fuso explícito (preferir identificador IANA, como `America/Sao_Paulo`) e distinguir hora de Brasília de UTC e hora local do utilizador.

## Dados mínimos para uma análise operacional

- ticker completo e vencimento;
- data e sessão;
- timestamp com fuso e origem;
- tipo de dado: candle, tick, negócio, livro ou agregado;
- unidade de preço e volume;
- regra de ajuste/rolagem;
- latência e política de correções;
- custos e especificações da corretora, se a análise depender deles.

## Fontes

- B3, página de produto: https://www.b3.com.br/pt_br/produtos-e-servicos/negociacao/renda-variavel/futuro-mini-de-ibovespa.htm
- B3, especificação contratual PDF: https://www.b3.com.br/lumis/portal/file/fileDownload.jsp?fileId=8A828D2951C9C377015221CF257F5253

Documento operacional deve ser reconfirmado em fonte institucional antes de uso.
