# MÓDULO 9 - UPLOAD DE IMAGENS

## 🎯 Objetivo do Módulo

- Configurar upload de arquivos no Django
- Criar model com FileField/ImageField
- Criar view que recebe arquivo via request.FILES
- Salvar no model manualmente
- Exibir arquivos enviados

------------------------------------------------------------------------

## 1. Configurações no arquivo `escola/settings.py`

``` python
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

------------------------------------------------------------------------

## 2. Configurando as URLs para servir os arquivos

No arquivo `escola/urls.py` você vai inserir o seguinte código, junto com os demais **imports**:

``` python
from django.conf import settings
from django.conf.urls.static import static
```

Ainda no arquivo `escola/urls.py` você vai inserir o seguinte código no final do arquivo:

``` python
if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

------------------------------------------------------------------------

## 3. Adicionando o campo no models de aluno

### 3.1. Adicionando biblioteca para trabalhar com imagens no Django

``` bash
pip install Pillow
```

### 3.2. Adicionando o campo de imagem no models

Abra o arquivo `alunos/models.py` e na `class Aluno` insira o novo atributo que será responsável por armazenar a foto dos alunos:

``` python
imagem = models.ImageField(upload_to='fotos/', null=True)
```

### 3.3. Rodando as migrações

Agora, devemos executar as migrações para criarmos o novo campo no nosso banco de dados:

- Comando para criar as migrações
``` bash
python manage.py makemigrations
```

- Comando para executar as migrações
``` bash
python manage.py migrate
```

------------------------------------------------------------------------

## 4. Ajustando nossos templates

### 4.1. Ajustando o template criar.html

Na tag `form` do arquivo `alunos/templates/alunos/criar.html` você irá adicionar o código `enctype="multipart/form-data"`, esse código serve para informar que o formulário irá trabalhar com arquivos de mídia.

``` html
<form method="POST" enctype="multipart/form-data">
```

No arquivo `alunos/templates/alunos/criar.html` você deverá inserir o seguinte código `html` abaixo do input de curso. Esse código serve para criar o campo em que iremos fazer o upload da imagem.

``` html
<label>Imagem:</label><br><br>
<input type="file" name="imagem" accept=".png">
```

### 4.2. Ajustando o template editar.html

Na tag `form` do arquivo `alunos/templates/alunos/criar.html` você irá adicionar o código `enctype="multipart/form-data"`, esse código serve para informar que o formulário irá trabalhar com arquivos de mídia.

``` html
<form method="POST" enctype="multipart/form-data">
```

No arquivo `alunos/templates/alunos/editar.html` você deverá inserir o seguinte código `html` abaixo do input de curso. Esse código serve para criar o campo em que iremos fazer o upload da imagem.

``` html
<label>Imagem:</label><br><br>
<input type="file" name="imagem" accept=".png">
```

### 4.3. Ajustando o template listar.html

No arquivo `aluno/templates/alunos/listar.html` você irá adicionar o seguinte código `html` dentro do `for`:

``` html
{% if aluno.imagem %}
    <img src="{{ aluno.imagem.url }}" class="aluno-foto">
{% endif %}
```

------------------------------------------------------------------------

## 5. Ajustando nossas views

### 5.1. Ajustando nossa view de criação

Na função `def criar_aluno(request):` do nosso arquivo `alunos/views.py` você irá inserir o seguinte código abaixo do `curso = request.POST.get('curso')`

``` python
imagem = request.FILES.get('imagem')
```

E onde tem o seguinte código:

``` python
Aluno.objects.create(
    nome=nome,
    idade=idade,
    curso=curso,
    cidade=cidade
)
```

Você deve substituir por:

``` python
Aluno.objects.create(
    nome=nome,
    idade=idade,
    curso=curso,
    cidade=cidade,
    imagem=imagem
)
```

### 5.2. Ajustando nossa view de edição

Na função `def editar_aluno(request, id):` do nosso arquivo `alunos/views.py` você irá inserir o seguinte código abaixo do `aluno.curso = request.POST.get('curso')`

``` python
aluno.imagem = request.FILES.get('imagem')
```

------------------------------------------------------------------------

