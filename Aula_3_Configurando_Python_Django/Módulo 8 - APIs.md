[11:17, 26/11/2025] Alexandre: # TUTORIAL COMPLETO DE DJANGO REST FRAMEWORK
## Do zero até criar uma API funcional para Alunos e Professores

---

## 1. O que é o Django REST Framework?

O *Django REST Framework (DRF)* é uma biblioteca que transforma um projeto Django em uma *API, permitindo enviar e receber dados no formato **JSON*.

Com uma API você pode:

- Criar apps mobile usando seu backend  
- Conectar o Django com JavaScript moderno (React, Vue, Angular)  
- Criar integrações entre sistemas  
- Fazer comunicação entre servidores  
- Automatizar processos com outras aplicações  

O DRF facilita isso com:

- Serializers  
- Views específicas  
- Autenticação  
- Permissões  
- Documentação automática  
- Suporte nativo a JSON  

---

## 2. Instalando the Django REST Framework

No terminal:

bash
pip install djangorestframework


Depois no arquivo settings.py adicione:

python
INSTALLED_APPS = [
    ...
    'rest_framework',
]


---

## 3. Criando o app da API

Dentro do projeto que já tem *alunos* e *professores*, crie um novo app para a API:

bash
python manage.py startapp api


Depois registre no *settings.py*:

python
INSTALLED_APPS = [
    ...
    'api',
]


---

## 4. Criando os SERIALIZERS

Os serializers transformam um *modelo Django → JSON*.

Crie o arquivo:


api/serializers.py


E coloque:

python
from rest_framework import serializers
from alunos.models import Aluno
from professores.models import Professor

class AlunoSerializer(serializers.ModelSerializer):
    class Meta:
        model = Aluno
        fields = '__all__'

class ProfessorSerializer(serializers.ModelSerializer):
    class Meta:
        model = Professor
        fields = '__all__'


---

## 5. Criando as API Views

Crie o arquivo:


api/views.py


E coloque:

python
from rest_framework import generics
from alunos.models import Aluno
from professores.models import Professor
from .serializers import AlunoSerializer, ProfessorSerializer

# Alunos
class AlunoListCreate(generics.ListCreateAPIView):
    queryset = Aluno.objects.all()
    serializer_class = AlunoSerializer

class AlunoDetail(generics.RetrieveUpdateDestroyAPIView):
    queryset = Aluno.objects.all()
    serializer_class = AlunoSerializer

# Professores
class ProfessorListCreate(generics.ListCreateAPIView):
    queryset = Professor.objects.all()
    serializer_class = ProfessorSerializer

class ProfessorDetail(generics.RetrieveUpdateDestroyAPIView):
    queryset = Professor.objects.all()
    serializer_class = ProfessorSerializer


Essas classes automaticamente implementam:

- *GET* listar
- *POST* criar
- *GET/PUT/PATCH/DELETE* no detalhe

Ou seja: *CRUD completo sem esforço*.

---

## 6. Criando as URLs da API

Crie o arquivo:


api/urls.py


E coloque:

python
from django.urls import path
from .views import (
    AlunoListCreate, AlunoDetail,
    ProfessorListCreate, ProfessorDetail
)

urlpatterns = [
    path('alunos/', AlunoListCreate.as_view()),
    path('alunos/<int:pk>/', AlunoDetail.as_view()),

    path('professores/', ProfessorListCreate.as_view()),
    path('professores/<int:pk>/', ProfessorDetail.as_view()),
]


Agora incluímos no *urls.py principal*:

python
path('api/', include('api.urls')),


---

## 7. Testando a API

### Listar alunos

GET http://localhost:8000/api/alunos/


### Criar aluno

POST http://localhost:8000/api/alunos/


Exemplo JSON:

json
{
    "nome": "Maria",
    "cidade": "São Paulo",
    "idade": 20
}


### Detalhar aluno

GET http://localhost:8000/api/alunos/1/


### Editar aluno

PUT http://localhost:8000/api/alunos/1/


### Deletar aluno

DELETE http://localhost:8000/api/alunos/1/


Mesma lógica para *professores*.

---

## 8. Autenticação (Opcional, mas recomendado)

Para exigir login na API:

No *settings.py*:

python
REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated'
    ]
}


Agora só usuários logados acessam os endpoints.

Dica para testes: crie um superuser com python manage.py createsuperuser e faça login no /admin/ antes de acessar a API no navegador.

---

## 9. Referências rápidas

- Django REST Framework — https://www.django-rest-framework.org/  

---
[12:26, 26/11/2025] Alexandre: 1) Qual definição de re
