# 🧩 Módulo 3 – Trabalhando com Models, Banco de Dados e Tipos de Campos Django

## 🎯 Objetivo do módulo
Compreender **o que é um banco de dados**, como ele armazena informações, e aprender a criar **models no Django**, entendendo os principais tipos de campos que podemos usar em uma aplicação web.

---

## 1. O que são dados e por que precisamos guardá-los?

No mundo digital, **quase tudo é dado**.  
Quando você:
- Cria uma conta no Instagram, seu nome e e-mail são dados.
- Faz uma compra online, o produto, o valor e o endereço são dados.
- Frequenta uma escola, o nome do aluno, notas e presença também são dados.

Essas informações não podem ficar “no ar” — elas precisam ser **guardadas em algum lugar seguro e organizado**, para que o sistema consiga **buscar, alterar e mostrar** quando necessário.

**Exemplo:** Imagine que a escola precisa mostrar o boletim do aluno João. Essas notas precisam estar **guardadas** em algum lugar — e é o **banco de dados** que faz isso.

---

## 2. O que é um banco de dados?

Um **banco de dados (database)** é como um **grande armário digital**, cheio de gavetas (tabelas).  
Cada gaveta guarda um tipo de informação, como:

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

- **Tabelas** → guardam informações de um tipo específico.  
- **Campos (colunas)** → descrevem o tipo de dado (nome, idade, nota...).  
- **Registros (linhas)** → cada registro é um conjunto de informações completas sobre um item (um aluno, uma prova, etc).  

**Exemplo visual:**

| id | nome | idade | cidade | curso |
|----|------|--------|--------|--------|
| 1 | João | 17 | Picos | Redes |
| 2 | Maria | 16 | Oeiras | Informática |
| 3 | Pedro | 18 | São Raimundo | Design |

Aqui temos **3 registros**, representando 3 alunos.

---

## 4. Como o Django se conecta ao banco de dados

O Django utiliza algo chamado **ORM (Object-Relational Mapper)**.

Em vez de escrever comandos complicados em SQL, você cria **classes em Python**, e o Django **traduz automaticamente** para SQL.

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

## 5. Criando o Model `Aluno` passo a passo

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

### Explicando os tipos de campos usados:
- `CharField(max_length=100)` → campo de texto curto (nome, cidade, curso).  
- `IntegerField()` → campo numérico inteiro (idade).  
- `__str__` → mostra o nome do aluno quando listamos objetos no admin ou no terminal.

---

## 6. Tipos de Campos no Django (Model Fields)

Além de `CharField` e `IntegerField`, existem outros campos úteis:

| Campo Django | O que armazena | Exemplo prático |
|--------------|----------------|----------------|
| `TextField` | Texto longo | Observações do aluno |
| `FloatField` | Número decimal | Nota da prova |
| `BooleanField` | Verdadeiro ou falso | Aluno ativo ou não |
| `DateField` | Data | Data de nascimento |
| `DateTimeField` | Data e hora | Hora da matrícula |
| `EmailField` | E-mail | Email do aluno |
| `URLField` | URL | Link para portfólio |
| `ForeignKey` | Relacionamento 1:N | Cada aluno pertence a uma turma |
| `ManyToManyField` | Relacionamento N:N | Aluno pode ter várias disciplinas |

**Exemplo de model com mais campos:**

```python
class Professor(models.Model):
    nome = models.CharField(max_length=100)
    disciplina = models.CharField(max_length=50)
    email = models.EmailField()
    ativo = models.BooleanField(default=True)

class Turma(models.Model):
    nome = models.CharField(max_length=50)
    professores = models.ManyToManyField(Professor)
```

---

## 7. Criando e aplicando migrações

No terminal:

```bash
python manage.py makemigrations
python manage.py migrate
```

- `makemigrations` → cria “planos de mudança” para o banco.  
- `migrate` → aplica as mudanças criando ou alterando tabelas.  

Após isso, será criado o arquivo `db.sqlite3`, que guarda todos os dados.

---

## 8. Explorando o banco com SQLite

Você pode abrir `db.sqlite3` com:
- [DB Browser for SQLite](https://sqlitebrowser.org/)
- Ou extensões no VS Code como “SQLite Viewer”.

Lá você verá tabelas como:
- `alunos_aluno`
- `auth_user`
- `django_migrations`

Cada coluna do model aparece como campo da tabela.

---

## 9. Desafios guiados

1. Adicione um campo `email` ao model Aluno e aplique migrações.  
2. Crie um model `Professor` com campos: `nome`, `disciplina`, `email`, `ativo`.  
3. Explique: o que é uma tabela? o que é um registro? Qual a relação entre model e tabela?  
4. Bônus: imagine um sistema de biblioteca escolar. Quais seriam as tabelas necessárias?

---

## Resumo do módulo

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

No **Módulo 4**, veremos como **visualizar, adicionar e editar** esses dados diretamente pelo **Django Admin**.
