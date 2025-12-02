# MÓDULO 8 - UPLOAD DE IMAGENS

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

## 2. Como o Django funciona (MTV)

O Django segue o padrão **MTV (Model--Template--View)**:
  
  | Sigla | Nome | Função |
  |---|---|---|
  | **M** | **Model** | Define as tabelas do banco de dados (ex: alunos, cursos). |
  | **T** | **Template** | Define a parte visual (páginas HTML). |
  | **V** | **View** | Faz a ligação entre Model e Template, processando os dados e exibindo-os. |
  
  -----------------------------------------------------------------------

### Exemplo de funcionamento

1.  Usuário acessa `http://localhost:8000/alunos/`
2.  A **View** busca os dados do **Model**
3.  A **View** envia os dados para o **Template**
4.  O **Template** exibe os dados na tela

------------------------------------------------------------------------

## 3. O que é o Terminal / Linha de Comando

O **terminal** (ou linha de comando) é uma ferramenta que permite **dizer para o computador o que fazer digitando comandos**, sem usar o mouse.

### Windows

-   **Prompt de Comando:** pressione `Win + R`, digite `cmd` e aperte `Enter`.
-   **PowerShell:** pressione `Win + X`, escolha `Windows PowerShell`.

### Linux

- **Terminal:** pessione o menu do teclado, digite `terminal` e aperte `Enter`.

### Instalação do VSCode

- Baixar o VSCode no site oficial para a pasta `Downloads`.

```bash
cd Downloads
sudo apt install ./nome_do_arquivo.deb
```

### VS Code

-   Abra a pasta do projeto no VS Code.
-   Vá em **Terminal → Novo Terminal**.
-   Ele já abre na pasta do projeto e permite digitar comandos.

### Comandos básicos

-   `dir` → lista arquivos e pastas no Windows (`ls` no Linux/macOS)\
-   `cd nome_da_pasta` → entra em uma pasta
-   `cd ..` → volta para a pasta anterior
-   `mkdir nome_da_pasta` → cria uma nova pasta

> Esses comandos serão usados durante todo o curso.

------------------------------------------------------------------------

## 4. Criando a Pasta do Projeto

No terminal, escolha onde quer criar o projeto e digite:

``` bash
mkdir curso_django
cd curso_django
```

Explicando: 
- `mkdir curso_django` cria a pasta do projeto
- `cd curso_django` entra dentro dela

------------------------------------------------------------------------

## 5. Instalando o Python

### Windows

- Baixar o Python no site **https://www.python.org/downloads/windows/**
- Durante a instalação, você verá uma janela marcada "Setup". Certifique-se de marcar a caixa "Adicionar Python 3.X ao PATH" ou "Adicionar Python às suas variáveis de ambiente" e clicar em "Instalar Agora".

<img width="650" height="408" alt="image" src="https://github.com/user-attachments/assets/08b53d4a-d9c5-4fc5-ac7c-806252eeca50" />

### Linux

- Primeiro, vamos verificar se você já possui o Python instalado.
- Abra o terminal e digite o seguinte comando:

``` bash
$ python3 --version
$ Python 3.X.X
```
- Se você já tiver o Python instalado, será exibida a versão da sua instalação, caso contrário, você precisará instalá-lo.

 ``` bash
$ sudo apt install python3
```

-------------------------------------------------------------------------

## 6. Criando o Ambiente Virtual

Um **ambiente virtual** isola as bibliotecas do projeto:

### Windows

``` bash
python -m venv venv
```

### Linux

``` bash
python3 -m venv venv
```

- Em algumas distribuiçõçes do Linux, você pode receber o seguinte erro:

``` bash
The virtual environment was not created successfully because ensurepip is not available.  On Debian/Ubuntu systems, you need to install the python3-venv package using the following command.
   apt install python3-venv
You may need to use sudo with that command.  After installing the python3-venv package, recreate your virtual environment.
```

- Caso você receba esse erro, siga as instruções acima e instale o pacote python3-venv:

``` bash
sudo apt install python3-venv
```

### Ativando o ambiente

-   **Windows:**

    ``` bash
    venv\Scripts\activate
    ```

-   **Linux/macOS:**

    ``` bash
    source venv/bin/activate
    ```

O terminal mostrará `(venv)` no começo da linha.

------------------------------------------------------------------------

## 7. Instalando o Django

Com a sua virtualenv ativa:

``` bash
pip install django
```

Verifique a versão instalada:

``` bash
django-admin --version
```

------------------------------------------------------------------------

## 8. Criando o Primeiro Projeto

Crie o projeto chamado `escola`:

``` bash
django-admin startproject escola
```

Estrutura de pastas:

    curso_django/
    ├── venv/
    └── escola/
        ├── manage.py
        └── escola/
            ├── __init__.py
            ├── settings.py
            ├── urls.py
            ├── asgi.py
            └── wsgi.py

### Explicação de cada arquivo

  Arquivo                 Função
  ----------------------- ---------------------------------------------
  `manage.py`             Comandos específicos do Django
  `settings.py`           Configurações do site (idioma, apps, banco)
  `urls.py`               Define as rotas do site
  `asgi.py` / `wsgi.py`   Usados pelo servidor web

------------------------------------------------------------------------

## 9. Abrindo no VS Code

1.  Abra o VS Code\
2.  **Arquivo → Abrir Pasta** → selecione `curso_django`\
3.  Terminal integrado → use para rodar comandos

------------------------------------------------------------------------

## 10. Rodando o Servidor

Entre na pasta `escola` (onde está `manage.py`) e digite:

``` bash
python manage.py runserver
```

Abra o navegador e acesse:

    http://127.0.0.1:8000/

Se aparecer a tela do Django, está funcionando! 🎉

------------------------------------------------------------------------

## 10. Fluxo MTV

    Usuário → URL → View → Model → Template → Navegador

Resumo:
- URL escolhe a função da View
- View pega dados do Model
- View envia dados ao Template
- Template mostra ao usuário

------------------------------------------------------------------------

## 11. Exercícios

1.  Abra o terminal e navegue até uma pasta de sua escolha
2.  Crie a pasta `curso_django` e entre nela
3.  Crie e ative o ambiente virtual
4.  Instale Django
5.  Crie o projeto `escola`
6.  Rode o servidor e abra a página inicial

