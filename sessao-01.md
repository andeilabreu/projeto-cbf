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

### 15. Aviso de possíveis atletas duplicados

- **Data:** 5 de novembro de 2026.
- **Evidência:** `evidencias/tela-possiveis-atletas-duplicados.png`.
- **Tela:** Adicionar destaque · Atleta · Novo atleta, na análise
  `teste A x teste B`.
- **Campos observados:**
  - Ano de nascimento: `2010`;
  - Perna dominante: Esquerda;
  - Posição natural: Zagueiro;
  - Clube selecionado: `teste B` (também aparece `teste A`);
  - botão: **É um novo atleta — cadastrar**.
- **Resultado obtido:** aviso amarelo **Possíveis atletas duplicados**, com a
  opção **Usar [TESTE] Atleta Base 01 (2010)**.
- **Observado:** o sistema reconheceu `[TESTE] Atleta Base 01` neste aviso,
  embora a busca por nome (item 14) não o tenha encontrado. Isso reforça o
  BUG-003 e registra inconsistência entre busca e detecção de duplicidade.

### 16. Cadastro de novo atleta avançou para escolha de posição

- **Evidência:** `evidencias/tela-adicionar-destaque-posicao-02.png` e
  `evidencias/tela-adicionar-destaque-posicao-02-lista.png`.
- **Ação:** Andeil clicou em **É um novo atleta — cadastrar**.
- **Resultado obtido:** a tela **Adicionar destaque · Posição** foi aberta.
- **Observado:**
  - a primeira opção aparece como **Zagueiro (posição natural)** — 11
    características;
  - outras posições listadas: Goleiro, Lateral direito, Lateral esquerdo,
    Volante, Volante 8, Meia, Atacante de lado, Centroavante;
  - o fluxo de cadastro avançou sem a mensagem genérica do BUG-002.
- **Próximo passo:** selecionar **Zagueiro (posição natural)** e seguir a
  avaliação do destaque.

### 17. Tela de avaliação do destaque (Passo 1 de 4)

- **Evidência:** `evidencias/tela-editar-observacao-passo1.png` e
  `evidencias/tela-editar-observacao-passo1-proximo.png`.
- **Tela:** Editar observação · **Passo 1 de 4: Avaliar**.
- **URL observada:** `/observacoes/...`
- **Resultado obtido:** formulário de características do zagueiro, com opções
  Ruim, Regular, Bom, Muito bom, Excelente e Não observado.
- **Observado:**
  - características visíveis incluem 1x1 Defensivo, Antecipação, Cabeceio
    Defensivo, Capacidade de Construção, Impulsão, Comunicação e entendimento
    de jogo, Cabeceio Ofensivo, Passe, linha alta/baixa, Velocidade/Aceleração
    e Força;
  - em pelo menos um item (**Cabeceio Ofensivo**) a opção **Bom** estava
    marcada;
  - no fim da tela aparecem **Anterior** e o botão azul **Próximo**.
- **Próximo passo:** marcar as demais características e clicar em **Próximo**.

### 18. Passo 2 de 4 — Classificar

- **Evidência:** `evidencias/tela-editar-observacao-passo2-classificar.png`.
- **Tela:** Editar observação · **Passo 2 de 4: Classificar**.
- **Resultado obtido:** lista de classificação de **1** a **5**, com botões
  **Anterior** e **Próximo**.
- **Observado:** o subtítulo mostra **Clube: —**, embora no cadastro do atleta
  o clube `teste B` tivesse sido selecionado. Isso fica como dúvida/achado.
- **Próximo passo:** escolher uma nota (1 a 5) e clicar em **Próximo**.

### 19. Passo 3 de 4 — Relato

- **Evidência:** `evidencias/tela-editar-observacao-passo3-relato.png`.
- **Tela:** Editar observação · **Passo 3 de 4: Relato**.
- **Resultado obtido:** a tela informa que a IA pode redigir o relato e que
  **o relato é opcional para finalizar**. Existe o botão
  **Iniciar relato com IA**, além de **Anterior** e **Próximo**.
- **Próximo passo sugerido para o teste:** clicar em **Próximo** sem usar a
  IA nesta etapa, para concluir o fluxo mínimo.

### 20. Passo 4 de 4 — Finalizar

- **Evidência:** `evidencias/tela-editar-observacao-passo4-finalizar.png`.
- **Tela:** Editar observação · **Passo 4 de 4: Finalizar**.
- **Checklist observado:**
  - Ao menos uma característica avaliada — marcado;
  - Classificação definida — marcado;
  - Relato (opcional) — não marcado.
- **Resultado obtido:** o botão **Finalizar observação** está disponível.
- **Observado:** o subtítulo continua **Clube: —**.
- **Próximo passo:** clicar em **Finalizar observação** e registrar a tela
  seguinte.

### 21. Destaque finalizado com sucesso

- **Evidência:** `evidencias/tela-analise-destaque-final-base-02.png`.
- **Tela:** análise `teste A x teste B`.
- **Resultado obtido:**
  - status da análise: **Em andamento**;
  - destaque: `[TESTE] Atleta Base 02`;
  - posição/clube: **Zagueiro · teste B**;
  - quantidade: **11 avaliações**;
  - status do destaque: **Final**.
- **Observado:** o fluxo completo de novo atleta + avaliação + finalização da
  observação funcionou. Diferente do BUG-004, aqui o destaque saiu de
  rascunho e ficou **Final** com avaliações preenchidas. O clube `teste B`
  aparece no destaque, mesmo tendo aparecido **Clube: —** durante a edição.

### 22. Confirmação para finalizar a análise

- **Evidência:** `evidencias/tela-confirmar-finalizar-analise.png`.
- **Ação:** Andeil clicou em **Finalizar análise**.
- **Resultado obtido:** modal **Finalizar análise?** com o aviso:
  “Ao finalizar, a partida fica consolidada e não poderá mais ser editada.”
- **Observado:** o destaque `[TESTE] Atleta Base 02` continua **Final**, com
  11 avaliações. Diferente do BUG-004, aqui há avaliação concluída antes do
  fechamento.
- **Próximo passo:** confirmar no botão vermelho **Finalizar análise**.

### 23. Análise teste A x teste B finalizada

- **Evidência:** `evidencias/tela-observacoes-analises-finalizadas.png`.
- **Tela:** Observações · aba **Análises finalizadas**.
- **Resultado obtido:** o card `teste A x teste B` aparece com status
  **Finalizada**, data `31/10/2026`, `1 destaque` e modo **Vídeo**.
- **Observado:** a análise antiga `TESTES x TESTES` também aparece como
  **Finalizada**, com `1 destaque` e modo **In loco**. Há outras partidas
  reais na lista; o ticket proíbe editá-las — apenas observação visual.
- **Conclusão deste fluxo:** com destaque **Final** e avaliações preenchidas,
  a finalização da análise concluiu normalmente.

### 24. Menu Gestão — Central de Gestão

- **Data:** 12 de novembro de 2026.
- **Evidência:** `evidencias/tela-central-de-gestao.png`.
- **Tela:** Central de Gestão (`/gestao`).
- **Resultado obtido:** panorama com filtros e totais.
- **Observado:**
  - subtítulo: “Panorama de observações, atletas e destaques. Clique num
    número para ver a lista.”;
  - card **Diagrama Tático** com link **Montar escalação**;
  - filtros: Posição, Categoria, Clube, Competição (todos em “Todas/Todos”);
  - totais exibidos: **203** partidas observadas, **221** atletas únicos,
    **277** observações, **275** destaques, **13** atletas com 3+ destaques;
  - cada total tem link **Ver lista**.
- **Limite:** nesta etapa só observação. Não editar listas nem montar
  escalação ainda.

### 25. Gestão — lista Partidas observadas

- **Evidência:** `evidencias/tela-gestao-partidas-observadas.png`.
- **Tela:** Partidas (`/gestao/partidas?observed=true&page=1`).
- **Resultado obtido:** grade de cards com status **Finalizada**.
- **Observado:**
  - a análise de teste `teste A x teste B` aparece na lista (1 destaque,
    Vídeo);
  - há várias partidas reais (Flamengo, Corinthians, etc.);
  - cada card mostra data, quantidade de destaques e modo (Vídeo / In loco /
    Não informado).
- **Limite:** não abrir para editar partidas reais. Se for abrir um card,
  preferir apenas `teste A x teste B` ou `TESTES x TESTES`.

### 26. Gestão — lista Atletas únicos

- **Evidência:** `evidencias/tela-gestao-atletas-unicos.png`.
- **Tela:** Atletas (`/atletas?observed=true&page=1`).
- **Resultado obtido:** lista de atletas com busca por nome e cards
  (nome, ano, posição).
- **Observado:** a página lista atletas reais observados. Existe campo
  **Buscar por nome** e botão **Buscar**. Link **← Gestão** no topo.
- **Limite:** não clicar em atletas reais. Próximo passo seguro: buscar
  `[TESTE] Atleta Base 01` e `[TESTE] Atleta Base 02` neste campo.

### 27. Busca em Gestão por `[TESTE] Atleta Base 02`

- **Evidência:** `evidencias/tela-gestao-busca-atleta-base-02.png`.
- **Tela:** Atletas · Buscar por nome.
- **Ação:** buscar `[TESTE] Atleta Base 02`.
- **Resultado obtido:** o atleta foi encontrado.
- **Observado:** card com `[TESTE] Atleta Base 02`, `2010 · Zagueiro`.
  Nesta tela de Gestão a busca funcionou para o Base 02. Ainda falta
  testar o Base 01 na mesma tela (comparar com o BUG-003).

### 28. Busca em Gestão por `[TESTE] Atleta Base 01`

- **Evidência:** `evidencias/tela-gestao-busca-atleta-base-01.png`.
- **Tela:** Atletas · Buscar por nome.
- **Ação:** buscar `[TESTE] Atleta Base 01`.
- **Resultado obtido:** “Nenhum atleta encontrado.”
- **Observado:**
  - Base 02 aparece nesta mesma busca de Gestão;
  - Base 01 não aparece aqui nem em Buscar atleta (BUG-003);
  - Base 01 foi reconhecido no aviso de duplicados (ACH-005) e existe no
    destaque da análise `TESTES × TESTES`.
- **Conclusão parcial:** o problema do Base 01 não é só da tela de destaque;
  a busca de Gestão também não o encontra.

### 29. Menu Painéis — aba Processo

- **Evidência:** `evidencias/tela-paineis-processo.png`.
- **Tela:** Painéis (`/paineis` ou equivalente).
- **Resultado obtido:** painel de análise visual do processo de observação.
- **Observado:**
  - filtros: Posição, Categoria, Clube, Competição, Status, Observador,
    período de/até;
  - abas: Processo (ativa), Analistas, Jogadores, Clubes e competições;
  - cards com totais: **203** partidas, **277** observações, **275**
    destaques, com gráficos;
  - alternância Semana/Mês (Mês selecionado);
  - seção “Cobertura: competição x categoria” parcialmente visível.
- **Limite:** só observação. Não alterar filtros reais nem editar dados.

### 30. Painéis — aba Jogadores

- **Evidência:**
  - `evidencias/tela-paineis-jogadores-topo.png`
  - `evidencias/tela-paineis-jogadores-status.png`
  - `evidencias/tela-paineis-jogadores-recorrencia.png`
- **Tela:** Painéis · Jogadores (`/paineis/jogadores`).
- **Resultado obtido:** painel de atletas com totais e gráficos.
- **Observado:**
  - totais: **221** atletas observados, **13** com 3+ destaques;
  - gráfico **Atletas por status**: Radar (~92), Selecionável (~48), Já
    convocado (~77), Sem status (~2);
  - aviso: “Recorrência não é qualidade...”;
  - gráfico **Recorrência de destaques**: muitos com 1 destaque, menos com 2
    e 3+; link “2 atletas observados sem destaque”;
  - seções seguintes: Atletas por posição observada e Atletas por categoria;
  - opções “Ver como tabela” nos gráficos.
- **Limite:** não clicar em listas que abram edição de atletas reais.

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

Em andamento. Em 05/11/2026, o destaque `[TESTE] Atleta Base 02` foi
concluído (**Final**, 11 avaliações) e a análise `teste A x teste B` passou
para **Finalizada**. **BUG-003**, **BUG-004** e **ACH-005** continuam
registrados.
