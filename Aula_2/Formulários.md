# Formulários HTML

## Introdução

- São a ponte entre o usuário e o sistema.
- Pode conter elementos como campos de texto, áreas de texto, caixas de seleção, botões de rádio, dentre outros elementos.

## Utilização

- Estrutura que permite entrada de dados do usuário.
- Utilizado em:
	- Login e cadastro
	- Pesquisas e enquetes
	- Compras online
	- Contato e feedback

## Estrutura Básica - Tag ```<form>``` 

```
<form action="/processa" method="post">
	<!-- campos -->
</form>
```

## Atributos da Tag ```<form>```


| Atributo | Valor | Descrição |
|--- |--- | --- |
| action | URL de processamento do formulário. | Especifica o destino dos dados do formulário. |
| method | GET ou POST | Especifica o método HTTP para envio do formulário de dados. |
| name | Nome do Formulários | Especifica o nome do formulário. |

## Campos de entrada ```<input>```

- Tipos principais:
	- text (texto simples)
	- email (valida formato de e-mail)
	- password (senha - oculta caracteres)
	- number (números)
	- date (mostra o calendário)
	- radio (seleção de opções)

### Atributos da Tag ```<input>```

| Atributo | Função/Exemplo |
| --- | --- |
| type | Define o tipo do campo (text, email, password, number, date, radio, checkbox) |
| name | Nome do campo para envio dos dados (name="nome") |
| id | Identificador único, usado com label e JavaScript (id="nome") |
| value | Valor inicial ou enviado. |
| placeholder | Texto de dica dentro do campo (placeholder="Digite seu nome") |
| required | Campo obrigatório (required) |
| min / max / maxlength | Define limites de números ou tamanho de texto (min="1" max="100" maxlength="50") |
| readonly / disabled | readonly = não pode editar, mas enviado; disabled = não pode editar e não enviado |

### Tag ```<label>```

- Serve para associar um texto descritivo a um campo de formulário.
- Melhora a usabilidade (o usuário sabe o que deve digitar).
- Melhora a acessibilidade (leitores de tela entendem melhor o formulário).
- Ao clicar no label, o campo correspondente recebe o foco.

### Text

```
<!-- Texto simples -->
<label for="nome">Nome:</label>
<input type="text" id="nome" name="nome" placeholder="Digite seu nome" required>
<br><br>
```

### Email

```
<!-- Email -->
<label for="email">Email:</label>
<input type="email" id="email" name="email" placeholder="Digite seu email" required>
<br><br>
```

### Senha

```
<!-- Senha -->
<label for="senha">Senha:</label>
<input type="password" id="senha" name="senha" placeholder="Digite sua senha" required>
<br><br>
```

### Número

```
<!-- Número -->
<label for="idade">Idade:</label>
<input type="number" id="idade" name="idade" min="1" max="120" required>
<br><br>
```

### Data

```
<!-- Data -->
<label for="nascimento">Data de Nascimento:</label>
<input type="date" id="nascimento" name="nascimento" required>
<br><br>
```

### Radio

```
<!-- Radio (seleção única) -->
<p>Gênero:</p>
<input type="radio" id="masculino" name="genero" value="masculino" required>
<label for="masculino">Masculino</label>
<input type="radio" id="feminino" name="genero" value="feminino">
<label for="feminino">Feminino</label>
<input type="radio" id="outro" name="genero" value="outro">
<label for="outro">Outro</label>
<br><br>
```

### Checkbox

```
<!-- Checkbox (seleção múltipla) -->
<p>Interesses:</p>
<input type="checkbox" id="tecnologia" name="interesses" value="tecnologia">
<label for="tecnologia">Tecnologia</label>
<input type="checkbox" id="musica" name="interesses" value="musica">
<label for="musica">Música</label>
<input type="checkbox" id="esporte" name="interesses" value="esporte">
<label for="esporte">Esporte</label>
<br><br>
```

