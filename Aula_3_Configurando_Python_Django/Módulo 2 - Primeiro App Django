# MÓDULO 2 - CRIANDO O PRIMEIRO APP DJANGO (ALUNOS)

## 🎯 Objetivo do Módulo

Aprender a criar um aplicativo dentro do projeto Django, configurar URLs, criar views e templates, e exibir a primeira página personalizada.

------------------------------------------------------------------------

## 1. O que é um App no Django?

No Django, um **projeto** pode ter vários **apps**. Um **app** é como um módulo do projeto, responsável por uma parte específica, por exemplo:

-   `alunos` → cadastro e listagem de alunos
-   `cursos` → gerenciamento de cursos
-   `matriculas` → controle de matrículas

💡 **Dica:** Sempre que pensar em "funcionalidade independente", pense em criar um app separado.

------------------------------------------------------------------------

## 2. Criando o App "alunos"

No terminal, estando na pasta do projeto (`curso_django`), digite:

``` bash
cd escola  # entre na pasta que contém manage.py
python manage.py startapp alunos
```

Isso cria a seguinte estrutura:

    escola/
    ├── manage.py
    ├── escola/
    └── alunos/
        ├── __init__.py
        ├── admin.py
        ├── apps.py
        ├── migrations/
        │   └── __init__.py
        ├── models.py
        ├── tests.py
        └── views.py

### Explicando cada arquivo do app

  Arquivo         Função
  --------------- --------------------------------------------------------
  `__init__.py`   Informa que esta pasta é um pacote Python
  `admin.py`      Permite registrar modelos para o painel administrativo
  `apps.py`       Configuração do app
  `migrations/`   Guarda alterações do banco de dados
  `models.py`     Define os modelos (tabelas do banco)
  `tests.py`      Criar testes automáticos (opcional por enquanto)
  `views.py`      Contém as funções que processam as páginas

------------------------------------------------------------------------

## 3. Registrando o App no Projeto

Abra o arquivo `settings.py` (em `escola/escola/settings.py`) e adicione
o app na lista `INSTALLED_APPS`:

``` python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'alunos',  # <-- nosso app
]
```

------------------------------------------------------------------------

## 4. Criando a Primeira View

No arquivo `views.py` do app `alunos`, crie uma função simples:

``` python
from django.http import HttpResponse

def home(request):
    return HttpResponse("Olá! Bem-vindo ao cadastro de alunos.")
```

💡 **Explicação:**
- `request` → informações sobre a requisição do usuário
- `HttpResponse` → retorna uma resposta simples em texto

------------------------------------------------------------------------

## 5. Configurando a URL do App

Crie um arquivo `urls.py` dentro da pasta `alunos` (ainda não existe) e adicione:

``` python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
]
```

Agora, abra o arquivo `urls.py` do projeto (`escola/escola/urls.py`) e inclua o app:

``` python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('alunos/', include('alunos.urls')),  # nosso app
]
```

------------------------------------------------------------------------

## 6. Testando a Primeira Página

No terminal, rode o servidor:

``` bash
python manage.py runserver
```

No navegador, acesse:

    http://127.0.0.1:8000/alunos/

Você verá a mensagem:

    Olá! Bem-vindo ao cadastro de alunos.

🎉 Primeira view funcionando!

------------------------------------------------------------------------

## 7. Criando Templates HTML

Para exibir páginas HTML em vez de texto simples:

1.  Crie uma pasta `templates` dentro de `alunos`:

```{=html}
<!-- -->
```
    alunos/
    └── templates/
        └── alunos/
            └── home.html

2.  No arquivo `home.html`, escreva:

``` html
<!DOCTYPE html>
<html>
<head>
    <title>Cadastro de Alunos</title>
</head>
<body>
    <h1>Bem-vindo ao Sistema de Cadastro de Alunos!</h1>
</body>
</html>
```

3.  Altere a view para renderizar o template:

``` python
from django.shortcuts import render

def home(request):
    return render(request, 'alunos/home.html')
```

Agora, ao acessar `http://127.0.0.1:8000/alunos/`, o navegador exibirá a
página HTML.

------------------------------------------------------------------------

## 8. Exercícios do Módulo

1.  Crie outro app chamado `cursos` e teste uma view simples.
2.  Crie um template para a view do app `alunos` e adicione um parágrafo
    com o seu nome.
3.  Altere a URL do app `alunos` para `alunos/home/` e teste no
    navegador.
4.  Experimente criar outro arquivo HTML e renderizá-lo a partir de uma
    nova view.

------------------------------------------------------------------------
