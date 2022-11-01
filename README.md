
## Endpoints
Para dar import no insomnia baixe esse arquivo https://drive.google.com/file/d/1755CeEUytUjRfctFpTkCvMytN7fhg5o-/view?usp=sharing
Para importar o arquivo no Insomnia é só baixa-lo. Na palavra "Insomnia" no canto superior esquerdo. Nesse dropdown é só clicar em "Import / Export > Import Data > From File" e selecionar o arquivo que foi feito download

O url base da API é ...

### Rotas que não precisam de autenticação

### LOGIN
POST /login - FORMATO DA REQUISIÇÃO

{
  "email": "barroso@mail.com",
  "password": "1234"
}

Caso dê tudo certo, a resposta será assim:

POST /login - FORMATO DA RESPOSTA - STATUS 200

{<br/>
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImJhcnJvc29AbWFpbC5jb20iLCJpYXQiOjE2NjczMzY1OTYsImV4cCI6MTY2NzM0MDE5Niwic3ViIjoiMyJ9.g7qIjWD0T-Eucfg-77mQ2khOuMTxVjNgBL2hb9TzUfc",<br/>
	"user": {<br/>
		"email": "barroso@mail.com",<br/>
		"isTrainer": false,<br/>
		"id": 3,<br/>
		"userId": 3<br/>
	}<br/>
}<br/>

### Rotas que necessitam de autorização
Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

Authorization: Bearer {token}

### GET STUDENTS
GET /students?userId=value - FORMATO DA REQUISIÇÃO
Na requisição apenas é necessário o TOKEN, a aplicação ficará responsável em buscar o id do usuário no token e retorna ele.

GET /students?userId=value - FORMATO DA RESPOSTA - STATUS 200

[
	{
		"email": "garcia@mail.com",
		"name": "Gabriel Garcia",
		"age": 25,
		"id": 1,
		"userId": 1
	},
	{
		"email": "magalhaes@mail.com",
		"name": "Lucas Magalhães",
		"age": 25,
		"course_module": "M3",
		"id": 3,
		"userId": 1
	}
]

### ADD STUDENTS
POST /students - FORMATO DA REQUISIÇÃO

{
	"email": "magalhaes@mail.com",
  "name":"Lucas Magalhães",
	"course_module": "M3",
  "id": 4,
  "userId": 3
}

POST /students?userId=value - FORMATO DA RESPOSTA - STATUS 201

{
	"email": "magalhaes@mail.com",
	"name": "Lucas Magalhães",
	"course_module": "M3",
	"id": 4,
	"userId": 3
}

### DELETE STUDENT
DELETE /students/id

Não é necessário um corpo da requisição.

### CHECKIN
POST /checkin - FORMATO DA REQUISIÇÃO

{
	"shedule": "14:00",
	"day": 1,
	"month": 11,
	"year": 2022,
	"status": "succeed",
	"impediments": true,
	"userId": 3
}

POST /checkin - FORMATO DA RESPOSTA - STATUS 201

{
	"shedule": "14:00",
	"day": 1,
	"month": 11,
	"year": 2022,
	"status": "succeed",
	"impediments": true,
	"userId": 3,
	"id": 4
}

### GET CHECKIN
GET /checkin?userId=value - FORMATO DA REQUISIÇÃO

Não é necessário um corpo da requisição. 

GET /checkin?userId=3 - FORMATO DA RESPOSTA - STATUS 201 (ex: userId = 3)

[
	{
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
		"shedule": "14:00",
		"day": 1,
		"month": 11,
		"year": 2022,
		"status": "succeed",
		"impediments": true,
		"userId": 3,
		"id": 4
	}
]

### GET INFO
GET /users?id=value - FORMATO DA REQUISIÇÃO

Não é necessário um corpo da requisição. 

GET /users?id=3  - FORMATO DA RESPOSTA - STATUS 201 (ex: id = 3)

[
	{
		"email": "barroso@mail.com",
		"password": "$2a$10$gKEkYCoqjdhRGhHBzf173uDhRZBlzHgyKndnblon9lxw2bTvI36FO",
		"isTrainer": false,
		"id": 3,
		"userId": 3
	}
]

### EDIT INFO
PATCH /users/id - FORMATO DA REQUISIÇÃO

{
	"email": "alysson@mail.com",
  "password": "1234"
}

PATCH /users/3 - FORMATO DA RESPOSTA (ex: id = 3)

{
	"email": "alysson@mail.com",
	"password": "$2a$10$A8XZ8yfIQZy/JHhqRisDlu.FtCYgvhQnsASkWKUg5QMMEAnfLqGLK",
	"isTrainer": false,
	"id": 3,
	"userId": 3
}
