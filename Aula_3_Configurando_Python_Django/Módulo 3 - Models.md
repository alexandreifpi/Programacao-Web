# 🧩 Módulo 3 – Trabalhando com Models e Bancos de Dados

## 🎯 Objetivo do módulo
Compreender **o que é um banco de dados**, como ele armazena informações, e aprender a criar **models no Django**, que são a base de qualquer aplicação web dinâmica.

---

## 1. O que são dados e por que precisamos guardá-los?

No mundo digital, **quase tudo é dado**.  
Quando você:
- Cria uma conta no Instagram, seu nome e e-mail são dados.
- Faz uma compra online, o produto, o valor e o endereço são dados.
- Frequenta uma escola, o nome do aluno, notas e presença também são dados.

Essas informações não podem ficar “no ar” — elas precisam ser **guardadas em algum lugar seguro e organizado**, para que o sistema consiga **buscar, alterar e mostrar** quando necessário.

**Exemplo:**  
- Imagine que a escola precisa mostrar o boletim do aluno João.  
= Essas notas precisam estar **guardadas** em algum lugar — e é o **banco de dados** que faz isso.

---

## 2. O que é um banco de dados?

Um **banco de dados (database)** é como um **grande armário digital**, cheio de gavetas (tabelas). Cada gaveta guarda um tipo de informação, como:

| Tabela | O que guarda | Exemplo de dados |
|--------|---------------|------------------|
| Aluno | Dados dos alunos | nome, idade, cidade, curso |
| Professor | Dados dos professores | nome, disciplina |
| Turma | Turmas da escola | 1º Ano A, 2º Ano B |
| Prova | Informações das provas | data, nota, matéria |

Assim, quando o sistema precisa buscar os alunos da turma “1º Ano A”, ele sabe exatamente onde procurar: **na tabela de alunos, filtrando pela turma**.

---

## 3. Estrutura de um banco de dados

Um banco de dados é composto de:

- **Tabelas** → como planilhas do Excel, guardam informações de um tipo específico.  
- **Campos (colunas)** → descrevem o tipo de dado (nome, idade, nota...).  
- **Registros (linhas)** → cada registro é um conjunto de informações completas sobre um item (um aluno, uma prova, etc).  

💬 **Exemplo visual:**

| id | nome | idade | cidade | curso |
|----|------|--------|--------|--------|
| 1 | João | 17 | Picos | Redes |
| 2 | Maria | 16 | Oeiras | Informática |
| 3 | Pedro | 18 | São Raimundo | Design |

Aqui temos **3 registros**, representando 3 alunos.

---

## 4. ⚙️ Como o Django se conecta ao banco de dados

O Django utiliza algo chamado **ORM (Object-Relational Mapper)**.

👉 Em vez de escrever comandos complicados em SQL (a linguagem dos bancos de dados), você cria **classes em Python**, e o Django **traduz automaticamente** para SQL.

Isso significa que:
- Criar uma **classe** = Criar uma **tabela**
- Criar um **atributo** = Criar uma **coluna**
- Criar um **objeto (instância)** = Criar um **registro**

💬 Exemplo:
```python
aluno = Aluno(nome="João", idade=17, cidade="Picos", curso="Redes")
aluno.save()
```
Esse código cria um **novo registro na tabela `alunos_aluno`** dentro do banco de dados.

---

## 5. ✏️ Criando o Model `Aluno` passo a passo

1. Abra o arquivo `models.py` dentro da pasta do app `alunos`.

   ```
   projeto_escola/
   ├── alunos/
   │   ├── models.py
   │   ├── views.py
   │   ├── urls.py
   │   └── templates/
   ```

2. Adicione o seguinte código:

   ```python
   from django.db import models

   class Aluno(models.Model):
       nome = models.CharField(max_length=100)
       idade = models.IntegerField()
       cidade = models.CharField(max_length=100)
       curso = models.CharField(max_length=100)

       def __str__(self):
           return self.nome
   ```

### 🧩 Entendendo o código:
- `models.Model`: indica que essa classe será convertida em uma tabela.
- `CharField`: campo de texto curto.
- `IntegerField`: campo numérico.
- `__str__`: define o texto que aparecerá quando o Django mostrar o objeto.

💡 O nome da tabela criada será `alunos_aluno`, seguindo o padrão `nome_do_app_nome_da_classe`.

---

## 6. 🧮 Criando e aplicando migrações

Depois de definir o model, o Django precisa **gerar e aplicar as migrações**, que são instruções automáticas para criar a tabela no banco.

Abra o **terminal** (ou **Prompt de Comando**, no Windows).

> 🧭 **Dica:** o terminal é uma “janela de comandos”.  
> Em vez de clicar com o mouse, você digita instruções para o computador executar.  
> No Windows, basta procurar por “Prompt de Comando” ou “cmd”.

Dentro da pasta do seu projeto, execute:

```bash
python manage.py makemigrations
python manage.py migrate
```

- `makemigrations`: o Django prepara o plano de criação da tabela.
- `migrate`: o Django executa o plano e cria as tabelas no banco.

💾 Após isso, será criado o arquivo `db.sqlite3`, o banco de dados padrão do Django.

---

## 7. 🔍 Explorando o banco com SQLite

O **SQLite** é um tipo de banco de dados leve — perfeito para testes e pequenos projetos.  
O arquivo `db.sqlite3` guarda todos os dados da aplicação.

Você pode abrir esse arquivo com:
- [DB Browser for SQLite](https://sqlitebrowser.org/)
- Ou extensões no VS Code como “SQLite Viewer”.

Lá, verá tabelas como:
- `alunos_aluno`
- `auth_user` (do sistema de login)
- `django_migrations` (controle interno)

Cada campo que criamos no model aparece como **coluna** no banco.

---

## 8. 🧭 Desafios guiados (para praticar)

1. **Adicione um novo campo “email” ao model Aluno.**  
   Depois rode novamente:
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

2. **Crie um novo model “Professor”** com os campos:
   - `nome`
   - `disciplina`
   - `cidade`

3. **Explique em duplas:**
   - O que é uma tabela?
   - O que é um registro?
   - Qual a relação entre um *model* e uma tabela?

4. **Desafio bônus:**  
   Imagine um sistema de biblioteca escolar.  
   Quais seriam as tabelas necessárias? (Ex: Livro, Autor, Empréstimo, Aluno)

---

## ✅ Resumo do módulo

| Conceito | Significado |
|-----------|-------------|
| Banco de dados | Local onde guardamos informações organizadas |
| Tabela | Conjunto de dados de um mesmo tipo |
| Model | Classe Python que representa uma tabela |
| Campo | Atributo que vira coluna |
| Registro | Linha da tabela com dados completos |
| Migração | Passo que cria ou atualiza as tabelas |
| SQLite | Banco de dados padrão do Django |

---

## 🚀 Próximo passo

No **Módulo 4**, aprenderemos como **visualizar, adicionar e editar** esses dados diretamente pelo **painel administrativo do Django (Django Admin)**.
