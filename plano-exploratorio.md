# Plano da sessão exploratória

## Objetivo da sessão

Descobrir como a plataforma se comporta para um observador técnico, sem alterar
dados reais já existentes.

## Carta de teste

Explorar o fluxo de observação de jogadores e o apoio à convocação, criando
somente dados novos com o prefixo `[TESTE]`, para identificar falhas de
validação, usabilidade, permissão e consistência das informações.

## Áreas previstas para observação

A lista abaixo é um ponto de partida. Ela será ajustada depois do acesso real
à plataforma e da leitura da documentação.

- Acesso e autenticação.
- Navegação inicial e menus disponíveis para o usuário de QA.
- Cadastro de clube com prefixo `[TESTE]`.
- Cadastro de atleta com prefixo `[TESTE]`.
- Criação de avaliação com prefixo `[TESTE]`.
- Consulta de informações criadas no próprio teste.
- Mensagens de erro, campos obrigatórios e salvamento.
- Comportamento ao tentar usar ou editar dados que o ticket proíbe.

## Riscos a observar

- O usuário conseguir editar avaliação concluída.
- O usuário conseguir alterar usuário, clube ou jogador já existente.
- O sistema aceitar cadastro sem o prefixo `[TESTE]` sem aviso, no contexto
  deste exercício.
- Perda de dados ao salvar.
- Permissões diferentes das esperadas para o perfil de QA.
- Telas sem mensagem clara quando uma ação é recusada.

## Regras da sessão

- Não usar dados reais já cadastrados.
- Parar imediatamente se uma tela pedir alteração de registro existente.
- Anotar hora, tela, ação, resultado esperado e resultado obtido.
- Separar fato observado, dúvida e sugestão.
