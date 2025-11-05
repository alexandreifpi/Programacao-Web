# Módulo 5 – Views e Templates no Django  
### Ligando o Django ao Mundo Real
---

## 🎯 Objetivos do módulo

Neste módulo, você vai aprender a:

- Entender o papel das **views** e **templates** no Django  
- Criar páginas que exibem dados do banco de dados  
- Cadastrar e editar alunos utilizando páginas próprias
- Conectar tudo: **URLs → Views → Templates → Banco de Dados**

---

## 1. O que são Views?

- As **views** são responsáveis por decidir **o que aparece na tela** quando alguém acessa uma página.  
- Elas recebem a requisição, **pegam os dados do banco**, e enviam para o **template** (o HTML) que será mostrado ao usuário.
  
**Pense assim:**
> A *View* é o cérebro da página.
> O *Template* é o rosto que o usuário vê.

---

## 2. Tipos de Views

No Django, existem dois tipos principais de views:

| Tipo | Nome | Explicação |
|---|---|---|
| **FBV** | Function-Based View | Criadas com funções Python simples — ideais para aprender |
| **CBV** | Class-Based View | Usam classes do Django para automatizar operações comuns |

- Neste curso, vamos **usar FBVs** (Function-Based Views), porque são mais simples e ajudam a entender o que está acontecendo por trás das cortinas.

---

## 3. Relembrando o Model `Aluno`

- Vamos usar o mesmo modelo criado no Módulo 3:

```python
# alunos/models.py
from django.db import models

class Aluno(models.Model):
    nome = models.CharField(max_length=100)
    idade = models.IntegerField()
    cidade = models.CharField(max_length=100)
    curso = models.CharField(max_length=100)

    def __str__(self):
        return self.nome
```

- Esse model já está migrado e registrado no `admin`.  
- Agora, vamos usá-lo nas **views e templates**.

---

## 4. Criando as URLs

- Vamos criar um arquivo `urls.py` dentro do app `alunos` (caso ainda não exista):

```python
# alunos/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.listar_alunos, name='listar_alunos'),
    path('criar/', views.criar_aluno, name='criar_aluno'),
    path('editar/<int:id>/', views.editar_aluno, name='editar_aluno'),
]
```

- E depois, no `urls.py` principal:

```python
# escola/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('alunos.urls')),
]
```

---

## 5. Criando as Views

- Agora vamos criar as **views** em `alunos/views.py`.

### View 1: Listar Alunos

```python
# alunos/views.py
from django.shortcuts import render, redirect, get_object_or_404
from .models import Aluno

def listar_alunos(request):
    alunos = Aluno.objects.all()  # Busca todos os alunos no banco
    return render(request, 'alunos/listar.html', {'alunos': alunos})
```

- Essa função busca todos os alunos no banco de dados e envia para o template `listar.html`.

---

### View 2: Cadastrar Novo Aluno

```python
def criar_aluno(request):
    if request.method == 'POST':
        nome = request.POST.get('nome')
        idade = request.POST.get('idade')
        cidade = request.POST.get('cidade')
        curso = request.POST.get('curso')

        Aluno.objects.create(
            nome=nome,
            email=email,
            curso=curso,
            cidade=cidade
        )
        return redirect('listar_alunos')

    return render(request, 'alunos/criar.html')
```

- Essa view mostra o formulário (GET)
- E cadastra o aluno quando o formulário é enviado (POST)

---

### View 3: Editar Aluno

```python
def editar_aluno(request, id):
    aluno = get_object_or_404(Aluno, id=id)

    if request.method == 'POST':
        aluno.nome = request.POST.get('nome')
        aluno.idade = request.POST.get('idade')
        aluno.cidade = request.POST.get('cidade')
        aluno.curso = request.POST.get('curso')
        aluno.save()
        return redirect('listar_alunos')

    return render(request, 'alunos/editar.html', {'aluno': aluno})
```

---

## 6. Criando as Pastas e Templates

- Crie dentro do app `alunos` a seguinte estrutura:

```
alunos/
 ├── templates/
 │    └── alunos/
 │         ├── listar.html
 │         ├── criar.html
 │         └── editar.html
```

---

### Template: listar.html

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <title>Lista de Alunos</title>
</head>
<body>
    <h1>Lista de Alunos</h1>

    <a href="{% url 'criar_aluno' %}">Cadastrar Novo Aluno</a>

    <ul>
        {% for aluno in alunos %}
            <li>
                <strong>{{ aluno.nome }}</strong> - {{ aluno.cidade }}
                (<a href="{% url 'editar_aluno' aluno.id %}">Editar</a>)
            </li>
        {% empty %}
            <li>Nenhum aluno cadastrado.</li>
        {% endfor %}
    </ul>
</body>
</html>
```

---

### Template: criar.html

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <title>Novo Aluno</title>
</head>
<body>
    <h1>Cadastrar Novo Aluno</h1>

    <form method="POST">
        {% csrf_token %}
        <label>Nome:</label><br>
        <input type="text" name="nome"><br><br>

        <label>Idade:</label><br>
        <input type="number" name="idade"><br><br>

        <label>Cidade:</label><br>
        <input type="text" name="cidade"><br><br>

        <label>Curso:</label><br>
        <input type="text" name="curso"><br><br>

        <button type="submit">Salvar</button>
    </form>

    <a href="{% url 'listar_alunos' %}">Voltar</a>
</body>
</html>
```

---

### Template: editar.html

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <title>Editar Aluno</title>
</head>
<body>
    <h1>Editar Aluno</h1>

    <form method="POST">
        {% csrf_token %}
        <label>Nome:</label><br>
        <input type="text" name="nome" value="{{ aluno.nome }}"><br><br>

        <label>Idade:</label><br>
        <input type="number" name="idade" value="{{ aluno.idade }}"><br><br>

        <label>Curso:</label><br>
        <input type="text" name="curso" value="{{ aluno.curso }}"><br><br>

        <label>Cidade:</label><br>
        <input type="text" name="cidade" value="{{ aluno.cidade }}"><br><br>

        <button type="submit">Salvar Alterações</button>
    </form>

    <a href="{% url 'listar_alunos' %}">Voltar</a>
</body>
</html>
```

---
