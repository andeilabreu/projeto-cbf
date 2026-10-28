# Relatório de bugs

## Situação atual

Quatro bugs foram registrados na sessão exploratória. Os achados anteriores
continuam em análise.

## Achados em análise

### ACH-001 — Rótulo de nascimento diferente do valor aceito

- **Tela:** Adicionar destaque · Atleta · Novo atleta.
- **Observado:** o campo se chama “Ano de nascimento”. Com `25/11/1974` o
  botão **Cadastrar** ficou desabilitado. Com `2010` o botão foi habilitado.
  Não houve mensagem clara no primeiro caso.
- **Status:** relacionado ao BUG-001.

### ACH-002 — Dois clubes com o mesmo nome TESTES

- **Tela:** Adicionar destaque · Atleta · Novo atleta.
- **Observado:** o campo Clube mostrou duas opções iguais, ambas `TESTES`.
- **Status:** em análise.

### ACH-003 — Data de nascimento incompatível com seleções de base

- **Tela:** Adicionar destaque · Atleta · Novo atleta.
- **Observado:** o sistema chegou a aceitar nascimento em 1974 no campo, mas
  manteve o botão desabilitado.
- **Status:** relacionado ao BUG-001.

### ACH-004 — Botão Adicionar destaque permanece em análise finalizada

- **Tela:** análise `TESTES × TESTES`.
- **Observado:** o status está **Finalizada**, mas o botão **Adicionar
  destaque** continua visível.
- **Status:** relacionado ao BUG-004. O ticket pede para não editar
  avaliação já concluída; neste teste o botão não deve ser usado.

## BUG-001 — Botão Cadastrar fica desabilitado sem mensagem

- **Origem:** encontrado na sessão exploratória, conforme relato de Andeil.
- **Tela:** Adicionar destaque · Atleta · Novo atleta.
- **Ambiente:** produção — https://cbf.lupafut.com/
- **Severidade:** Alta.
- **Prioridade:** Alta.
- **Evidência:** prints em `evidencias/tela-analise-finalizada.png` e
  `evidencias/tela-novo-atleta-botao-desabilitado.png`.
- **Status:** Aberto.

### Passos para reprodução

1. Abrir **Adicionar destaque** e escolher **Novo atleta**.
2. Preencher o nome e o clube.
3. Informar nascimento como data completa, por exemplo `25/11/1974`, ou
   deixar a posição natural vazia.
4. Observar o botão **Cadastrar**.

### Resultado esperado

O sistema deveria habilitar o botão quando os dados obrigatórios estivessem
válidos ou, se algo estiver inválido, mostrar uma mensagem clara.

### Resultado obtido

O botão permanece claro, como se estivesse desabilitado, sem mensagem. Com
ano `2010` e posição preenchida, o botão foi habilitado.

## BUG-002 — Cadastro de atleta falha com mensagem genérica

- **Origem:** encontrado na sessão exploratória.
- **Tela:** Adicionar destaque · Atleta · Novo atleta.
- **Ambiente:** produção — https://cbf.lupafut.com/
- **Severidade:** Alta.
- **Prioridade:** Alta.
- **Evidência:** relato de Andeil.
- **Status:** Aberto.

### Passos para reprodução

1. Em **Novo atleta**, informar ano `2010`.
2. Manter nome `TESTES` e clube `TESTES`.
3. Selecionar **Cadastrar**.

### Resultado esperado

O atleta deveria ser cadastrado ou o erro deveria explicar o motivo.

### Resultado obtido

O sistema exibiu: “Não foi possível cadastrar o atleta. Tente novamente.”

## BUG-003 — Atleta do destaque não aparece na busca de atletas

- **Origem:** encontrado na sessão exploratória.
- **Tela:** Buscar atleta, depois conferência na análise.
- **Ambiente:** produção — https://cbf.lupafut.com/
- **Severidade:** Alta — o nome existe no destaque da análise, mas a busca
  de atleta não o encontra.
- **Prioridade:** Alta.
- **Evidência:** relato de Andeil na busca; print
  `evidencias/tela-analise-finalizada-destaque-rascunho.png`.
- **Status:** Aberto.

### Passos para reprodução

1. Cadastrar um atleta novo com nome `[TESTE] Atleta Base 01` ao adicionar
   destaque.
2. Concluir o fluxo até o destaque aparecer na análise.
3. Procurar o mesmo nome em **Buscar atleta**.

### Resultado esperado

O atleta usado no destaque deveria aparecer na busca.

### Resultado obtido

A busca não encontrou `[TESTE] Atleta Base 01`. O mesmo nome aparece na
análise `TESTES × TESTES` como destaque em rascunho, posição Zagueiro,
clube TESTES.

## BUG-004 — Análise pode ser finalizada com destaque em rascunho

- **Origem:** encontrado na sessão exploratória.
- **Tela:** análise `TESTES × TESTES`.
- **Ambiente:** produção — https://cbf.lupafut.com/
- **Severidade:** Alta — a análise fica marcada como concluída sem avaliação
  preenchida.
- **Prioridade:** Alta.
- **Evidência:** print
  `evidencias/tela-analise-finalizada-destaque-rascunho.png`.
- **Status:** Aberto.
- **Nota:** a regra de negócio ainda não foi lida neste repositório. O
  resultado esperado abaixo é o comportamento razoável para um fluxo de
  análise, não uma regra confirmada no documento do produto.

### Passos para reprodução

1. Criar uma análise nova.
2. Adicionar um destaque sem preencher avaliações.
3. Finalizar a análise.

### Resultado esperado

O sistema deveria impedir a finalização, ou avisar que o destaque ainda está
em rascunho e sem avaliações.

### Resultado obtido

A análise `TESTES × TESTES` aparece como **Finalizada**. O destaque
`[TESTE] Atleta Base 01` permanece em **Rascunho**, com `0 avaliações`. O
botão **Adicionar destaque** continua visível.
