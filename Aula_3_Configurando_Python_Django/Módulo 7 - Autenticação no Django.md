# Tutorial de Autenticação no Django (Simples, Sem base.html)

## 🎯 Objetivo

Adicione login, logout e home protegido ao projeto que já contém os cadastros de **Alunos** e **Professores**.

Os alunos aprenderão a:

- Criar um novo aplicativo para login (`contas`)
- Configurar URLs de autenticação
- Criar formulários de login simples
- Proteger páginas com `@login_required`
- Criar uma página inicial com menu simples
- Navegar para Alunos e Professores a partir da Home

---

## 1) Criar o aplicativo `contas`

Sem terminal (onde está `manage.py`):

```
python manager.py startapp contas
```

---

## 2) Configure o aplicativo em `settings.py` da pasta `escola`

### a) Adicione em `INSTALLED_APPS`:

```python
APLICATIVOS_INSTALADOS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    'alunos',
    'professores',
    'contas', # novo aplicativo
]
```

### b) Habilitar o carregamento automático de modelos nos aplicativos:

```python
MODELOS = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': Verdadeiro,
        'OPÇÕES': { ... },
    },
]
```

### c) Configurar URLs de autenticação:

```python
URL_DE_LOGIN = 'login'
LOGIN_REDIRECT_URL = 'home'
URL_REDIRECIONADA_DE_LOGOUT = 'login'
```

---

## 3) Criar visualizações: login, logout e home

Arquivo: `contas/views.py`

```python
from django.shortcuts import render, redirect
from django.contrib.auth import authenticate, login, logout
from django.contrib.auth.decorators import login_required
from django.contrib import messages


def login_usuario(request):
    Se request.method == "POST":
        nome de usuário = solicitação.POST.get("nome de usuário")
        senha = request.POST.get("senha")

        usuário = autenticar(solicitação, nome de usuário=nome de usuário, senha=senha)
        Se o usuário não for None:
            login(solicitação, usuário)
            retornar redirect('home')
        outro:
            messages.error(request, "Usuário ou senha incorreta.")

    retornar render(request, "contas/login.html")


def logout_usuario(request):
    logout(solicitação)
    retornar redirect('login')


@login_required
def home(request):
    retornar render(request, "contas/home.html")
```

---

## 4) Criar URLs do app `contas`

Arquivo: `contas/urls.py`

```python
from django.urls import path
de . importar visualizações

urlpatterns = [
    caminho('login/', views.login_usuario, nome='login'),
    caminho('logout/', views.logout_usuario, nome='logout'),
    caminho('', views.home, nome='home'),
]
```

---

## 5) Incluir URLs no arquivo principal do projeto

Arquivo: `seuprojeto/urls.py`

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    caminho('admin/', admin.site.urls),

    #
    path('', include('contas.urls')),

    # já
    caminho('alunos/', include('alunos.urls')),
    path('professores/', include('professores.urls')),
]
```

---

## 6) Criar templates (sem base.html)

Estrutura:

```
contas/
    modelos/
        contas/
            login.html
            página inicial.html
```

### Modelo: `login.html`

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Login - Sistema Escolar</title>
</head>
<body>
    <h1>Entrar</h1>

    {% if messages %}
        <ul>
            {% para m em mensagens %}
                <li>{{ m }}</li>
            {% endfor %}
        </ul>
    {% endif %}

    <form method="post">
        {% csrf_token %}
        <label>Usuário:</label><br>
        <input type="text" name="username" required><br><br>

        <label>Senha:</label><br>
        <input type="password" name="password" required><br><br>

        <button type="submit">Entrar</button>
    </formulário>
</body>
</html>
```

### Modelo: `home.html`

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Home - Sistema Escolar</title>
</head>
<body>

    <h1>Bem-vindo, {{user.username }}!</h1>

    <p>Escolha uma das opções abaixo:</p>

    <ul>
        <li><a href="/alunos/">Gerenciar Alunos</a></li>
        <li><a href="/professores/">Gerenciar Professores</a></li>
        <li><a href="{% url 'logout' %}">Sair</a></li>
    </ul>

</body>
</html>
```

---

## 7) Proteger páginas de alunos e professores

### Alunos (`alunos/views.py`):

```python
from django.contrib.auth.decorators import login_required

@login_required
def listar_alunos(request):
    alunos = Aluno.objects.all()
    return render(request, "alunos/listar.html", {"alunos":alunos})
```

### Professores (`professores/views.py`):

```python
from django.contrib.auth.decorators import login_required

@login_required
def listar_professores(solicitação):
    professores = Professor.objetos.todos()
    return render(request, "professores/listar.html", {"professores": professores})
```

---

## ✔️ 8) Criar superusuário

```
python manage.py createsuperuser
```

---

## 9) Rodar o servidor

```
python manage.py runserver
```

:

- Login: http://127.0.0.1:8000/login/
- Home: redirecionamento automático após login

---

