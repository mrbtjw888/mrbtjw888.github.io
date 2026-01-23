---
title: 'Project part 1'
description: 'Defining a project'
pubDate: '2026-01-23'
heroImage: ''
---

## Project overview
This project is to serve as my learning and demonstrate my skills. I am also building it with monetization in mind.

### The project functionalities include:
1. People can sign up/in with a password or google account. They can also delete their account (unlike some sites...)
2. Logged in people can create a post sharing something, image or gif only (my broke ass can't handle video storage cost)
3. Anyone can a send request to that post.
4. Post creator can see that request

#Disclaimer! I am not responsible for any scam or misuse, this app is effectively promoting direct connection and peer to peer.

### Technology in use:
- Frontend: Astro + Tailwind 4
- Backend: Fastify + Drizzle
- DB: PostgreSQL
- Auth: Better Auth

### Deployment:
- Cloudflare static page
- VPS for API and DB hosting, everything is inside docker
- Grafana and Prometheus for observability
- Github action for basic CICD (might use gitlab in the future) 

## System Design

### Database schema:
User:
```
{
	id: int, (primary key)
	name: str,
	email: str,
	password: str,
	create_at: date,
}
```

Post:
```
{
	id: int,
	title: str,
	content: text,
	user: user.id, (foreign key)
	create_at: date,
	last_edited: date,
}
```

Tag:
```
{
	id: int,
	name: str,
	post: post.id,
}
```

Image:
```
{
	id: int,
	url: str,
	order: int,
	post: post.id,
}
```

Request:
```
{
	id: int,
	name: str,
	email: str,
	message: text,
	user: user.id, (foreign key)
	post: post.id (foreign key)
	create_at: date,
	last_edited: date,
}
```

Post & User: One to One

Post & Tag: Many to Many

Post & Image: One to Many

### API endpoint:

User:
| Method | Description | routes |
|-|-|-|
| GET | Get single user by id | /api/user/:id |
| GET | Get all user | /api/user |
| POST | Create a user | /api/user |
| PUTS | Update a user | /api/user/:id |


Post:
| Method | Description | routes |
|-|-|-|
| GET | Get single post by id | /api/post/:id |
| GET | Get all post | /api/post |
| POST | Create a post | /api/post |
| PUTS | Update a post | /api/post/:id |

Request:
| Method | Description | routes |
|-|-|-|
| GET | Get single request by id | /api/request/:id |
| GET | Get all request | /api/request |
| POST | Create a request | /api/request |
| PUTS | Update a request | /api/request/:id |


### Astro frontend:
Pages:
```
/
/login
/account
/post/:id
/user/:id
/search
/tags
```

That's it for know, I will continue in part 2, starting with the API.