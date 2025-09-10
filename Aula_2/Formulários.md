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

| Atributo 			| Valor									| Descrição 													|
-----------------------------------------------------------------------------------------------------------------------------
| action			| URL de processamento do formulário. 	| Especifica o destino dos dados do formulário.					|
| method			| GET ou POST						  	| Especifica o método HTTP para envio do formulário de dados.	|
| name				| Nome do Formulários				  	| Especifica o nome do formulário.								|
