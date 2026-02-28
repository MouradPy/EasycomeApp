# 🇲🇦 EasyCome — Morocco Tourism Platform

> **Plan your trip. Book your stay. Know your budget. All in one click.**

EasyCome is a full-stack web platform built to help tourists visiting Morocco for the **FIFA World Cup 2030** and the **African Cup of Nations** plan and manage their entire trip — hotels, food, transport, cafés, and more — with an automatic expense calculator that gives them a clear total before they even land.

---

## 🌍 What is EasyCome?

EasyCome solves a real problem: tourists arriving in Morocco don't know how much their trip will cost until it's too late. EasyCome lets them:

- **Browse and book** hotels, riads, apartments, and houses for rent
- **Explore** local restaurants, cafés, and experiences
- **Plan their itinerary** by selecting number of days, meal preferences, and transport type
- **Get an instant total** — all costs calculated automatically in MAD (Moroccan Dirham)
- **Visualize spending** with a clear, interactive expense breakdown chart

---

## ✨ Key Features

| Feature | Description |
|---|---|
| 🏨 Hotel & Accommodation Booking | Search and book hotels, riads, apartments by city, price, and rating |
| ☕ Cafés & Restaurants | Discover local food spots and include them in your budget |
| 💰 Expense Calculator | Select your days, food level, and transport — get total cost instantly |
| 📊 Visual Budget Charts | Doughnut chart showing cost breakdown per category |
| 🔐 Secure Authentication | JWT-based login and registration with role-based access |
| 🔍 Smart Search | Elasticsearch-powered search by city, amenities, and price range |
| ⚡ Fast Performance | Redis caching for instant hotel listings |
| 📱 Responsive Design | Works beautifully on mobile, tablet, and desktop |

---

## 🛠️ Technology Stack

### Backend
- **Spring Boot 3.x** — Core framework
- **Spring Security + JWT** — Authentication & authorization
- **Spring Data JPA** — Database ORM
- **Spring MVC** — REST API web layer
- **Spring Boot Validation** — Input validation
- **Spring Boot Actuator** — Health monitoring
- **Lombok** — Boilerplate reduction

### Database
- **PostgreSQL** — Primary relational database
- **Redis** — Caching & session storage
- **Elasticsearch** — Full-text search

### Frontend
- **Thymeleaf** — Server-side templating (MVP)
- **React.js + Next.js** — Dynamic UI (advanced phase)
- **Tailwind CSS** — Responsive design
- **Chart.js** — Expense visualizations

### DevOps & Tools
- **Maven** — Build tool
- **Docker + Docker Compose** — Containerization
- **JUnit 5 + Mockito** — Testing

---

## 🗂️ Project Structure

```
easycome/
│
├── backend/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/easycome/
│   │   │   │   ├── config/          # Security, Redis, Elasticsearch config
│   │   │   │   ├── controller/      # REST API endpoints
│   │   │   │   ├── service/
│   │   │   │   │   └── impl/        # Business logic implementations
│   │   │   │   ├── repository/      # JPA + Elasticsearch repositories
│   │   │   │   ├── model/           # JPA entities (User, Hotel, Booking...)
│   │   │   │   ├── dto/             # Data Transfer Objects
│   │   │   │   ├── security/        # JWT filter and service
│   │   │   │   ├── exception/       # Global error handling
│   │   │   │   └── EasycomeApplication.java
│   │   │   └── resources/
│   │   │       ├── application.yml
│   │   │       ├── application-dev.yml
│   │   │       └── application-prod.yml
│   │   └── test/
│   ├── pom.xml
│   ├── Dockerfile
│   └── docker-compose.yml
│
└── frontend/
    ├── src/
    │   ├── components/
    │   │   ├── calculator/      # Expense calculator UI
    │   │   ├── booking/         # Hotel booking components
    │   │   ├── auth/            # Login / Register forms
    │   │   └── common/          # Navbar, Footer, Cards
    │   ├── pages/
    │   │   ├── index.js         # Home
    │   │   ├── hotels.js        # Hotel listing
    │   │   ├── calculator.js    # Trip calculator
    │   │   ├── login.js
    │   │   └── register.js
    │   ├── hooks/
    │   ├── services/            # Axios API calls
    │   ├── contexts/            # Auth context
    │   └── styles/
    ├── package.json
    ├── tailwind.config.js
    └── next.config.js
```

---

## 🚀 Getting Started

### Prerequisites

Make sure you have these installed:

- Java 17 or 21
- Maven
- Node.js + npm
- Docker Desktop
- PostgreSQL (or use Docker)

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/easycome.git
cd easycome
```

### 2. Start Infrastructure with Docker

```bash
cd backend
docker-compose up -d
```

This starts PostgreSQL, Redis, and Elasticsearch automatically.

### 3. Run the Backend

```bash
cd backend
./mvnw spring-boot:run
```

Backend will be available at: `http://localhost:8080`

### 4. Run the Frontend

```bash
cd frontend
npm install
npm run dev
```

Frontend will be available at: `http://localhost:3000`

---

## ⚙️ Configuration

Edit `backend/src/main/resources/application.yml`:

```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/easycome
    username: postgres
    password: yourpassword

  redis:
    host: localhost
    port: 6379

  elasticsearch:
    uris: http://localhost:9200

jwt:
  secret: your-very-long-secret-key
  expiration: 86400000  # 24 hours
```

---

## 📡 API Endpoints

### Authentication
| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/auth/register` | Create a new user account |
| POST | `/api/auth/login` | Login and receive JWT token |

### Hotels
| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/hotels` | List all hotels |
| GET | `/api/hotels/{id}` | Get hotel by ID |
| GET | `/api/hotels/location/{city}` | Filter hotels by city |
| POST | `/api/hotels` | Add a new hotel (admin) |

### Bookings
| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/bookings` | Create a new booking |
| GET | `/api/bookings/user` | Get current user's bookings |

### Expense Calculator
| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/calculator/calculate` | Calculate total trip cost |

**Example request:**
```json
{
  "checkIn": "2030-06-10",
  "checkOut": "2030-06-17",
  "guests": 2,
  "hotelId": 5,
  "foodPreference": "STANDARD",
  "transportOption": "PUBLIC",
  "includeCoffee": true,
  "includeTours": false
}
```

**Example response:**
```json
{
  "totalCost": 4850.00,
  "hotelCost": 3500.00,
  "foodCost": 1050.00,
  "transportCost": 250.00,
  "extrasCost": 50.00,
  "currency": "MAD"
}
```

---

## 🧪 Running Tests

```bash
cd backend
./mvnw test
```

---

## 🐳 Docker Deployment

To run the full application stack with one command:

```bash
docker-compose up --build
```

This starts:
- Spring Boot backend on port `8080`
- PostgreSQL on port `5432`
- Redis on port `6379`
- Elasticsearch on port `9200`

---

## 🗺️ Roadmap

- [x] Project architecture & setup
- [x] JWT authentication system
- [x] Hotel CRUD with Redis caching
- [x] Elasticsearch search integration
- [x] Expense calculator API
- [x] Thymeleaf + Tailwind CSS frontend (MVP)
- [ ] React / Next.js frontend migration
- [ ] Google Maps hotel location pins
- [ ] Stripe payment integration
- [ ] Mobile app (React Native)
- [ ] AI-powered trip recommendations

---

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

---

## 📄 License

This project is licensed under the MIT License.

---

## 📬 Contact

Built with ❤️ for Morocco — World Cup 2030 & AFCON ready.

> *"One link. One click. Your whole Morocco trip, planned."*
