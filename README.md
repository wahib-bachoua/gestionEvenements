
---

# 🎉 Event Management System (Gestion d'Événements)

> ** web application for club event management with role-based access control**

A comprehensive solution for clubs and organizations to create, manage, and participate in events. The system features separate interfaces for organizers and students with real-time event management capabilities. 

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Architecture](#-architecture)
- [Database Schema](#️-database-schema)
- [Technologies](#️-technologies)
- [Installation](#-installation)
- [Configuration](#️-configuration)
- [Usage](#-usage)
- [API Documentation](#-api-documentation)
- [Project Structure](#-project-structure)
- [Testing](#-testing)
- [Future Roadmap](#️-future-roadmap)

---

## 🎯 Overview

**Event Management System** is a Spring Boot REST API application designed to help clubs and organizations manage their events efficiently. The system provides role-based access control with distinct interfaces for event organizers and participants (students).

### Use Cases

- 🎓 **University Clubs**: Manage workshops, seminars, and social events
- 🏢 **Organizations**: Schedule meetings and conferences
- 🎮 **Gaming Communities**:  Organize tournaments and gaming sessions
- 🔒 **Cybersecurity Groups**: Coordinate training sessions and announcements
- 📚 **Study Groups**: Plan group activities and collaborative events

### Key Highlights

- **Role-_Based Access**:  Separate interfaces for organizers and participants
- **RESTful API**: Clean API design with Spring Boot
- **Real-Time Updates**: Instant event creation and participation
- **Participant Limits**: Control maximum attendance per event
- **Multi-Day Events**: Support for events spanning multiple days

---

## ✨ Features

### For Organizers (Créateur d'événements)

- **📝 Event Management**
  - Create events with detailed information (title, description, dates, location)
  - Set maximum participant limits
  - Upload event images
  - Edit and update event details
  - Delete events
  
- **👥 Participant Tracking**
  - View registered participants for each event
  - Monitor registration counts
  - Manage participant lists

- **📊 Event Dashboard**
  - Overview of all created events
  - Quick access to event statistics
  - Event performance metrics

### For Participants/Students

- **🔍 Event Discovery**
  - Browse all available events
  - Filter events by category or date
  - View detailed event information with images
  
- **🎟️ Event Registration**
  - One-click participation in events
  - View participation history
  - Unregister from events if needed

- **📅 Personal Event Calendar**
  - Track registered events
  - Upcoming events notifications
  - Past events history

### System-Wide Features

- **🔐 User Authentication**
  - Secure registration and login
  - Role-based authorization (ORGANISATEUR/PARTICIPANT)
  - Session management

- **🔔 Notifications System**
  - Event reminders
  - Registration confirmations
  - Event updates and changes

- **📱 Responsive Design**
  - Mobile-friendly interface
  - Cross-browser compatibility
  - Modern UI/UX

---

## 🏛 Architecture

The application follows a **3-tier MVC architecture**:

```
┌─────────────────────┐
│   Frontend Layer    │  (HTML/CSS/JS - Client)
│   (React/Angular)   │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Controller Layer   │  (REST Controllers)
│  (@RestController)  │  - EvenementController
│                     │  - UtilisateurController
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│   Service Layer     │  (Business Logic)
│    (@Service)       │  - EvenementService
│                     │  - UtilisateurService
└──────────┬──────────┘
           │
           ▼
┌──────────��──────────┐
│ Repository Layer    │  (Data Access)
│ (JpaRepository)     │  - EvenementRepository
│                     │  - UtilisateurRepository
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│   Database Layer    │
│   (MySQL - myDb5)   │
└─────────────────────┘
```

---

## 🗄️ Database Schema

### Core Entities

#### **Utilisateur** (Base Entity)
- **Inheritance Strategy**:  JOINED
- Fields: 
  - `id` (PK, Auto-increment)
  - `nom` (Last Name)
  - `prenom` (First Name)
  - `email` (Email Address)
  - `mdp` (Password)
  - `role` (ORGANISATEUR | PARTICIPANT)

#### **Organisateur** (Extends Utilisateur)
- Inherits all Utilisateur fields
- Relationships:
  - One-to-Many with `Evenement`

#### **Participant** (Extends Utilisateur)
- Inherits all Utilisateur fields
- Relationships: 
  - Many-to-Many with `Evenement`

#### **Evenement**
- Fields:
  - `id` (PK, Auto-increment)
  - `titre` (Event Title)
  - `description` (Event Description)
  - `dateDebut` (Start Date)
  - `dateFin` (End Date)
  - `lieu` (Location)
  - `nbrMaxPart` (Maximum Participants)
- Relationships:
  - Many-to-One with `Organisateur`
  - Many-to-Many with `Participant`

#### **Notification**
- Fields:
  - `id` (PK, Auto-increment)
  - `message` (Notification Content)
  - `dateEnvoi` (Send Date)
  - `lu` (Read Status)

### Entity Relationships

```
Utilisateur (JOINED inheritance)
    ├── Organisateur
    │       └── Events (1:N)
    └── Participant
            └── Events (M:N)

Evenement
    ├── Organisateur (N:1)
    └── Participants (M:N)
```

---

## 🛠️ Technologies

### Backend

- **Spring Boot 3.4.0** - Application framework
- **Spring Data JPA** - Data persistence
- **Spring Web** - REST API
- **Hibernate** - ORM implementation
- **MySQL Connector/J** - Database driver

### Database

- **MySQL 8.1.25** - Relational database (via XAMPP)
- **JPA/Hibernate** - ORM layer

### Build Tools

- **Maven** - Dependency management
- **Java 23** - Programming language

### Development Tools

- **Lombok** - Boilerplate code reduction
- **Spring DevTools** - Hot reload during development

### Frontend (Not in repository)

- **HTML5/CSS3** - Markup and styling
- **JavaScript** - Client-side logic
- **Bootstrap** (assumed) - UI framework

---

## 📥 Installation

### Prerequisites

- **Java JDK 23** or higher
- **Maven 3.6+** (or use included Maven wrapper)
- **MySQL 8.0+** (XAMPP recommended for Windows)
- **Git**

### Step 1: Clone the Repository

```bash
git clone https://github.com/wahib-bachoua/gestionEvenements. git
cd gestionEvenements
```

### Step 2: Install XAMPP (if not already installed)

**For Windows:**

1. Download XAMPP 8.1.25+ from [https://www.apachefriends.org](https://www.apachefriends.org)
2. Install XAMPP to `C:\xampp`
3. Launch XAMPP Control Panel
4. Start **Apache** and **MySQL** modules

**For macOS/Linux:**

Alternatively, install MySQL standalone: 

```bash
# macOS
brew install mysql
brew services start mysql

# Ubuntu/Debian
sudo apt update
sudo apt install mysql-server
sudo systemctl start mysql
```

### Step 3: Configure MySQL Database

```bash
# Access MySQL through XAMPP or terminal
mysql -u root -p

# Create database (or let Spring Boot create it automatically)
CREATE DATABASE myDb5;

# Exit MySQL
exit;
```

**Note**: The application is configured with `createDatabaseIfNotExist=true`, so the database will be created automatically if it doesn't exist.

### Step 4: Configure Application Properties

Edit `src/main/resources/application.properties` if needed:

```properties
spring.application.name=gestionEvenements3
spring.datasource.url=jdbc:mysql://localhost:3306/myDb5?createDatabaseIfNotExist=true&useSSL=false&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=
spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=update
server.port=8081
```

**Important**: If your MySQL has a password, update the `spring.datasource.password` property.

### Step 5: Build and Run

#### Using Maven Wrapper (Recommended)

```bash
# Windows
mvnw. cmd clean install
mvnw.cmd spring-boot:run

# macOS/Linux
./mvnw clean install
./mvnw spring-boot:run
```

#### Using System Maven

```bash
mvn clean install
mvn spring-boot:run
```

The application will start on **http://localhost:8081**

---

## ⚙️ Configuration

### Database Configuration

The application uses MySQL with automatic schema generation:

- **DDL Mode**: `update` - Updates schema without dropping existing data
- **SQL Logging**:  Enabled via `spring.jpa.show-sql=true`
- **Auto Database Creation**: Enabled

### Server Configuration

- **Port**: `8081` (default)
- **Context Path**:  `/` (root)

### Environment Variables (Optional)

You can override properties using environment variables:

```bash
# Example
export SPRING_DATASOURCE_URL=jdbc:mysql://localhost:3306/myDb5
export SPRING_DATASOURCE_USERNAME=root
export SPRING_DATASOURCE_PASSWORD=yourpassword
export SERVER_PORT=8081
```

---

## 🚀 Usage

### Starting the Application

1. **Start MySQL** (via XAMPP or standalone)
2. **Run the Spring Boot application**: 
   ```bash
   ./mvnw spring-boot:run
   ```
3. **Access the application**:  http://localhost:8081

### Organizer Workflow

1. **Register/Login** as an organizer
   - Select role: "ORGANISATEUR"
   
2. **Create an Event**
   - Navigate to event creation form
   - Fill in event details: 
     - Event name (e.g., "GAMING-POLE")
     - Description
     - Start and end dates
     - Location
     - Maximum participants
     - Upload event image
   - Click "Créer un événement"

3. **Manage Events**
   - View all your created events
   - Edit event details
   - Delete events
   - View registered participants

4. **Monitor Participation**
   - Check registration counts
   - View participant lists
   - Track event popularity

### Participant/Student Workflow

1. **Register/Login** as a participant
   - Select role: "PARTICIPANT"
   
2. **Browse Available Events**
   - View all upcoming events
   - See event details: 
     - Title and description
     - Date and location
     - Available spots
     - Event image

3. **Participate in Events**
   - Click "Participate" button on desired event
   - Receive confirmation notification
   - Event appears in "My Events"

4. **Manage Participation**
   - View registered events
   - Unregister from events if needed
   - Check upcoming events

---

## 📡 API Documentation

### Base URL

```
http://localhost:8081/api
```

### User Endpoints

#### Get All Users
```http
GET /api/utilisateurs
```

**Response:**
```json
[
  {
    "id": 1,
    "nom": "Dupont",
    "prenom":  "Jean",
    "email":  "jean.dupont@example. com",
    "role": "ORGANISATEUR"
  }
]
```

#### Create User
```http
POST /api/utilisateurs
Content-Type:  application/json

{
  "nom": "Martin",
  "prenom": "Sophie",
  "email": "sophie.martin@example.com",
  "mdp": "password123",
  "role": "PARTICIPANT"
}
```

#### Delete User
```http
DELETE /api/utilisateurs/{id}
```

### Event Endpoints

#### Get All Events
```http
GET /api/evenements
```

**Response:**
```json
[
  {
    "id": 1,
    "titre": "GAMING-POLE",
    "description": "Plongez dans le gaming ! ",
    "dateDebut":  "2025-11-23",
    "dateFin":  "2025-11-25",
    "lieu": "Salle de Party",
    "nbrMaxPart": 50,
    "organisateur": {
      "id": 1,
      "nom": "Dupont",
      "prenom": "Jean"
    },
    "participants": []
  }
]
```

#### Create Event
```http
POST /api/evenements
Content-Type: application/json

{
  "titre": "Android Studio Workshop",
  "description": "Découvrez les bases de la création d'applications Android",
  "dateDebut": "2025-11-20",
  "dateFin":  "2025-11-22",
  "lieu": "Amphi Tech Lab",
  "nbrMaxPart": 30,
  "organisateur": {
    "id": 1
  }
}
```

#### Delete Event
```http
DELETE /api/evenements/{id}
```

### Common Response Codes

- `200 OK` - Successful GET request
- `201 Created` - Successful POST request
- `204 No Content` - Successful DELETE request
- `400 Bad Request` - Invalid input
- `404 Not Found` - Resource not found
- `500 Internal Server Error` - Server error

---

## 📁 Project Structure

```
gestionEvenements/
│
├── src/
│   ├── main/
│   │   ├── java/com/example/gestionevenements3/
│   │   │   ├── GestionEvenements3Application.java    # Main application class
│   │   │   │
│   │   │   ├── controllers/                          # REST Controllers
│   │   │   │   ├── EvenementController.java          # Event endpoints
│   │   │   │   └── UtilisateurController.java        # User endpoints
│   │   │   │
│   │   │   ├── models/                               # JPA Entities
│   │   │   │   ├── Utilisateur.java                  # Base user entity
│   │   │   │   ├── Organisateur.java                 # Organizer entity
│   │   │   │   ├── Participant.java                  # Participant entity
│   │   │   │   ├── Evenement.java                    # Event entity
│   │   │   │   └── Notification.java                 # Notification entity
│   │   │   │
│   │   │   ├── repositories/                         # JPA Repositories
│   │   │   │   ├── EvenementRepository.java
│   │   │   │   ├── UtilisateurRepository.java
│   │   │   │   ├── OrganisateurRepository.java
│   │   │   │   ├── ParticipantRepository.java
│   │   │   │   └── NotificationRepository.java
│   │   │   │
│   │   │   └── services/                             # Business Logic
│   │   │       ├── EvenementService.java
│   │   │       └── UtilisateurService.java
│   │   │
│   │   └── resources/
│   │       ├── application.properties                # App configuration
│   │       ├── static/                               # Static resources (CSS, JS, images)
│   │       └── templates/                            # HTML templates (if using Thymeleaf)
│   │
│   └── test/                                         # Test classes
│       └── java/com/example/gestionevenements3/
│
├── . mvn/                                             # Maven wrapper files
├── mvnw                                              # Maven wrapper script (Unix)
├── mvnw.cmd                                          # Maven wrapper script (Windows)
├── pom.xml                                           # Maven dependencies
├── . gitignore                                        # Git ignore rules
└── README.md                                         # This file
```

---

## 🧪 Testing

### Running Unit Tests

```bash
# Using Maven wrapper
./mvnw test

# Using system Maven
mvn test
```

### Testing API Endpoints

#### Using cURL

**Get all events:**
```bash
curl -X GET http://localhost:8081/api/evenements
```

**Create a new user:**
```bash
curl -X POST http://localhost:8081/api/utilisateurs \
  -H "Content-Type: application/json" \
  -d '{
    "nom": "Test",
    "prenom": "User",
    "email": "test@example.com",
    "mdp": "password123",
    "role": "PARTICIPANT"
  }'
```

**Create a new event:**
```bash
curl -X POST http://localhost:8081/api/evenements \
  -H "Content-Type:  application/json" \
  -d '{
    "titre": "Test Event",
    "description":  "A test event",
    "dateDebut": "2025-12-01",
    "dateFin": "2025-12-02",
    "lieu": "Test Location",
    "nbrMaxPart": 25
  }'
```

#### Using Postman

1. Import the API endpoints into Postman
2. Test each endpoint with sample data
3. Verify responses and status codes

### Database Testing

```bash
# Connect to MySQL
mysql -u root -p

# Use the database
USE myDb5;

# Check tables
SHOW TABLES;

# View events
SELECT * FROM evenement;

# View users
SELECT * FROM utilisateur;
```

---

## 🎓 Academic Context

This project was developed as part of an academic curriculum to demonstrate: 

- **Spring Boot Application Development**: RESTful API design and implementation
- **Object-Relational Mapping (ORM)**: Using JPA/Hibernate with MySQL
- **MVC Architecture**:  Separation of concerns in web applications
- **Database Design**: Entity relationships and inheritance strategies
- **RESTful Principles**: Proper HTTP methods and status codes
- **Version Control**: Git and GitHub workflows

### Learning Objectives Achieved

- ✅ Building enterprise-grade REST APIs with Spring Boot
- ✅ Implementing role-based access control
- ✅ Database schema design with inheritance
- ✅ CRUD operations with Spring Data JPA
- ✅ Dependency injection and inversion of control
- ✅ Service-oriented architecture

---

## 🗺️ Future Roadmap

### Short Term (v1.1)

- [ ] **User Authentication & Security**
  - JWT token-based authentication
  - Spring Security integration
  - Password encryption with BCrypt
  - Role-based authorization

- [ ] **Event Image Upload**
  - File upload functionality
  - Image storage and retrieval
  - Thumbnail generation

- [ ] **Pagination & Filtering**
  - Paginated event lists
  - Search functionality
  - Filter by date, location, category

### Medium Term (v1.5)

- [ ] **Email Notifications**
  - Event registration confirmations
  - Event reminders (24h before)
  - Event updates and cancellations

- [ ] **Advanced Event Management**
  - Event categories/tags
  - Recurring events
  - Waitlist for full events
  - QR code for event check-in

- [ ] **User Profile Management**
  - Profile pictures
  - User preferences
  - Event participation history
  - Badges and achievements

### Long Term (v2.0)

- [ ] **Frontend Application**
  - React. js SPA
  - Real-time updates with WebSockets
  - Progressive Web App (PWA)
  - Mobile-responsive design

- [ ] **Analytics & Reporting**
  - Event statistics dashboard
  - Participant demographics
  - Popular events trends
  - Export reports (PDF, CSV)

- [ ] **Social Features**
  - Event comments and ratings
  - Share events on social media
  - Friend system
  - Event recommendations

- [ ] **Multi-tenancy**
  - Support multiple organizations
  - Organization-specific branding
  - Separate event catalogs

- [ ] **Integration & API**
  - Calendar integration (Google Calendar, Outlook)
  - Payment gateway (Stripe, PayPal)
  - OpenAPI/Swagger documentation
  - Webhooks for external integrations

---

## 📄 License

This project is developed for educational purposes.  Feel free to use it as a learning resource or starting point for your own event management system.

---


## 📞 Support

If you encounter any issues or have questions: 

1. Check the [Issues](https://github.com/wahib-bachoua/gestionEvenements/issues) page
2. Create a new issue with detailed description
3. Contact via GitHub

---

**⭐ If you find this project helpful, please give it a star!  ⭐**

Made with ❤️ for learning and development

---
