# Motion Active API

A fitness rewards platform built for Motion Sportswear. Users track steps, earn Motion Points, and compete on leaderboards to win real sportswear rewards.

Built as both a real product and a demonstration of professional .NET backend engineering.

---

## Tech Stack

- **Backend:** C# ASP.NET Core 8
- **Database:** PostgreSQL (Supabase)
- **ORM:** Entity Framework Core 8
- **Auth:** JWT Bearer Tokens
- **Docs:** Swagger / OpenAPI
- **Architecture:** Clean Architecture (Domain, Application, Infrastructure, API)

---

## Features (MVP)

- User registration and login with JWT authentication
- Password hashing with BCrypt
- Manual step logging with automatic Motion Points calculation
- Bonus points for hitting 5,000 and 10,000 step milestones
- Daily step cap fraud prevention (50,000 steps max)
- Points transaction history
- Global leaderboard ranked by total points
- Swagger UI for full API documentation and testing

---

## Architecture

The backend follows Clean Architecture with four distinct layers:
MotionActive.Domain         → Entities, no dependencies
MotionActive.Application    → DTOs, interfaces, business logic
MotionActive.Infrastructure → EF Core, database, repositories
MotionActive.API            → Controllers, middleware, Swagger

Dependencies only flow inward — the domain has no knowledge of the database or web framework.

---

## Points System

| Activity | Points |
|---|---|
| 1,000 steps | 10 points |
| 5,000 steps in one log | +25 bonus |
| 10,000 steps in one log | +50 bonus |

---

## Getting Started

### Prerequisites
- .NET 8 SDK
- PostgreSQL database (or Supabase free tier)

### Setup

1. Clone the repository
```bash
git clone https://github.com/mubarizm12/projects.git
cd projects/backend
```

2. Configure your database connection in `appsettings.json`
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Host=...;Database=postgres;Username=...;Password=..."
  },
  "Jwt": {
    "Key": "your-secret-key",
    "Issuer": "MotionActive",
    "Audience": "MotionActiveUsers"
  }
}
```

3. Run migrations
```bash
dotnet ef database update --project MotionActive.Infrastructure --startup-project MotionActive.API
```

4. Run the API
```bash
dotnet run --project MotionActive.API
```

5. Open Swagger
http://localhost:5164/swagger

---

## API Endpoints

### Auth
| Method | Endpoint | Description |
|---|---|---|
| POST | /api/Auth/register | Register a new user |
| POST | /api/Auth/login | Login and receive JWT token |

### Steps
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| POST | /api/Steps/log | ✅ | Log steps and earn points |
| GET | /api/Steps/history | ✅ | View step history |

### Leaderboard
| Method | Endpoint | Description |
|---|---|---|
| GET | /api/Leaderboard/global | Global leaderboard ranked by points |

---

## Roadmap

**Version 2**
- Apple Health / Google Fit sync
- Friends system and friends leaderboard
- Weekly and monthly leaderboards
- Challenges system
- In-app notifications

**Version 3**
- React Native iOS app
- Push notifications
- Shopify reward integration
- AI fitness coach
- Azure deployment pipeline

---

## Author

Built by Mubariz Malik — [github.com/mubarizm12](https://github.com/mubarizm12)