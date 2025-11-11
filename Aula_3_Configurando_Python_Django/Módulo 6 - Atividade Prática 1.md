# Atividade Prática: Cadastro de Professores

## 🎯 Objetivo Geral
Nesta atividade, você vai aplicar o que aprendeu sobre Django para criar um **cadastro de professores**, semelhante ao cadastro de alunos desenvolvido anteriormente.

---

## Passo 1 – Criando o Modelo de Professor e Registrando no Admin

### Descrição do problema

A escola deseja cadastrar os professores com informações básicas para controle interno.  
Você deverá criar um model `Professor` com os seguintes campos:

- **nome** (texto)
- **email** (texto)
- **telefone** (texto)
- **disciplina** (texto)

Além disso, o modelo deve ter um método `__str__` retornando o nome do professor, assim como no model Aluno.

Registre o model do Professor para que ele também apareça na tela de Admin do Django.

### Orientações
1. Crie o modelo `Professor` no arquivo `models.py`.
2. Execute as migrações para criar a tabela no banco.
3. Localize o arquivo admin.py dentro do mesmo app onde está o model Professor.
4. Faça o registro do model para que ele apareça no painel admin.
5. Personalize a exibição da listagem, mostrando as colunas mais importantes (por exemplo: nome, e-mail e telefone).
6. Adicione também um campo de busca, permitindo procurar professores pelo nome ou e-mail.

## Passo 2 - Criando a Listagem, Cadastro e Edição públicos de Professores

### Descrição do problema

A direção da escola pediu que o sistema apresente uma página simples com a lista de professores registrados, para cadastro de novos professores e edição de professores já cadastrados.
Essa página deve exibir informações básicas de cada professor, como nome, e-mail e telefone.

**Você deverá criar:**
- Uma view (função Python) que busca os dados dos professores no banco.
- Um template HTML para exibir esses dados.
- Uma rota (URL) que ligue a página ao navegador.

## Orientações
1. Seguir o tutorial 5.

