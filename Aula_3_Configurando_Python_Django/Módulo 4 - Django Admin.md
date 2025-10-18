
# 🧩 Módulo 4 – Django Admin

## 🎯 Objetivo do módulo
Explorar o **painel administrativo do Django** em profundidade, aprendendo a personalizá-lo para deixá-lo mais bonito, funcional e com a cara da escola.

---

## Inicializar Ambiente

- Abra o terminal de comandos do Sistema Operacional que você estiver utilizando.

### Windows

```bash
cd Documents/curso_django
venv\Scripts\activate
cd escola
python manage.py runserver
```
 
### Linux

```bash
cd Documentos/curso_django
source venv/bin/activate
cd escola
python3 manage.py runserver
```

---

## 1. O que é o Django Admin?

- O Django Admin é uma ferramenta automática que o framework cria para facilitar a administração dos dados do sistema.
- Ele permite **cadastrar, visualizar, editar e excluir registros** sem precisar criar telas manualmente.
- Com poucos comandos, é possível ter um painel completo de gerenciamento para o sistema escolar.

---

## 2. Criando o superusuário

Antes de acessar o painel, é preciso criar um **usuário administrador**:

```bash
python manage.py createsuperuser
```

O terminal pedirá:

```
Username: admin
Email address: (opcional)
Password: ******
```

Depois, acesse no navegador:

```
http://127.0.0.1:8000/admin
```

---

## 3. Registrando models no admin

- Por padrão, o Django Admin não mostra nada até que você **registre** os modelos.

- Abra `admin.py` do seu app e registre as tabelas que deseja gerenciar:

```python
from django.contrib import admin
from .models import Aluno, Professor

admin.site.register(Aluno)
admin.site.register(Professor)
```

---

## 4. Personalizando a listagem

- Você pode definir **quais colunas aparecem** e como o Django deve exibir os dados:

```python
admin.site.register(Aluno)

class AlunoAdmin(admin.ModelAdmin):
    list_display = ('id', 'nome', 'idade', 'cidade', 'curso')
    list_display_links = ('nome',)
    search_fields = ('nome', 'cidade')
    list_filter = ('curso', 'cidade')
    ordering = ('nome',)
    list_per_page = 10
    readonly_fields = ('id',)
```

### Explicando cada opção
| Configuração | Função |
|---------------|--------|
| `list_display` | Define as colunas que aparecem na tabela |
| `list_display_links` | Define quais colunas são clicáveis |
| `search_fields` | Adiciona campo de busca |
| `list_filter` | Adiciona filtro lateral |
| `ordering` | Define a ordem padrão |
| `list_per_page` | Limita a quantidade por página |
| `readonly_fields` | Define campos somente leitura |

---

## 5. Personalizando formulários de cadastro

- Para controlar quais campos aparecem no formulário e sua ordem:

```python
admin.site.register(Aluno)

class AlunoAdmin(admin.ModelAdmin):
    fields = ('nome', 'idade', 'curso', 'cidade')
```

### Agrupando campos com `fieldsets`
```python
admin.site.register(Aluno)

class AlunoAdmin(admin.ModelAdmin):
    fieldsets = (
        ('Informações pessoais', {
            'fields': ('nome', 'idade', 'cidade')
        }),
        ('Informações acadêmicas', {
            'fields': ('curso',)
        }),
    )
```
- Esses agrupamentos deixam o formulário mais organizado e agradável.

---

## 6. Exibindo dados calculados

- Você pode mostrar **informações derivadas** dos dados reais.

```python
admin.site.register(Aluno)

class AlunoAdmin(admin.ModelAdmin):
    list_display = ('nome', 'idade', 'curso', 'is_maior')

    def is_maior(self, obj):
        return obj.idade >= 18

    is_maior.short_description = "Maior de idade"
```
- O método `is_maior` cria uma nova coluna na listagem com “Sim” ou “Não”.

---

## 7. Personalizando o visual do painel

### 7.1 Alterar o título e cabeçalho

- No `admin.py` principal (ou em qualquer app):

```python
from django.contrib import admin

admin.site.site_header = "Painel da Escola"
admin.site.site_title = "Administração Escolar"
admin.site.index_title = "Bem-vindo ao sistema!"
```
Essas linhas alteram os textos exibidos no topo e nas abas do navegador.

---

### 7.2 Tema moderno com **Django Jazzmin**

- O Jazzmin transforma o admin em um painel visualmente moderno.

#### Instalação:

```bash
pip install django-jazzmin
```

Em `settings.py`, adicione **antes** de `'django.contrib.admin'`:

```python
INSTALLED_APPS = [
    'jazzmin',
    'django.contrib.admin',
    ...
]
```

- O painel ganhará menus laterais, ícones e um tema escuro automático.

---

## 8. Controle de permissões e grupos
O Django Admin possui um sistema de permissões poderoso:
- **Superusuário** → acesso total  
- **Usuário comum** → acesso limitado  
- **Grupos** → conjunto de permissões (ex: “Professores”, “Secretaria”)

No painel, vá em:
```
Admin → Grupos → Adicionar Grupo
```
E marque as permissões desejadas (ex: pode visualizar alunos, mas não excluir).

---

## 9. Ações personalizadas
Você pode adicionar **botões de ação** para realizar tarefas em massa.
Exemplo: marcar alunos como “ativos”.

```python
@admin.action(description="Marcar alunos como ativos")
def marcar_ativos(modeladmin, request, queryset):
    queryset.update(ativo=True)

@admin.register(Aluno)
class AlunoAdmin(admin.ModelAdmin):
    list_display = ('nome', 'curso', 'ativo')
    actions = [marcar_ativos]
```
Essas ações aparecem em um menu no topo da listagem do admin.

---

## 10. Desafios práticos
1. Use `fieldsets` para organizar o formulário de professores. 
2. Crie um grupo de usuários com permissão apenas para visualizar dados.  
3. Faça uma coluna no admin mostrando se o aluno é maior de idade.

---

## Resumo do módulo
| Recurso | Função |
|----------|--------|
| `list_display` | Define colunas na listagem |
| `search_fields` | Adiciona busca |
| `list_filter` | Cria filtros laterais |
| `fieldsets` | Agrupa campos |
| `readonly_fields` | Campos somente leitura |
| `actions` | Cria ações personalizadas |
| `Jazzmin` | Deixa o admin moderno e bonito |

---

## 🚀 Próximo passo
No **Módulo 5**, aprenderemos a criar **páginas personalizadas** com *views* e *templates*, para que o usuário comum (não administrador) também possa interagir com o sistema escolar.
