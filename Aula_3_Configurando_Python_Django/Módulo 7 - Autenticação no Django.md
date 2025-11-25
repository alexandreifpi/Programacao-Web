# Tutorial de Autenticação no Django

## 🎯 Objetivo

Adicionar login, logout e home protegida ao projeto que já contém os cadastros de **Alunos** e **Professores**.

Os alunos aprenderão a:

- Criar um novo app para login (`contas`)
- Configurar URLs de autenticação
- Criar formulários de login simples
- Proteger páginas com `@login_required`
- Criar uma página inicial com menu simples
- Navegar para Alunos e Professores a partir da Home

---

## ✔️ 1) Criar o app `contas`

No terminal (onde está `manage.py`):

```
python manage.py startapp contas
```

---

## ✔️ 2) Configurar o app no `settings.py`

### a) Adicione em `INSTALLED_APPS`:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    'alunos',
    'professores',
    'contas',   # novo app
]
```
### b) Configure URLs de autenticação:

```python
LOGIN_URL = 'login'
LOGIN_REDIRECT_URL = 'home'
LOGOUT_REDIRECT_URL = 'login'
```

---

## ✔️ 3) Criar views: login, logout e home

Arquivo: `contas/views.py`

```python
from django.shortcuts import render, redirect
from django.contrib.auth import authenticate, login, logout
from django.contrib.auth.decorators import login_required
from django.contrib import messages


def login_usuario(request):
    if request.method == "POST":
        username = request.POST.get("username")
        senha = request.POST.get("password")

        user = authenticate(request, username=username, password=senha)
        if user is not None:
            login(request, user)
            return redirect('home')
        else:
            messages.error(request, "Usuário ou senha incorretos.")

    return render(request, "contas/login.html")


def logout_usuario(request):
    logout(request)
    return redirect('login')


@login_required
def home(request):
    return render(request, "contas/home.html")
```

---

## ✔️ 4) Criar URLs do app `contas`

Arquivo: `contas/urls.py`

```python
from django.urls import path
from . import views

urlpatterns = [
    path('login/', views.login_usuario, name='login'),
    path('logout/', views.logout_usuario, name='logout'),
    path('', views.home, name='home'),
]
```

---

## ✔️ 5) Incluir URLs no arquivo principal do projeto

Arquivo: `seuprojeto/urls.py`

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),

    # autenticação
    path('', include('contas.urls')),

    # módulos já feitos
    path('alunos/', include('alunos.urls')),
    path('professores/', include('professores.urls')),
]
```

---

## ✔️ 6) Criar templates (sem base.html)

Estrutura:

```
contas/
    templates/
        contas/
            login.html
            home.html
```

### 🟦 Template: `login.html`

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Login - Sistema Escolar</title>
</head>
<body>
    <h1>Login</h1>

    {% if messages %}
        <ul>
            {% for m in messages %}
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
    </form>
</body>
</html>
```

### 🟩 Template: `home.html`

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Home - Sistema Escolar</title>
</head>
<body>

    <h1>Bem-vindo, {{ user.username }}!</h1>

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

## ✔️ 7) Proteger páginas de alunos e professores

### Alunos (`alunos/views.py`):

```python
from django.contrib.auth.decorators import login_required

@login_required
def listar_alunos(request):
    alunos = Aluno.objects.all()
    return render(request, "alunos/listar.html", {"alunos": alunos})
```

### Professores (`professores/views.py`):

```python
from django.contrib.auth.decorators import login_required

@login_required
def listar_professores(request):
    professores = Professor.objects.all()
    return render(request, "professores/listar.html", {"professores": professores})
```

---

## ✔️ 8) Criar superusuário

```
python manage.py createsuperuser
```

---

## ✔️ 9) Rodar o servidor

```
python manage.py runserver
```

Acesse:

- Login: http://127.0.0.1:8000/login/
- Home: redirecionamento automático após login

---
