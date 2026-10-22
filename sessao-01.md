# Sessão 01 — Teste exploratório

## Identificação

- **QA:** Andeil Abreu
- **Ambiente:** produção — https://cbf.lupafut.com/
- **Data:** 22 de outubro de 2026
- **Duração:** em andamento
- **Status:** iniciada — observação da autenticação

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

## Observações

- A documentação em `thatix-io/cbf-scouting-mvp-metaspecs` ainda não pôde ser
  lida por esta conta GitHub.
- Nenhum clube, atleta, avaliação ou usuário existente foi editado.

## Dúvidas

- O usuário de QA deveria ter perfil de administrador ou um perfil mais
  restrito de observador?
- Quais telas o observador técnico realmente usa no dia a dia?

## Resultado da sessão

Em andamento. Próximo passo: entrar pela interface no navegador e observar os
menus, sem clicar em editar registros existentes.
