BITLY Clone - URL Shortener with Analytics
<div align="center">
https://img.shields.io/badge/version-1.0.0-blue.svg
https://img.shields.io/badge/Spring%2520Boot-3.x-green.svg
https://img.shields.io/badge/React-18-blue.svg
https://img.shields.io/badge/PostgreSQL-14-blue.svg
https://img.shields.io/badge/license-MIT-green.svg

A full-stack, production-ready URL shortener with advanced analytics

Live Demo · Report Bug · Request Feature

</div>
✨ Features
🔗 URL Shortening
Create short URLs from long links

Custom alias support

QR code generation

Path-based and subdomain routing

One-click copy to clipboard

📊 Advanced Analytics
Real-time click tracking

Geographic analytics (country, city)

Device & browser detection

Referral source tracking

Click timeline visualization

👤 User Management
Secure registration & login

JWT authentication

Link management dashboard

Profile customization

Link history & organization

⚡ Advanced Features
Custom domain support

Link expiration dates

Password-protected links

API access for developers

Bulk URL shortening

CSV data export

🚀 Quick Start
Prerequisites
Java 17+

Node.js 18+

PostgreSQL 14+

Maven 3.8+

Installation
Clone the repository

bash
git clone https://github.com/yourusername/bitly-clone.git
cd bitly-clone
Backend Setup

bash
cd backend
# Configure application.properties with your database settings
cp src/main/resources/application.properties.example src/main/resources/application.properties

# Update the properties file with your configuration
# DATABASE_URL, JWT_SECRET, etc.

# Run the backend
mvn spring-boot:run
Frontend Setup

bash
cd ../frontend
# Install dependencies
npm install

# Configure environment
cp .env.example .env.local
# Update REACT_APP_API_URL to point to your backend

# Start development server
npm start
🏗️ Project Structure
text
bitly-clone/
├── backend/
│   ├── src/main/java/com/bitlyclone/
│   │   ├── config/          # Configuration classes
│   │   ├── controller/      # REST controllers
│   │   ├── dto/            # Data Transfer Objects
│   │   ├── entity/         # JPA entities
│   │   ├── exception/      # Custom exceptions
│   │   ├── repository/     # Data access layer
│   │   ├── security/       # JWT and security config
│   │   ├── service/        # Business logic
│   │   └── util/          # Utility classes
│   ├── src/main/resources/
│   │   ├── application.properties
│   │   └── application.properties.example
│   └── pom.xml
│
├── frontend/
│   ├── public/
│   │   └── index.html
│   ├── src/
│   │   ├── components/     # Reusable components
│   │   │   ├── analytics/
│   │   │   ├── common/
│   │   │   ├── dashboard/
│   │   │   └── links/
│   │   ├── contexts/       # React contexts
│   │   ├── hooks/         # Custom hooks
│   │   ├── pages/         # Page components
│   │   ├── services/      # API services
│   │   ├── store/         # Redux store
│   │   ├── types/         # TypeScript types
│   │   ├── utils/         # Helper functions
│   │   ├── App.tsx
│   │   └── index.tsx
│   ├── package.json
│   └── tsconfig.json
│
├── docker/
│   ├── docker-compose.yml
│   └── Dockerfile
│
├── screenshots/           # Project screenshots
├── .github/workflows/     # CI/CD workflows
├── .gitignore
├── LICENSE
└── README.md
📦 Tech Stack
Backend
Java 17 - Core programming language

Spring Boot 3 - Backend framework

Spring Security - Authentication & authorization

Spring Data JPA - Database operations

PostgreSQL - Primary database

JWT - JSON Web Tokens for auth

Lombok - Reduced boilerplate code

Maven - Build automation

Frontend
React 18 - UI library

TypeScript - Type safety

Tailwind CSS - Styling framework

Redux Toolkit - State management

React Router - Navigation

Axios - HTTP client

Chart.js - Analytics visualization

React Hot Toast - Notifications

DevOps
Docker - Containerization

GitHub Actions - CI/CD

Render/Railway - Free tier hosting

Vercel/Netlify - Frontend hosting

🛠️ API Reference
Authentication Endpoints
http
POST /api/auth/register
Content-Type: application/json
{
  "email": "user@example.com",
  "password": "password123",
  "name": "John Doe"
}

POST /api/auth/login
Content-Type: application/json
{
  "email": "user@example.com",
  "password": "password123"
}

GET /api/auth/profile
Authorization: Bearer {token}
URL Endpoints
http
POST /api/links
Authorization: Bearer {token}
Content-Type: application/json
{
  "originalUrl": "https://example.com/very-long-url",
  "customAlias": "myalias",
  "expirationDate": "2024-12-31"
}

GET /api/links
Authorization: Bearer {token}

GET /api/links/{id}/analytics
Authorization: Bearer {token}

DELETE /api/links/{id}
Authorization: Bearer {token}
Public Endpoint
http
GET /{shortCode}
Redirects to original URL
🐳 Docker Deployment
Using Docker Compose

bash
# Clone the repository
git clone https://github.com/yourusername/bitly-clone.git
cd bitly-clone/docker

# Start all services
docker-compose up -d

# Access the application
# Frontend: http://localhost:3000
# Backend: http://localhost:8080
# Database: localhost:5432
Environment Variables
Create a .env file in the docker directory:

env
# Database
POSTGRES_DB=bitlyclone
POSTGRES_USER=admin
POSTGRES_PASSWORD=securepassword

# Backend
JWT_SECRET=your-jwt-secret-key-here
FRONTEND_URL=http://localhost:3000
DATABASE_URL=jdbc:postgresql://db:5432/bitlyclone

# Frontend
REACT_APP_API_URL=http://localhost:8080
🌐 Free Tier Deployment
Option 1: Render (Recommended)
Backend & Database

Push to GitHub

Create new Web Service on Render

Connect GitHub repository

Set build command: mvn clean package

Set start command: java -jar target/*.jar

Add environment variables

Frontend

Create new Static Site on Render

Set build command: npm install && npm run build

Set publish directory: build

Option 2: Railway
bash
# Install Railway CLI
npm i -g @railway/cli

# Deploy backend
cd backend
railway up

# Deploy frontend
cd ../frontend
railway up
Environment Variables Setup
env
# Backend (.env)
DATABASE_URL=postgresql://user:pass@host:5432/dbname
JWT_SECRET=your-secret-key-here
FRONTEND_URL=https://your-frontend.app
ALLOWED_ORIGINS=https://your-frontend.app

# Frontend (.env.production)
REACT_APP_API_URL=https://your-backend.app
REACT_APP_BASE_URL=https://your-frontend.app
📊 Database Schema
sql
-- Users table
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    name VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Links table
CREATE TABLE links (
    id SERIAL PRIMARY KEY,
    short_code VARCHAR(10) UNIQUE NOT NULL,
    original_url TEXT NOT NULL,
    user_id INTEGER REFERENCES users(id),
    clicks INTEGER DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    expires_at TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- Analytics table
CREATE TABLE analytics (
    id SERIAL PRIMARY KEY,
    link_id INTEGER REFERENCES links(id),
    ip_address VARCHAR(45),
    user_agent TEXT,
    referrer TEXT,
    country VARCHAR(100),
    city VARCHAR(100),
    device_type VARCHAR(50),
    browser VARCHAR(50),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
🧪 Running Tests
Backend Tests
bash
cd backend
# Run all tests
mvn test

# Run specific test class
mvn test -Dtest=LinkServiceTest

# Run with coverage
mvn jacoco:report
Frontend Tests
bash
cd frontend
# Run tests
npm test

# Run with coverage
npm test -- --coverage

# Run e2e tests
npm run test:e2e
🤝 Contributing
Contributions are what make the open-source community such an amazing place to learn, inspire, and create. Any contributions you make are greatly appreciated.

Fork the Project

Create your Feature Branch (git checkout -b feature/AmazingFeature)

Commit your Changes (git commit -m 'Add some AmazingFeature')

Push to the Branch (git push origin feature/AmazingFeature)

Open a Pull Request

Development Guidelines
Follow the existing code style

Write meaningful commit messages

Add tests for new features

Update documentation as needed

Ensure all tests pass before submitting PR

📝 License
Distributed under the MIT License. See LICENSE file for more information.

🙏 Acknowledgments
Inspired by Bitly

Icons by React Icons

UI components from Tailwind UI

Deployment guides from Render and Railway

📞 Contact
 Name - Rajshekhar 

Project Link: https://github.com/NBRajshekhar/SpringBoot-BITLY-CLONE

⭐ Show Your Support
Give a ⭐️ if this project helped you!
