# Relatório de bugs

## Situação atual

Um bug foi registrado a partir do relato de Andeil na tela de cadastro de
atleta. Os achados anteriores continuam em análise.

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
- **Observado:** o sistema aceitou nascimento em 1974 para um contexto de
  seleções de base.
- **Status:** em análise. Depende da regra de negócio, ainda não lida.

## Estrutura

Cada bug deverá informar:

- identificador;
- título;
- tela ou fluxo;
- ambiente;
- pré-condição;
- passos para reprodução;
- resultado esperado;
- resultado obtido;
- severidade;
- prioridade;
- evidência;
- status.

## BUG-001 — Botão Cadastrar não conclui o cadastro do atleta

- **Origem:** encontrado na sessão exploratória, conforme relato de Andeil.
- **Tela:** Adicionar destaque · Atleta · Novo atleta.
- **Ambiente:** produção — https://cbf.lupafut.com/
- **Pré-condição:** análise de teste `TESTES × TESTES` em andamento; formulário
  de novo atleta preenchido com nome `TESTES`, nascimento `25/11/1974`, perna
  direita, posição Goleiro e clube `TESTES`.
- **Severidade:** Alta — impede criar atleta novo pelo fluxo permitido do
  ticket.
- **Prioridade:** Alta.
- **Evidência:** print em `evidencias/tela-analise-finalizada.png`.
- **Status:** Aberto — parcialmente reproduzido.

## BUG-002 — Cadastro de atleta falha com mensagem genérica

- **Origem:** encontrado na sessão exploratória, após o ajuste do ano de
  nascimento para `2010`.
- **Tela:** Adicionar destaque · Atleta · Novo atleta.
- **Ambiente:** produção — https://cbf.lupafut.com/
- **Pré-condição:** formulário de novo atleta com nome `TESTES`, nascimento
  `2010`, perna direita, posição Goleiro e clube `TESTES`.
- **Severidade:** Alta — o fluxo permitido de criar atleta do zero não
  conclui.
- **Prioridade:** Alta.
- **Evidência:** relato de Andeil na sessão; print anterior do formulário.
- **Status:** Aberto.

### Passos para reprodução

1. Em **Novo atleta**, informar um ano de nascimento com quatro dígitos, por
   exemplo `2010`.
2. Manter nome `TESTES` e clube `TESTES`.
3. Selecionar **Cadastrar**.

### Resultado esperado

O atleta de teste deveria ser cadastrado.

### Resultado obtido

Com o nome `TESTES`, o sistema exibiu “Não foi possível cadastrar o atleta.
Tente novamente.”

Com o nome `[TESTE] Atleta Base 01` e ano `2010`, o cadastro passou. Isso
sugere falha ou bloqueio relacionado ao nome `TESTES`, possivelmente por
duplicidade, sem mensagem clara.

### Passos para reprodução

1. Em uma análise em andamento, selecionar **Adicionar destaque**.
2. Escolher **Novo atleta**.
3. Preencher os campos do formulário.
4. Selecionar o botão **Cadastrar**.

### Resultado esperado

O atleta de teste deveria ser cadastrado e o fluxo do destaque deveria
continuar.

### Resultado obtido

Com a data `25/11/1974`, o botão permaneceu claro, como se estivesse
desabilitado, sem mensagem de erro.

Quando o campo foi alterado para `2010`, o botão foi habilitado. Ao clicar,
o sistema exibiu: “Não foi possível cadastrar o atleta. Tente novamente.”
