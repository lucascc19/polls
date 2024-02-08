<p>A aplicação permite que você crie e participe de enquetes online que são atualizadas instantaneamente. Você pode ver os resultados em tempo real e o ranking das opções.</p>

## Requisitos

Necessário ter instalado:
- Docker
- Node.js

## Configuração

- Instalar dependências (``npm install``)
- Configuração PostgreSQL e Redis (``docker compose up -d``)
- Copiar arquivo (``.env.example`` ``cp .env.example .env``)
- Executar aplicação (```npm run dev``)
- Teste (API Client de sua preferência)

## HTTP

### POST``/polls``

Criar uma nova enquete.

**Request body**

```JSON
{
  "title": "Qual a melhor linguagem de programação?",
  "options": [
    "JavaScript",
    "Java",
    "PHP",
    "C#"
  ]
}
```

**Response body**

```JSON
{
  "pollId": "194cef63-2ccf-46a3-aad1-aa94b2bc89b0"
}
```

### GET ``/polls/:pollId``

Retornar dados de uma única pesquisa.

**Response body**

```JSON
{
  "poll": {
		"id": "e4365599-0205-4429-9808-ea1f94062a5f",
		"title": "Qual a melhor linguagem de programação?",
		"options": [
			{
				"id": "4af3fca1-91dc-4c2d-b6aa-897ad5042c84",
				"title": "JavaScript",
				"score": 1
			},
			{
				"id": "780b8e25-a40e-4301-ab32-77ebf8c79da8",
				"title": "Java",
				"score": 0
			},
			{
				"id": "539fa272-152b-478f-9f53-8472cddb7491",
				"title": "PHP",
				"score": 0
			},
			{
				"id": "ca1d4af3-347a-4d77-b08b-528b181fe80e",
				"title": "C#",
				"score": 0
			}
		]
	}
}
```

### POST``/polls/:pollId/votes``

Adiciona um voto a uma enquete específica.

**Request body**

```JSON
{
  "pollOptionId": "31cca9dc-15da-44d4-ad7f-12b86610fe98"
}
```

## WebSockets

ws ``/polls/:pollId/results``

**Message**

```JSON
{
  "pollOptionId": "da9601cc-0b58-4395-8865-113cbdc42089",
  "votes": 2
}
```
