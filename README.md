
## Endpoints
Para dar import no insomnia baixe esse arquivo https://drive.google.com/file/d/1755CeEUytUjRfctFpTkCvMytN7fhg5o-/view?usp=sharing
Para importar o arquivo no Insomnia é só baixa-lo. Na palavra "Insomnia" no canto superior esquerdo. Nesse dropdown é só clicar em "Import / Export > Import Data > From File" e selecionar o arquivo que foi feito download

O url base da API é ...

### Rotas que não precisam de autenticação

### LOGIN
POST /login - FORMATO DA REQUISIÇÃO
<br/>
{<br/>
       "email": "barroso<span>@mail.<span>com",<br/>
       "password": "1234"<br/>
}<br/>

Caso dê tudo certo, a resposta será assim:

POST /login - FORMATO DA RESPOSTA - STATUS 200

{<br/>
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImJhcnJvc29AbWFpbC5jb20iLCJpYXQiOjE2NjczMzY1OTYsImV4cCI6MTY2NzM0MDE5Niwic3ViIjoiMyJ9.g7qIjWD0T-Eucfg-77mQ2khOuMTxVjNgBL2hb9TzUfc",<br/>
"user": {<br/>
             "email": "ba<span>rros</span>o<span>@mail.c</span>om",<br/>
	     "isTrainer": false,<br/>
	     "id": 3,<br/>
	     "userId": 3<br/>
	}<br/>
}<br/>

### Rotas que necessitam de autorização
Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma: Authorization: Bearer {token}

### GET STUDENTS
GET /students?userId=value - FORMATO DA REQUISIÇÃO
Na requisição apenas é necessário o TOKEN, a aplicação ficará responsável em buscar o id do usuário no token e retorna ele.

GET /students?userId=value - FORMATO DA RESPOSTA - STATUS 200

[<br/>
	{<br/>
		"email": "gar<span>cia@<span>mail.com",<br/>
		"name": "Gabriel Garcia",<br/>
		"age": 25,<br/>
		"id": 1,<br/>
		"userId": 1<br/>
	},<br/>
	{<br/>
		"email": "maga<span>lhaes@mail.<span>com",<br/>
		"name": "Lucas Magalhães",<br/>
		"age": 25,<br/>
		"course_module": "M3",<br/>
		"id": 3,<br/>
		"userId": 1<br/>
	}<br/>
]<br/>

### ADD STUDENTS
POST /students - FORMATO DA REQUISIÇÃO

{<br/>
"email": "maga<span>lhaes@mail.<span>com",<br/>
  "name":"Lucas Magalhães",<br/>
"course_module": "M3",<br/>
  "id": 4,<br/>
  "userId": 3<br/>
}<br/>

POST /students?userId=value - FORMATO DA RESPOSTA - STATUS 201

{<br/>
	"email": "magal<span>haes@ma<span>il.com",<br/>
	"name": "Lucas Magalhães",<br/>
	"course_module": "M3",<br/>
	"id": 4,<br/>
	"userId": 3<br/>
}<br/>

### DELETE STUDENT
DELETE /students/id

Não é necessário um corpo da requisição.

### CHECKIN
POST /checkin - FORMATO DA REQUISIÇÃO

{<br/>
	"shedule": "14:00",<br/>
	"day": 1,<br/>
	"month": 11,<br/>
	"year": 2022,<br/>
	"status": "succeed",<br/>
	"impediments": true,<br/>
	"userId": 3<br/>
}<br/>

POST /checkin - FORMATO DA RESPOSTA - STATUS 201

{<br/>
	"shedule": "14:00",<br/>
	"day": 1,<br/>
	"month": 11,<br/>
	"year": 2022,<br/>
	"status": "succeed",<br/>
	"impediments": true,<br/>
	"userId": 3,<br/>
	"id": 4<br/>
}<br/>

### GET CHECKIN
GET /checkin?userId=value - FORMATO DA REQUISIÇÃO

Não é necessário um corpo da requisição. 

GET /checkin?userId=3 - FORMATO DA RESPOSTA - STATUS 201 (ex: userId = 3)

[<br/>
	{<br/>
		"shedule": "14:00",<br/>
		"day": 1,<br/>
		"month": 11,<br/>
		"year": 2022,<br/>
		"status": "succeed",<br/>
		"impediments": true,<br/>
		"userId": 3,<br/>
		"id": 3<br/>
	},<br/>
	{<br/>
		"shedule": "14:00",<br/>
		"day": 1,<br/>
		"month": 11,<br/>
		"year": 2022,<br/>
		"status": "succeed",<br/>
		"impediments": true,<br/>
		"userId": 3,<br/>
		"id": 4<br/>
	}<br/>
]<br/>

### GET INFO
GET /users?id=value - FORMATO DA REQUISIÇÃO

Não é necessário um corpo da requisição. 

GET /users?id=3  - FORMATO DA RESPOSTA - STATUS 201 (ex: id = 3)

[<br/>
	{<br/>
		"email": "barros<span>o@mail.<span>com",<br/>
		"password": "$2a$10$gKEkYCoqjdhRGhHBzf173uDhRZBlzHgyKndnblon9lxw2bTvI36FO",<br/>
		"isTrainer": false,<br/>
		"id": 3,<br/>
		"userId": 3<br/>
	}<br/>
]<br/>

### EDIT INFO
PATCH /users/id - FORMATO DA REQUISIÇÃO

{<br/>
	"email": "aly<span>sson@mail.c<span>om",<br/>
  "password": "1234"<br/>
}<br/>

PATCH /users/3 - FORMATO DA RESPOSTA (ex: id = 3)

{<br/>
	"email": "alys<span>son@mail<span>.com",<br/>
	"password": "$2a$10$A8XZ8yfIQZy/JHhqRisDlu.FtCYgvhQnsASkWKUg5QMMEAnfLqGLK",<br/>
	"isTrainer": false,<br/>
	"id": 3,<br/>
	"userId": 3<br/>
}<br/>
