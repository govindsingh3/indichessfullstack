# IndiChess

A real-time, full-stack chess playing platform with interactive multiplayer capabilities, built with modern web technologies and cloud-ready architecture.

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [API Documentation](#api-documentation)
- [Contributing](#contributing)
- [License](#license)

---

## Features

✓ **Real-Time Multiplayer Chess** - Play chess matches with other users in real-time using WebSocket connections  
✓ **User Authentication** - Secure OAuth2-based authentication with Google and GitHub  
✓ **Game Management** - Create, join, and manage multiple chess games simultaneously  
✓ **Move Validation** - Comprehensive piece movement logic (Pawns, Rooks, Knights, Bishops, Queens, Kings)  
✓ **Game Analysis** - Review and analyze completed games  
✓ **Chat Integration** - Real-time in-game and global chat functionality  
✓ **Responsive UI** - Modern React-based frontend with intuitive chess board interface  
✓ **Secure Backend** - Spring Security integration with role-based access control  

---

## Tech Stack

### Frontend
- **React** 19.2.3 - UI library
- **React Router DOM** 7.11.0 - Client-side routing
- **Axios** 1.13.2 - HTTP client
- **Socket.JS & STOMP** - Real-time WebSocket communication
- **React Icons** 5.5.0 - Icon library
- **CSS3** - Responsive styling

### Backend
- **Spring Boot** 4.0.1 - Java application framework
- **Spring Security** - Authentication and authorization
- **Spring Data JPA** - ORM and database access
- **Spring WebSocket** - Real-time communication
- **MySQL** 8.x - Relational database
- **OAuth2** - External authentication provider integration
- **Java** 17 - Programming language

### Build & DevOps
- **Maven** - Java build automation
- **npm** - Node.js package manager

---

## Project Structure

```
IndiChess/
├── frontend/                          # React frontend application
│   ├── public/                        # Static assets
│   ├── src/
│   │   ├── components/               # Reusable UI components
│   │   │   ├── game-page-components/ # Game-specific components
│   │   │   │   ├── Board.js          # Chess board display
│   │   │   │   ├── GameContainer.js  # Main game orchestrator
│   │   │   │   ├── GameControls.js   # Game action buttons
│   │   │   │   ├── Moves.js          # Move history
│   │   │   │   ├── Players.js        # Player information
│   │   │   │   └── pieceMoves/       # Piece movement logic
│   │   │   ├── component-styles/     # CSS modules
│   │   │   ├── Header.js
│   │   │   ├── LoginCard.js
│   │   │   └── SideNav.js
│   │   ├── pages/                    # Page components
│   │   │   ├── Game.js               # Game page
│   │   │   └── Home.js               # Landing page
│   │   ├── App.js                    # Root component
│   │   └── index.js                  # Entry point
│   └── package.json
│
├── src/                               # Spring Boot backend
│   ├── main/
│   │   ├── java/com/IndiChess/
│   │   │   ├── Config/               # Spring configuration
│   │   │   │   ├── SecurityConfig.java
│   │   │   │   ├── WebSocketConfig.java
│   │   │   │   └── WebSocketAuthInterceptor.java
│   │   │   ├── Controller/           # REST API endpoints
│   │   │   │   ├── AuthController.java
│   │   │   │   ├── GameWebSocketController.java
│   │   │   │   ├── ChatWebSocketController.java
│   │   │   │   ├── MatchController.java
│   │   │   │   └── ...
│   │   │   ├── Model/                # Entity classes
│   │   │   ├── Service/              # Business logic
│   │   │   ├── Repository/           # Data access layer
│   │   │   ├── Security/             # Security utilities
│   │   │   ├── dto/                  # Data Transfer Objects
│   │   │   └── IndiChessApplication.java
│   │   └── resources/
│   │       └── application.properties
│   └── test/                         # Unit tests
│
├── pom.xml                            # Maven configuration
├── mvnw & mvnw.cmd                    # Maven wrapper scripts
└── README.md                          # This file
```

---

## Prerequisites

Ensure you have the following installed on your system:

- **Java Development Kit (JDK)** 17 or higher
- **Apache Maven** 3.6.0 or higher
- **Node.js** 16.x or higher with npm
- **MySQL** 8.0 or higher
- **Git** for version control

### Verify Installation

```bash
# Check Java version
java -version

# Check Maven version
mvn -version

# Check Node.js and npm versions
node -v
npm -v

# Check MySQL version
mysql --version
```

---

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/govindsingh3/indichessfullstack.git
cd IndiChess
```

### 2. Backend Setup

Navigate to the project root and install backend dependencies:

```bash
# Using Maven wrapper (Windows)
mvnw clean install

# Or using system Maven
mvn clean install
```

### 3. Frontend Setup

Navigate to the frontend directory and install dependencies:

```bash
cd frontend
npm install
cd ..
```

### 4. Database Setup

Create the MySQL database and tables:

```bash
# Connect to MySQL
mysql -u root -p

# Create database (the app will auto-create on first run with ddl-auto=create-drop)
CREATE DATABASE Indichess_db;

# Exit MySQL
exit
```

---

## Configuration

### Backend Configuration

Update [src/main/resources/application.properties](src/main/resources/application.properties) with your settings:

```properties
# Database Configuration
spring.datasource.url=jdbc:mysql://localhost:3306/Indichess_db?createDatabaseIfNotExist=true
spring.datasource.username=root
spring.datasource.password=YOUR_MYSQL_PASSWORD
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA Configuration
spring.jpa.hibernate.ddl-auto=create-drop
spring.jpa.show-sql=true

# OAuth2 Configuration
spring.security.oauth2.client.registration.google.client-id=YOUR_GOOGLE_CLIENT_ID
spring.security.oauth2.client.registration.google.client-secret=YOUR_GOOGLE_CLIENT_SECRET
spring.security.oauth2.client.registration.github.client-id=YOUR_GITHUB_CLIENT_ID
spring.security.oauth2.client.registration.github.client-secret=YOUR_GITHUB_CLIENT_SECRET

# Default Security Credentials
spring.security.user.name=user
spring.security.user.password=user
```

### OAuth2 Setup

1. **Google OAuth**: Visit [Google Cloud Console](https://console.cloud.google.com/)
   - Create a new project
   - Enable Google+ API
   - Create OAuth2 credentials (Web application)
   - Add `http://localhost:8080` to authorized redirect URIs

2. **GitHub OAuth**: Visit [GitHub Developer Settings](https://github.com/settings/developers)
   - Create a new OAuth App
   - Set Authorization callback URL to `http://localhost:8080/login/oauth2/code/github`

### Frontend Configuration

Update the API endpoint in frontend configuration if your backend is running on a different port:

```javascript
// In frontend/src/services/api.js or similar
const API_BASE_URL = 'http://localhost:8080';
```

---

## Running the Application

### Start MySQL Server

```bash
# Windows (if MySQL is installed as a service)
net start MySQL80

# Or start MySQL manually
mysqld
```

### Start Backend Server

From the project root:

```bash
# Using Maven wrapper (Windows)
mvnw spring-boot:run

# Or using system Maven
mvn spring-boot:run
```

The backend will start on `http://localhost:8080`

### Start Frontend Development Server

From the project root:

```bash
cd frontend
npm start
cd ..
```

The frontend will start on `http://localhost:3000` (opens automatically in your browser)

### Building for Production

#### Backend
```bash
mvn clean package
# JAR file created in target/IndiChess-0.0.1-SNAPSHOT.jar
```

#### Frontend
```bash
cd frontend
npm run build
# Build output created in frontend/build/
```

---

## API Documentation

### Authentication Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Register new user |
| POST | `/api/auth/login` | User login |
| POST | `/api/auth/oauth2/google` | Google OAuth callback |
| POST | `/api/auth/oauth2/github` | GitHub OAuth callback |

### Game Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/matches` | Get all matches |
| POST | `/api/matches` | Create new match |
| GET | `/api/matches/{id}` | Get match details |
| PUT | `/api/matches/{id}` | Update match |

### WebSocket Endpoints

- `/ws/game` - Game move and state updates
- `/ws/chat` - Real-time chat messages

---

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines

- Follow Java coding conventions for backend code
- Follow React best practices for frontend code
- Write unit tests for new features
- Update documentation for API changes
- Use meaningful commit messages

---

## Troubleshooting

### Common Issues

**Port Already in Use**
```bash
# Find and kill process using port 8080 (backend)
netstat -ano | findstr :8080
taskkill /PID <PID> /F

# For port 3000 (frontend), use similar commands
```

**MySQL Connection Error**
- Ensure MySQL service is running
- Verify credentials in `application.properties`
- Check database name matches configuration

**Node Modules Issues**
```bash
cd frontend
rm -r node_modules package-lock.json
npm install
```

**WebSocket Connection Issues**
- Ensure WebSocket URLs match your deployment environment
- Check firewall settings allow WebSocket connections
- Verify Spring WebSocket configuration in SecurityConfig

---

## License

This project is currently under development. Please contact the repository owner for licensing information.

---

## Contact & Support

- **Repository**: [github.com/govindsingh3/indichessfullstack](https://github.com/govindsingh3/indichessfullstack)
- **Issues**: Use GitHub Issues for bug reports and feature requests

---

**Last Updated**: January 2026
