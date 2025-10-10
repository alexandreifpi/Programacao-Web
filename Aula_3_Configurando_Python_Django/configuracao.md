# Instalação Django

## O que é terminal, cmd ou linha de comando?

- O terminal é o programa que permite digitar comandos para interagir com o sistema operacional. 
- É uma interface de texto (sem janelas, ícones nem botões).

### Como abrir o terminal no Linux?

- Pressione o menu inicial do teclado, e digite a palavra **Terminal**.

### Como abrir o terminal no Windows?

- Pressione o menu inical do teclado, e digite a palavra **Cmd**.

## Como instalar o Python?

- Nesta seção você verá como instalar o python nos principais sistemas operacionais:

### Como instalar o Python no Linux

- Primeiro verifique se o Python já está instalado.

```
python3 --version
```

- Caso você já tenha o Python instalado, não precisa instalar novamente, mas caso não tenha, siga o seguinte comando:

```
sudo apt install python3
```

## Criando o ambiente virtual

### Criando o ambiente virtual no Linux

```
python3 -m venv myenv
```

- Você pode receber o seguinte erro:

```
The virtual environment was not created successfully because ensurepip is not
available.  On Debian/Ubuntu systems, you need to install the python3-venv
package using the following command.

    apt install python3.10-venv

You may need to use sudo with that command.  After installing the python3-venv
package, recreate your virtual environment.

Failing command: /home/alexandre/Documentos/Atividades PW/AtividadesDjango/myenv/bin/python3
```

- Caso isso aconteça, execute o seguinte comando:

```
sudo apt install python3.10-venv
```

### Executando o ambiente virtual

```
source myvenv/bin/activate
```

## Instalando o Django

- Com o ambiente virtual executando você está pronto(a) para instalar o Django.

- Vamos, inicialmente, atualizar a versão do Pip, que é o gerenciador de pacotes do Python.

