
<h1> Endpoints </h1>
	
Para dar import no insomnia baixe esse arquivo https://drive.google.com/file/d/1755CeEUytUjRfctFpTkCvMytN7fhg5o-/view?usp=sharing
Para importar o arquivo no Insomnia é só baixa-lo. Na palavra "Insomnia" no canto superior esquerdo. Nesse dropdown é só clicar em "Import / Export > Import Data > From File" e selecionar o arquivo que foi feito download

O url base da API é ... (Não fizemos o deploy ainda por enquanto vai ser http://localhost...)

<h1 align ='center'>Rotas que não precisam de autenticação</h1>
<br/>
<h2>LOGIN</h2>

`POST /login - FORMATO DA REQUISIÇÃO`

```json	
{
	"email": "barroso@mail.com",
	"password": "1234"
}
```
Caso dê tudo certo, a resposta será assim:
<br/>

`POST /login - FORMATO DA RESPOSTA - STATUS 200`

```json	
{
"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImJhcnJvc29AbWFpbC5jb20iLCJpYXQiOjE2NjczMzY1OTYsImV4cCI6MTY2NzM0MDE5Niwic3ViIjoiMyJ9.g7qIjWD0T-Eucfg-77mQ2khOuMTxVjNgBL2hb9TzUfc",
"user": {
	"email": "barroso@mail.com",
	"is_trainer": false,
	"userId": 3,
	"id": 3
	}
}
```
<h1 align ='center'> Rotas que necessitam de autorização </h1>

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma: Authorization: Bearer {token}

<h2> GET STUDENTS </h2>

`GET /students?userId=value - FORMATO DA REQUISIÇÃO`

Na requisição apenas é necessário o TOKEN, a aplicação ficará responsável em buscar o id do usuário no token e retorna ele.
<br/>

`GET /students?userId=1 - FORMATO DA RESPOSTA - STATUS 200 (ex: userId = 1)`

```json	
[
	{
		"email": "garcia@mail.com",
		"name": "Gabriel Garcia",
		"userId": 1,
		"studentId": 4,
		"id": 1
	},
	{
		"email": "magalhaes@mail.com",
		"name": "Lucas Magalhães",
		"userId": 1,
		"studentId": 5,
		"id": 2
	}
]
```

<h2>ADD STUDENTS</h2>

`POST /students - FORMATO DA REQUISIÇÃO`

```json	
{
	"email": "magalhaes@mail.com",
	"name":"Lucas Magalhães",
  	"userId": 1,
	"studentId": 5,
	"id": 2
}
```

`POST /students?userId=3 - FORMATO DA RESPOSTA - STATUS 201 (ex: userId = 3)`

```json	
{
	"email": "magalhaes@mail.com",
	"name": "Lucas Magalhães",
	"userId": 1,
	"studentId": 5,
	"id": 2
	
}
```

<h2> DELETE STUDENT</h2>

`DELETE /students/id - FORMATO DA REQUISIÇÃO`

Não é necessário um corpo da requisição.
<br/>
`DELETE /students/id - FORMATO DA RESPOSTA - STATUS 200`
Não tem resposta.
<br/>

<h2>CHECKIN TRAINER</h2>

`POST /checkin - FORMATO DA REQUISIÇÃO`

```json	
{
	"name": Alysson",
	"shedule": "14:00",
	"day": 1,
	"month": 11,
	"year": 2022,
	"status": "succeed",
	"userId": 2
}
```

`POST /checkin - FORMATO DA RESPOSTA - STATUS 201`

```json	
{
	"name": "Alysson",
	"shedule": "14:00",
	"day": 1,
	"month": 11,
	"year": 2022,
	"status": "succeed",
	"userId": 2,
	"id": 4
}
```
<h2>CHECKIN STUDENT</h2>

`POST /checkin - FORMATO DA REQUISIÇÃO`

```json	
{
	"name": "Rafael Barroso",
	"shedule": "14:00",
	"day": 1,
	"month": 11,
	"year": 2022,
	"status": "succeed",
	"impediments": true,
	"userId": 3
}
```

`POST /checkin - FORMATO DA RESPOSTA - STATUS 201`

```json	
{
	"name": "Rafael Barroso",
	"shedule": "14:00",
	"day": 1,
	"month": 11,
	"year": 2022,
	"status": "succeed",
	"impediments": true,
	"userId": 3,
	"id": 4
}
```

<h2>GET CHECKIN STUDENT</h2>
*LISTAR TODOS CHECK-INS DO ALUNO COM BASE NO userId (TANTO INSTRUTOR QUANTO ALUNO FAZEM ESSA REQUISIÇÃO)*
`GET /checkin?userId=value - FORMATO DA REQUISIÇÃO`

Não é necessário um corpo da requisição. 
<br/>
`GET /checkin?userId=3 - FORMATO DA RESPOSTA - STATUS 201 (ex: userId = 3)`

```json	
[
	{
		"name": "Rafael Barroso",
		"shedule": "14:00",
		"day": 1,
		"month": 11,
		"year": 2022,
		"status": "succeed",
		"impediments": true,
		"userId": 3,
		"id": 3
	},
	{
		"name": "Rafael Barroso",
		"shedule": "14:00",
		"day": 2,
		"month": 11,
		"year": 2022,
		"status": "succeed",
		"impediments": true,
		"userId": 3,
		"id": 4
	}
]
```
<h2>GET CHECKIN TRAINER</h2>
*LISTAR TODOS CHECK-INS DO INSTRUTOR COM BASE NO userId*
`GET /checkin?userId=value - FORMATO DA REQUISIÇÃO`

Não é necessário um corpo da requisição. 
<br/>
`GET /checkin?userId=2 - FORMATO DA RESPOSTA - STATUS 201 (ex: userId = 2)`

```json	
[
	{
		"name": "Alysson",
		"shedule": "9:00",
		"day": 1,
		"month": 11,
		"year": 2022,
		"status": "succeed",
		"userId": 2,
		"id": 8
	},
	{
		"name": "Alysson",
		"shedule": "9:00",
		"day": 1,
		"month": 11,
		"year": 2022,
		"status": "succeed",
		"userId": 2,
		"id": 9
	}
]
```

<h2>GET INFO</h2>

`GET /users?userId=value - FORMATO DA REQUISIÇÃO`

Não é necessário um corpo da requisição. 
<br/>
`GET /users?userId=3  - FORMATO DA RESPOSTA - STATUS 201 (ex: id = 3)`

```json	
[
	{
		"email": "barroso@mail.com",
		"password": "$2a$10$gKEkYCoqjdhRGhHBzf173uDhRZBlzHgyKndnblon9lxw2bTvI36FO",
		"name": "Rafael Barroso",
		"course_module": "M3",
     		"class": "T13",
		"is_trainer": false,	
		"userId": 3
		"id": 3,
	}
]
```

<h2>EDIT INFO</h2>  
*MESMO ENDPOINT TANTO PARA ALUNO QUANTO PARA INSTRUTOR*
`PATCH /users/id - FORMATO DA REQUISIÇÃO`

```json	
{
	"email": "alysson@mail.com",
	"name": "Alysson digdin",
	"avatar": ""
}
```

`PATCH /users/3 - FORMATO DA RESPOSTA (ex: id = 3)`

```json	
{
	"email": "alysson@mail.com",
	"password": "$2a$10$A8XZ8yfIQZy/JHhqRisDlu.FtCYgvhQnsASkWKUg5QMMEAnfLqGLK",
	"name": "Alysson digdin",
	"avatar": "",
	"is_trainer": true,
	"userId": 2,
	"id": 2
}
```
