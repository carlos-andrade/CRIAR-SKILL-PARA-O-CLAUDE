# Chat — Verificação das instruções do projeto e organização do histórico

- **Data:** 2026-11-02
- **Projeto:** CRIAR SKILL PARA O CLAUDE
- **Assunto:** Verificação das instruções do projeto ChatGPT e criação da estrutura de arquivo dos chats
- **Tipo de registo:** Registo cronológico da conversa, com síntese fiel das respostas. Não é uma transcrição literal integral.

---

## 1. Verificação da descrição do projeto

**Utilizador:** Pediu para verificar se o texto estava na descrição do projeto.

**ChatGPT:** Consultou inicialmente a descrição pública do repositório GitHub e encontrou a descrição institucional da Skill WIN. Concluiu que a descrição curta estava preenchida, mas que não era possível confirmar nela a presença do prompt completo de 7.999 caracteres.

## 2. Correção do local de verificação

**Utilizador:** Enviou uma captura de ecrã das «Configurações do projeto» e esclareceu que a verificação deveria ter sido feita naquele local.

**ChatGPT:** Reconheceu o equívoco. A captura mostrava o início do campo **Instruções**, com texto coincidente com o início do PROMPT-MESTRE. Foi ressalvado que a imagem não permitia verificar a totalidade do conteúdo nem confirmar a contagem integral de caracteres. Foi solicitado o texto completo para uma auditoria de integridade.

## 3. Regra de registo obrigatório das conversas

**Utilizador:** Determinou que todas as respostas dos chats relacionados com este projeto deveriam ser guardadas no repositório, num ficheiro de histórico.

**ChatGPT:** Formalizou a regra de registo cumulativo, organizado por data e assunto, preservando conteúdo técnico, decisões, alterações, conclusões e pendências. Também esclareceu que não poderia garantir gravação automática em segundo plano e que cada atualização deveria ser efetivamente executada e confirmada no GitHub.

## 4. Criação do histórico e correção da estrutura

**Utilizador:** Pediu a criação do ficheiro de histórico.

**ChatGPT:** Criou inicialmente `CHATS.md` na raiz do repositório e confirmou a gravação.

**Utilizador:** Questionou se o correto não seria uma pasta «CHAT'S».

**ChatGPT:** Concordou que uma pasta é mais adequada para organizar vários registos. Criou `CHATS/`, colocou nela `HISTORICO.md`, removeu o ficheiro `CHATS.md` da raiz e verificou a leitura do novo ficheiro no GitHub.

### Estrutura resultante nessa etapa

```text
CRIAR-SKILL-PARA-O-CLAUDE/
└── CHATS/
    └── HISTORICO.md
```

Foi adotado o nome técnico `CHATS` sem apóstrofo, por simplicidade e compatibilidade com ferramentas e sistemas de ficheiros.

## 5. Arquivamento desta conversa

**Utilizador:** Solicitou que esta conversa fosse guardada na pasta de chats com o respetivo nome.

**Decisão de arquivamento:** Criar este documento com o nome:

`2026-11-02-verificacao-instrucoes-e-organizacao-historico.md`

O índice `CHATS/HISTORICO.md` deve ser atualizado para apontar para este registo.

---

## Decisões consolidadas

1. A localização correta para verificar as instruções do projeto é o campo **Instruções** nas configurações do projeto ChatGPT, não a descrição pública do repositório.
2. A pasta de arquivo dos chats no GitHub é `CHATS/`.
3. Cada conversa deve ter um ficheiro próprio, com data e assunto no nome.
4. `CHATS/HISTORICO.md` funciona como índice geral e registo cumulativo.
5. Não sobrescrever registos anteriores; acrescentar novos documentos e atualizar o índice.
6. Só comunicar que um registo foi salvo depois de confirmar a sua existência e conteúdo no GitHub.

## Limitações deste registo

Este documento cobre a conversa atual e as decisões nela tomadas. Não inclui o texto integral do PROMPT-MESTRE de 7.999 caracteres nem recupera automaticamente conversas anteriores que não estejam presentes no contexto desta sessão.

---
