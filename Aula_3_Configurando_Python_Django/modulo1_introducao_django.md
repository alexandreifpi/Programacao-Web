# 📗 MÓDULO 1 - INTRODUÇÃO AO DJANGO

## 🎯 Objetivo do Módulo

Aprender o que é Django, configurar o ambiente de desenvolvimento, entender o terminal e criar o primeiro projeto Django.

------------------------------------------------------------------------

## 1. O que é Django?

O **Django** é um **framework web feito em Python**. Ele ajuda você a: 
- Criar sites e sistemas web rapidamente;
- Organizar melhor o código;
- Conectar com banco de dados sem escrever SQL manual;
- Criar sistemas completos com login, formulários e páginas dinâmicas.

### O que é um framework?

É um **conjunto de ferramentas e estruturas** que ajuda você a desenvolver mais rápido, evitando reinventar a roda.

------------------------------------------------------------------------

## 2. Como o Django funciona (MTV)

O Django segue o padrão **MTV (Model--Template--View)**:

  -----------------------------------------------------------------------
  Sigla                     Nome                Função
  ------------------------- ------------------- -------------------------
  **M**                     **Model**           Define as tabelas do
                                                banco de dados (ex:
                                                alunos, cursos).

  **T**                     **Template**        Define a parte visual
                                                (páginas HTML).

  **V**                     **View**            Faz a ligação entre Model
                                                e Template, processando
                                                os dados e exibindo-os.
                                                
  -----------------------------------------------------------------------

### Exemplo de funcionamento

1.  Usuário acessa `http://localhost:8000/alunos/`\
2.  A **View** busca os dados do **Model**\
3.  A **View** envia os dados para o **Template**\
4.  O **Template** exibe os dados na tela

------------------------------------------------------------------------

## 3. O que é o Terminal / Linha de Comando

O **terminal** (ou linha de comando) é uma ferramenta que permite **dizer para o computador o que fazer digitando comandos**, sem usar o mouse.

### Windows

-   **Prompt de Comando:** pressione `Win + R`, digite `cmd` e aperte Enter.\
-   **PowerShell:** pressione `Win + X`, escolha "Windows PowerShell".

### Linux

- **Terminal:** pessione o menu do teclado, digite `terminal` e aperte Enter.\

### 🔹 VS Code

-   Abra a pasta do projeto no VS Code.
-   Vá em **Terminal → Novo Terminal**.\
-   Ele já abre na pasta do projeto e permite digitar comandos.

### 🔹 Comandos básicos

-   `dir` → lista arquivos e pastas no Windows (`ls` no Linux/macOS)\
-   `cd nome_da_pasta` → entra em uma pasta\
-   `cd ..` → volta para a pasta anterior\
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
- `mkdir curso_django` cria a pasta do projeto\
- `cd curso_django` entra dentro dela

------------------------------------------------------------------------

## 5. Instalando o Python

### Windows

- Baixar o Python no site https://www.python.org/downloads/windows/
- Durante a instalação, você verá uma janela marcada "Setup". Certifique-se de marcar a caixa "Adicionar Python 3.X ao PATH" ou "Adicionar Python às suas variáveis de ambiente" e clicar em "Instalar Agora".

<img width="650" height="408" alt="image" src="https://github.com/user-attachments/assets/08b53d4a-d9c5-4fc5-ac7c-806252eeca50" />

### Linux

- Primeiro, vamos verificar se você já possui o Python instalado.
- Abra o terminal e digite o seguinte comando:

```bash
python3 --version
Python 3.X.X
```

-------------------------------------------------------------------------

## 6. Criando o Ambiente Virtual

Um **ambiente virtual** isola as bibliotecas do projeto:

``` bash
python -m venv venv
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

## 📦 6. Instalando o Django

Com o ambiente ativo:

``` bash
pip install django
```

Verifique a versão instalada:

``` bash
django-admin --version
```

------------------------------------------------------------------------

## 🚀 7. Criando o Primeiro Projeto

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
  `manage.py`             Comandos administrativos do Django
  `settings.py`           Configurações do site (idioma, apps, banco)
  `urls.py`               Define as rotas do site
  `asgi.py` / `wsgi.py`   Usados pelo servidor web

------------------------------------------------------------------------

## 🌍 8. Abrindo no VS Code

1.  Abra o VS Code\
2.  **Arquivo → Abrir Pasta** → selecione `curso_django`\
3.  Terminal integrado → use para rodar comandos

------------------------------------------------------------------------

## 🌐 9. Rodando o Servidor

Entre na pasta `escola` (onde está `manage.py`) e digite:

``` bash
python manage.py runserver
```

Abra o navegador e acesse:

    http://127.0.0.1:8000/

Se aparecer a tela do Django, está funcionando! 🎉

------------------------------------------------------------------------

## 🧩 10. Fluxo MTV

    Usuário → URL → View → Model → Template → Navegador

Resumo:\
- URL escolhe a função da View\
- View pega dados do Model\
- View envia dados ao Template\
- Template mostra ao usuário

------------------------------------------------------------------------

## 🧪 11. Exercícios

1.  Abra o terminal e navegue até uma pasta de sua escolha\
2.  Crie a pasta `curso_django` e entre nela\
3.  Crie e ative o ambiente virtual\
4.  Instale Django\
5.  Crie o projeto `escola`\
6.  Rode o servidor e abra a página inicial\
7.  Escreva no caderno o que faz cada arquivo dentro de `escola/`

------------------------------------------------------------------------

✅ **Próximo módulo:**\
**Módulo 2 -- Criando o Primeiro App Django (alunos)**\
→ Vamos criar nosso primeiro aplicativo dentro do projeto, configurar as
rotas (URLs) e exibir nossa primeira página HTML personalizada.
