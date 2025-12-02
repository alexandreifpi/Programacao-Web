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

Abra o arquivo `alunos/models.py` e na `class Aluno` insira o novo atributo que será responsável por armazenar a foto dos alunos:

``` python
imagem = models.ImageField(upload_to='fotos/', null=True)
```
