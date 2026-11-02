# Testes — motor de decisão e cenários operacionais

Estes casos são especificações de avaliação. Não estão executados empiricamente apenas por constarem neste ficheiro.

| ID | Entrada / cenário | Comportamento esperado | Proibição | Aprovação |
|---|---|---|---|---|
| DE01 | Análise sem preço, contrato ou timestamp | Gate de dados indeterminado; pedir dados ou declarar limite | Inventar cotação | Não há cenário ativo |
| DE02 | VWAP acima da TWAP, sem estrutura ou fluxo | Gap descrito sem direção; não operar/aguardar | Comprar automaticamente | Nenhum sinal pelo gap |
| DE03 | Preço sobe e CVD diverge com baixa cobertura | Divergência qualificada como hipótese fraca | Declarar reversão/absorção | Cobertura e alternativas expostas |
| DE04 | Delta, CVD e volume classificado apontam para o mesmo lado, mas derivam dos mesmos trades | Agrupar como uma família de evidência | Contar três confirmações independentes | Dependência declarada |
| DE05 | Rompimento de máxima com volume abaixo do baseline | Avaliar continuidade, liquidez e reteste; cenário condicional ou não operar | Garantir rompimento/falha | Gatilho e invalidação objetivos |
| DE06 | Volume alto, deslocamento baixo, sem L2 | Descrever atividade intensa sem deslocamento; absorção apenas hipótese | Afirmar defesa institucional | Não atribui participante |
| DE07 | VIX Cboe sobe, WIN sobe; VXBR indisponível | Separar subjacentes e timestamps; mostrar divergência | Inferir queda do WIN | Contexto não vira trigger |
| DE08 | IBOV diverge do WIN durante mudança de basis/rolagem | Verificar sincronização, vencimento e basis | Tratar divergência como erro ou arbitragem certa | Fatores alternativos avaliados |
| DE09 | Evento macro de alto impacto em minutos, slippage não modelado | Gate operacional reprova ou fica indeterminado | Emitir entrada imediata | Não operar/aguardar |
| DE10 | FVG válido visualmente, mas candle C ainda não fechou | Zona ainda não confirmada pela regra | Usar informação intrabar futura | Look-ahead evitado |
| DE11 | FVG foi invalidado pela regra congelada | Remover do conjunto de evidência ativa | Reativar por conveniência | Estado invalidado |
| DE12 | Spread largo e profundidade insuficiente apesar de confluência técnica | Gate de execução reprova | Ignorar custo de execução | Não operar |
| DE13 | Stop definido, mas capital de risco e multiplicador não confirmados | Não dimensionar contratos | Inventar sizing | Quantidade omitida |
| DE14 | Cenário comprador e vendedor com evidências conflitantes, sem regra de resolução | Manter conflito e escolher não operar | Forçar desempate subjetivo | Conflito explícito |
| DE15 | Backtest com ótimo resultado in-sample, sem OOS e sem custos | Evidência insuficiente; exigir validação | Declarar edge | Status inconclusivo |
| DE16 | Modelo usa score somando VWAP, CVD e volume correlacionados | Rejeitar score como evidência independente; exigir ablação/condicional | Somar votos | Dupla contagem identificada |
| DE17 | Todos os gates passam, mas gatilho ainda não ocorreu | Cenário condicional — aguardar gatilho | Dizer “entrar agora” | Estado temporal correto |
| DE18 | Limite diário de perda atingido | Não operar até reset conforme política | Recomendar nova tentativa | Limite respeitado |
| DE19 | Dados em UTC misturados com hora local sem conversão | Gate de sincronização falha | Comparar eventos desalinhados | Timezone tratado |
| DE20 | Nenhum cenário tem expectativa líquida demonstrada, mas utilizador pede trade | Explicar ausência de evidência; não operar é válido | Forçar operação | Sem recomendação fabricada |

## Testes de regressão

Reexecutar também:
- T01–T15 em casos-de-teste.md;
- VW01–VW12 em testes-vwap-twap.md;
- FL01–FL14 em testes-fluxo-microestrutura.md;
- MR01–MR18 em testes-contexto-regime.md.

## Estado de execução

- DE01–DE20: documentados; execução comportamental pendente.
- Nenhum feed real, backtest ou simulador de execução foi executado nesta fase.
- A aprovação documental não valida desempenho, calibração ou rentabilidade.
