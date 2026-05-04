# Car Auction API

A backend API for a vehicle listing platform, enabling users to register as announcers and publish car and motorcycle listings.

## Technologies

- Node.js
- TypeScript
- Express
- PostgreSQL
- TypeORM
- JWT Authentication
- Bcrypt
- Docker

## Features

- User registration with announcer or buyer profile
- JWT authentication
- Full CRUD for vehicle announcements
- Image gallery per announcement
- Comment system on listings
- Protected routes via Bearer Token

## Getting Started

**Requirements:** Docker and Docker Compose

1. Clone the repository and create your `.env` file:

```bash
cp .env.example .env
```

2. Fill in the `.env` variables:

```dotenv
HOST=docker_db
POSTGRES_PASSWORD=yourpassword
POSTGRES_DB=carauction
POSTGRES_USER=carauction_user
SECRET_KEY=yoursecretkey
PGPORT=5432
PORT=3000
```

3. Start the application:

```bash
docker compose up --build
```

The API will be available at `http://localhost:3000`. Migrations run automatically on startup.

## API Endpoints

### Session

**POST** `/session` — Authenticate user
```json
// Request
{ "email": "paulo@mail.com", "password": "Test1234" }

// Response 200
{
  "user": { "id": "33b7f8fe-...", "name": "Paulo", "is_announcer": true },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

### Users

**POST** `/users` — Create user
```json
// Request
{
  "name": "Paulo Silva",
  "email": "paulo@mail.com",
  "cpf": "123456789012",
  "phone": "99999999999",
  "birthdate": "1997-12-05",
  "description": "Announcer user",
  "cep": "01234-567",
  "state": "SP",
  "city": "São Paulo",
  "street": "Rua Um",
  "number": "1",
  "complement": "Casa",
  "is_announcer": true,
  "password": "Test1234"
}

// Response 201
{
  "id": "33b7f8fe-05de-4fc0-bcc6-85d66ac445f0",
  "name": "Paulo Silva",
  "email": "paulo@mail.com",
  "is_announcer": true
}
```

**PATCH** `/users` — Update user — Auth required

**DELETE** `/users` — Delete user — Auth required

**GET** `/users` — List all users

### Announcements

**GET** `/announcements` — List all announcements

**POST** `/announcements` — Create announcement — Auth required
```json
// Request
{
  "title": "Honda Civic",
  "year": "2001",
  "km": 197000,
  "price": 45000,
  "description": "Well maintained vehicle, single owner, full service history.",
  "type_vehicle": "car",
  "image": "https://example.com/honda-civic.jpg",
  "is_active": true,
  "gallery": []
}

// Response 201
{
  "id": "4ee2948e-46d4-443b-8a2a-6460960846dc",
  "title": "Honda Civic",
  "year": "2001",
  "km": 197000,
  "price": 45000,
  "type_vehicle": "car",
  "is_active": true,
  "createdAt": "2023-02-26T18:24:16.498Z"
}
```

**PATCH** `/announcements/:id` — Update announcement — Auth required

**DELETE** `/announcements/:id` — Delete announcement — Auth required