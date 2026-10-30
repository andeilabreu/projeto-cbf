# Sessão 01 — Teste exploratório

## Identificação

- **QA:** Andeil Abreu
- **Ambiente:** produção — https://cbf.lupafut.com/
- **Data:** 22 e 28 de outubro de 2026
- **Duração:** em andamento
- **Status:** em andamento — análise de teste finalizada com destaque em rascunho

## Preparação

- [x] Credenciais do ticket disponíveis fora deste repositório.
- [ ] Documentação de regras de negócio acessível.
- [x] Prefixos `[TESTE]` definidos.
- [x] Confirmação de que nenhum dado existente será editado.

## Anotações da sessão

### 1. Acesso à tela de login

- **Ação:** abrir https://cbf.lupafut.com/
- **Resultado obtido:** a plataforma redireciona para a tela de Login.
- **Observado:**
  - o título da página é `CBF`;
  - existem os campos **E-mail** e **Senha**;
  - existe o botão **Entrar**;
  - o idioma da página é `pt-BR`;
  - a conexão usa HTTPS;
  - o formulário marca o campo de senha como tipo senha;
  - a API usada pela interface é `https://api.lupafut.com`.

### 2. Estrutura aparente do sistema

Antes do login, a interface já revela estas áreas futuras:

- `/login`
- `/paineis`
- `/observacoes` e `/observacoes/nova`
- `/atletas`
- `/analises`
- `/gestao`, `/gestao/observacoes`, `/gestao/partidas`, `/gestao/relatorio`,
  `/gestao/duplicatas`, `/gestao/diagrama-tatico`
- `/config` e `/config/usuarios`
- `/conta`

### 3. Autenticação com as credenciais do ticket

- **Ação:** enviar e-mail e senha do ticket para o serviço de login.
- **Resultado obtido:** o acesso foi aceito.
- **Observado:** o perfil autenticado possui papel de **admin**.
- **Risco:** com perfil de administrador, a tela de usuários e outros cadastros
  existentes podem ficar disponíveis. O ticket proíbe editar usuários,
  avaliações concluídas, clubes e jogadores já cadastrados. A sessão deve
  permanecer em modo de observação até haver um dado novo criado com o
  prefixo `[TESTE]`.

### 4. Tela inicial após o login no navegador

- **Ação:** entrar com as credenciais do ticket e observar os menus, sem
  editar registros existentes.
- **Resultado obtido:** a tela inicial apresentou os menus informados por
  Andeil:
  - Observar
  - Painéis
  - Perfil
  - Gestão
  - Configurações
- **Observado:** os nomes batem com áreas previstas na interface, com
  pequenas diferenças de escrita. Não houve clique em edição nesta etapa.

### 5. Menu Observar

- **Ação:** abrir o menu **Observar**.
- **Resultado obtido:** Andeil informou a opção **Iniciar nova análise**.
- **Observado:** essa ação parece criar um registro novo, o que é permitido
  pelo ticket, desde que não use clube ou jogador já cadastrado e que o
  prefixo `[TESTE]` seja aplicado.

### 6. Início de uma nova análise

- **Ação:** Andeil preencheu os campos da nova análise com dados de teste e
  clicou em **Iniciar análise**.
- **Evidência:** print da tela, extraído de `TELA CBF.ods`.
- **Resultado obtido:** a análise foi criada com status **Em andamento**.
- **Observado na tela:**
  - título da aplicação: CBF Scouting;
  - menus: Observar, Gestão, Painéis, Configurações e Perfil;
  - partida: `TESTES × TESTES`;
  - data exibida: `TESTES · 31/10/2026`;
  - tipo: Assistida;
  - modo selecionado: **In loco**;
  - modo disponível e não selecionado: **Vídeo**;
  - botões: **Adicionar destaque**, **Editar partida** e **Finalizar análise**;
  - área Destaques: “Nenhum destaque ainda.”
- **Desvio do critério do ticket:** os nomes usam `TESTES`, e não o prefixo
  `[TESTE]`. O registro parece ter sido criado do zero, o que atende a outra
  regra do ticket. Nas próximas criações, o prefixo `[TESTE]` deve ser usado.

### 7. Destaque e finalização

- **Ação:** Andeil informou que adicionou um destaque e clicou em
  **Finalizar análise**.
- **Resultado obtido:** a confirmação visual da análise concluída não
  apareceu no print daquele momento. O print seguinte mostrou outra tela.
  A tela atual, descrita no item 11, confirma que a análise ficou
  **Finalizada**.

### 8. Tela Novo atleta ao adicionar destaque

- **Evidência:** print extraído de `TELA CBF 2.ods`.
- **Título da tela:** Adicionar destaque · Atleta.
- **Aba selecionada:** Novo atleta. Também existe a aba **Buscar atleta**.
- **Campos visíveis:**
  - Nome: `TESTES`;
  - Ano de nascimento: `25/11/1974`;
  - Perna dominante: Direita;
  - Posição natural: Goleiro;
  - Clube: duas opções com o mesmo nome `TESTES`;
  - botão **Cadastrar**.
- **Observado:**
  - o cadastro parece ser de atleta novo, o que o ticket permite;
  - o prefixo `[TESTE]` não foi usado;
  - o rótulo diz “Ano de nascimento”, mas o valor informado é uma data
    completa;
  - existem dois clubes com o mesmo nome `TESTES`, o que dificulta saber qual
    está selecionado;
  - a data de nascimento `25/11/1974` geraria um atleta com cerca de 51 anos
    em 2026, o que merece conferência porque a plataforma é de seleções de
    base;
  - Andeil informou que o botão **Cadastrar** não funciona. Registrado como
    **BUG-001**.
- Confirmação: o botão permanece claro, como se estivesse desabilitado.
- Após trocar o nascimento para `2010`, o botão foi habilitado. O clique em
  **Cadastrar** exibiu: “Não foi possível cadastrar o atleta. Tente
  novamente.” Registrado como **BUG-002**.
- Depois o nome foi alterado para `[TESTE] Atleta Base 01` e o fluxo avançou
  para a tela de posição.
- Na busca de atleta, `[TESTE] Atleta Base 01` não apareceu. Andeil também
  não encontrou o nome na conferência de registros da busca. O mesmo atleta
  aparece depois como destaque desta análise. O BUG-003 permanece: o nome
  não foi encontrado na busca, embora exista no destaque.

### 9. Tela Adicionar destaque · Posição

- **Evidência:** print extraído de `TELA CBF 03.ods`.
- **Título:** Adicionar destaque · Posição.
- **Opções visíveis:**
  - Goleiro (posição natural) — 10 características;
  - Lateral direito — 10;
  - Lateral esquerdo — 10;
  - Zagueiro — 11;
  - Volante — 10;
  - Volante 8 — 15;
  - Meia — 15;
  - Atacante de lado — 9;
  - Centroavante — 8.
- **Observado:** a posição natural cadastrada (Goleiro) aparece marcada. O
  menu Observar não está visível neste print; aparecem Gestão, Painéis,
  Configurações e Perfil.

### 10. Novo formulário de atleta com botão desabilitado

- **Evidência:** print `evidencias/tela-novo-atleta-botao-desabilitado.png`.
- **Tela:** Adicionar destaque · Atleta · Novo atleta.
- **Campos visíveis:**
  - Nome: `TESTES`;
  - Ano de nascimento: `2008`;
  - Perna dominante: Ambidestro;
  - Posição natural: vazia (`Buscar posição`);
  - Clube: duas opções `TESTES`, a primeira selecionada;
  - botão **Cadastrar** claro, aparentemente desabilitado.
- **Observado:** o botão volta a ficar desabilitado quando a posição natural
  não está preenchida, de novo sem mensagem clara. Isso reforça o BUG-001.

### 11. Análise finalizada com destaque em rascunho

- **Evidência:** print `evidencias/tela-analise-finalizada-destaque-rascunho.png`.
- **Tela:** análise `TESTES × TESTES`.
- **Observado na tela:**
  - status da análise: **Finalizada**;
  - data: `TESTES · 31/10/2026`;
  - modo: In loco;
  - botão **Adicionar destaque** ainda visível;
  - um destaque: `[TESTE] Atleta Base 01`;
  - posição do destaque: Zagueiro;
  - clube: TESTES;
  - quantidade de avaliações: `0 avaliações`;
  - status do destaque: **Rascunho**.
- **Fato:** o atleta de teste existe neste destaque. O cadastro não se
  perdeu por completo.
- **Fato:** a busca de atleta, feita antes, não encontrou esse nome.
- Registrado como **BUG-003** (nome não aparece na busca) e **BUG-004**
  (análise finalizada com destaque em rascunho e sem avaliações).
- **Confirmação de Andeil:** a análise aparece como **Finalizada**.
- **Limite do ticket:** esta análise já está finalizada. Não clicar em
  **Adicionar destaque** nem alterar o rascunho.

### 12. Lista de Observações com nova análise em andamento

- **Data:** 30 de outubro de 2026.
- **Evidência:** `evidencias/tela-observacoes-analise-em-andamento.png`.
- **Tela:** Observações · aba **Análises em andamento**.
- **Resultado obtido:** existe uma análise nova:
  - título: `teste A x teste B`;
  - status: **Em andamento**;
  - descrição: `teste`;
  - data: `31/10/2026`;
  - destaques: `0 destaques`;
  - modo: **Vídeo**.
- **Observado:** o prefixo `[TESTE]` não foi usado neste título. O registro
  parece novo e ainda sem destaques. Próximo passo: abrir essa análise,
  adicionar destaque e buscar `[TESTE] Atleta Base 01`.

### 13. Busca de atleta com o termo “teste”

- **Evidência:** `evidencias/tela-buscar-atleta-teste.png`.
- **Tela:** Adicionar destaque · Atleta · aba **Buscar atleta**.
- **Ação:** buscar por nome com o texto `teste`.
- **Resultado obtido:** “Nenhum atleta encontrado. Cadastre um novo.”

### 14. Reteste da busca por `[TESTE] Atleta Base 01`

- **Tela:** Adicionar destaque · Atleta · aba **Buscar atleta**, dentro da
  análise `teste A x teste B`.
- **Ação:** buscar pelo nome exato `[TESTE] Atleta Base 01`.
- **Resultado obtido (confirmado por Andeil):** nenhum atleta encontrado.
- **Observado:** o mesmo nome aparece como destaque em rascunho na análise
  finalizada `TESTES × TESTES`. Isso reforça o **BUG-003**.
- **Limite:** não selecionar atleta de outra pessoa.

## Observações

- Em 29/10/2026 a conta `andeilabreu` autenticou no GitHub com sucesso, mas o
  repositório `thatix-io/cbf-scouting-mvp-metaspecs` ainda retornou 404
  (sem permissão). A leitura das regras de negócio continua bloqueada até a
  liberação no ticket.
- Nenhum clube, atleta, avaliação ou usuário existente foi editado.

## Dúvidas

- O usuário de QA deveria ter perfil de administrador ou um perfil mais
  restrito de observador?
- Quais telas o observador técnico realmente usa no dia a dia?

## Resultado da sessão

Em andamento. A análise `TESTES × TESTES` está **Finalizada**. O atleta
`[TESTE] Atleta Base 01` aparece nela como destaque em **Rascunho**, com
`0 avaliações`. Em 30/10/2026, na análise `teste A x teste B`, a busca pelo
nome exato também não encontrou o atleta. **BUG-003** reforçado. **BUG-004**
permanece aberto.
