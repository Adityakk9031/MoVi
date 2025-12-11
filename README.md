# 🎬 MoVi 

A full-stack streaming application built with **Flutter** (cross-platform frontend) and **Node.js/Express** (backend), featuring user authentication, movie browsing, TV show recommendations, and search functionality.

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Screenshots](#screenshots)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Project Structure](#project-structure)
- [Installation & Setup](#installation--setup)
- [API Documentation](#api-documentation)
- [Features](#features)
- [Authentication Flow](#authentication-flow)
- [Database Schema](#database-schema)
- [Development](#development)

---

## 🎯 Project Overview

MoVi is a Netflix-inspired streaming application that demonstrates modern mobile and backend development practices. It integrates with **TMDB API** to fetch real movie and TV show data, providing users with:

- User authentication (signup/signin)
- Browse trending movies and TV shows
- Get recommendations based on content
- Search functionality for movies and shows
- Watch trailers via YouTube
- Responsive UI across all platforms (iOS, Android, Web, macOS, Linux, Windows)

---

## 📸 Screenshots

### App UI Screenshots

| Screenshot 1 | Screenshot 2 | Screenshot 3 |
|:---:|:---:|:---:|
| ![Image 1](https://raw.githubusercontent.com/Adityakk9031/MoVi/f28b12d565a93d9b20a3fed366725c1d87ec698c/IMAGE1.jpeg) | ![Image 2](https://raw.githubusercontent.com/Adityakk9031/MoVi/f28b12d565a93d9b20a3fed366725c1d87ec698c/IMAGE2.jpeg) | ![Image 3](https://raw.githubusercontent.com/Adityakk9031/MoVi/f28b12d565a93d9b20a3fed366725c1d87ec698c/IMAGE3.jpeg) |
| ![Image 4](https://raw.githubusercontent.com/Adityakk9031/MoVi/f28b12d565a93d9b20a3fed366725c1d87ec698c/IMAGE4.jpeg) | ![Image 5](https://raw.githubusercontent.com/Adityakk9031/MoVi/f28b12d565a93d9b20a3fed366725c1d87ec698c/IMAGE5.jpeg) | ![Image 6](https://raw.githubusercontent.com/Adityakk9031/MoVi/f28b12d565a93d9b20a3fed366725c1d87ec698c/IMAGE6.jpeg) |
| ![Image 7](https://raw.githubusercontent.com/Adityakk9031/MoVi/f28b12d565a93d9b20a3fed366725c1d87ec698c/IMAGE7.jpeg) | ![Image 8](https://raw.githubusercontent.com/Adityakk9031/MoVi/f28b12d565a93d9b20a3fed366725c1d87ec698c/IMAGE8.jpeg) | ![Image 9](https://raw.githubusercontent.com/Adityakk9031/MoVi/f28b12d565a93d9b20a3fed366725c1d87ec698c/IMAGE9.jpeg) |
| ![Image 10](https://raw.githubusercontent.com/Adityakk9031/MoVi/f28b12d565a93d9b20a3fed366725c1d87ec698c/IMAGE10.jpeg) | ![Image 11](https://raw.githubusercontent.com/Adityakk9031/MoVi/f28b12d565a93d9b20a3fed366725c1d87ec698c/IMAGE11.jpeg) | ![Image 12](https://raw.githubusercontent.com/Adityakk9031/MoVi/f28b12d565a93d9b20a3fed366725c1d87ec698c/IMAGE12.jpeg) |
| ![Image 13](https://raw.githubusercontent.com/Adityakk9031/MoVi/f28b12d565a93d9b20a3fed366725c1d87ec698c/IMAGE13.jpeg) | ![Image 14](https://raw.githubusercontent.com/Adityakk9031/MoVi/f28b12d565a93d9b20a3fed366725c1d87ec698c/IMAGE14.jpeg) | |

---

## 🛠 Tech Stack

### Frontend (Flutter)
| Technology | Purpose |
|-----------|---------|
| **Flutter 3.4.3+** | Cross-platform mobile framework |
| **BLoC/Cubit** | State management |
| **Dio** | HTTP client with interceptors |
| **GetIt** | Dependency injection |
| **flutter_svg** | SVG asset rendering |
| **youtube_player_flutter** | Video playback |
| **fan_carousel_image_slider** | Image carousel |
| **shared_preferences** | Local data storage |
| **reactive_button** | UI component |

### Backend (Node.js)
| Technology | Purpose |
|-----------|---------|
| **Express.js** | Web server framework |
| **MongoDB + Mongoose** | NoSQL database |
| **JWT** | Token-based authentication |
| **bcryptjs** | Password hashing |
| **axios** | HTTP requests to TMDB API |
| **cookie-parser** | Cookie middleware |
| **nodemon** | Development server auto-reload |

### External APIs
- **TMDB API** - Movie and TV show data

---

## 🏗 Architecture

### Clean Architecture + SOLID Principles

The application follows **Clean Architecture** with clear separation of concerns:

```
┌─────────────────────────────────────┐
│     PRESENTATION LAYER (UI)         │
│  (Screens, Widgets, BLoC/Cubit)     │
└────────────────┬────────────────────┘
                 ↓
┌─────────────────────────────────────┐
│     DOMAIN LAYER (Business Logic)   │
│  (UseCases, Entities, Repositories) │
└────────────────┬────────────────────┘
                 ↓
┌─────────────────────────────────────┐
│      DATA LAYER (Data Sources)      │
│  (API Services, Local Storage)      │
└─────────────────────────────────────┘
```

### Design Patterns Used
- **BLoC Pattern** - State management
- **Repository Pattern** - Data abstraction
- **Dependency Injection** - Using GetIt
- **Singleton Pattern** - Service instances
- **Observer Pattern** - Stream-based updates

---

## 📁 Project Structure

### Frontend: `lib/`

```
lib/
├── main.dart                          # Application entry point
├── service_locator.dart               # Dependency injection setup (GetIt)
│
├── presentation/                      # UI & State Management
│   ├── splash/                        # Splash/Loading screen
│   ├── auth/                          # Login & Signup screens
│   ├── home/                          # Main content screen
│   ├── search/                        # Search functionality
│   └── watch/                         # Movie/Show details
│
├── domain/                            # Business Logic Layer
│   ├── auth/
│   │   ├── repositories/              # Auth repository interface
│   │   └── usecases/                  # SignUp, SignIn, IsLoggedIn
│   ├── movie/
│   │   ├── repositories/              # Movie repository interface
│   │   └── usecases/
│   │       ├── get_trending_movies.dart
│   │       ├── get_now_playing_movies.dart
│   │       ├── get_recommendation_movies.dart
│   │       ├── get_similar_movies.dart
│   │       ├── get_movie_trailer.dart
│   │       └── search_movie.dart
│   └── tv/
│       ├── repositories/              # TV repository interface
│       └── usecases/
│           ├── get_popular_tv.dart
│           ├── get_recommendation_tvs.dart
│           ├── get_similar_tvs.dart
│           ├── get_keywords.dart
│           └── search_tv.dart
│
├── data/                              # Data & API Layer
│   ├── auth/
│   │   ├── sources/                   # AuthApiService
│   │   │   └── auth_api_service.dart
│   │   └── repositories/              # AuthRepositoryImpl
│   │       └── auth.dart
│   ├── movie/
│   │   ├── sources/                   # MovieApiService
│   │   │   └── movie.dart
│   │   └── repositories/              # MovieRepositoryImpl
│   │       └── movie.dart
│   └── tv/
│       ├── sources/                   # TVApiService
│       │   └── tv.dart
│       └── repositories/              # TVRepositoryImpl
│           └── tv.dart
│
├── core/                              # Core & Utilities
│   ├── configs/
│   │   └── theme/                     # App theming (AppTheme)
│   ├── constants/
│   │   └── api_url.dart               # API endpoints
│   ├── entity/                        # Domain models
│   ├── models/                        # Data models (from API)
│   ├── network/
│   │   ├── dio_client.dart            # DioClient instance
│   │   └── interceptors.dart          # Auth & Logger interceptors
│   └── usecase/                       # Base UseCase class
│
└── common/                            # Shared Components
    ├── bloc/                          # Shared BLoC logic
    ├── helper/                        # Helper functions
    └── widgets/                       # Reusable widgets
```

### Backend: `Backend/backend/`

```
backend/
├── server.js                          # Express server setup
│
├── config/
│   ├── db.js                          # MongoDB connection
│   └── envVars.js                     # Environment variable loader
│
├── models/
│   └── user.model.js                  # MongoDB User schema
│
├── controllers/                       # Business Logic
│   ├── auth.controller.js             # Signup, Login, Logout, AuthCheck
│   ├── movie.controller.js            # Movie endpoints
│   ├── tv.controller.js               # TV show endpoints
│   └── search.controller.js           # Search endpoints
│
├── routes/                            # API Routes
│   ├── auth.route.js                  # /api/v1/auth/*
│   ├── movie.route.js                 # /api/v1/movie/*
│   ├── tv.route.js                    # /api/v1/tv/*
│   └── search.route.js                # /api/v1/search/*
│
├── middleware/
│   └── protectRoute.js                # JWT verification middleware
│
├── services/                          # External API calls
│   └── (calls to TMDB API via axios)
│
└── utils/
    └── generateToken.js               # JWT token generation & cookie setup
```

---

## 🚀 Installation & Setup

### Prerequisites
- **Node.js** 16+ and npm/yarn
- **Flutter** 3.4.3+
- **MongoDB** running locally or MongoDB Atlas URI
- **TMDB API Key** from [themoviedb.org](https://www.themoviedb.org/settings/api)
- **Git**

### Backend Setup

1. **Navigate to backend directory:**
   ```bash
   cd Backend
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Create `.env` file in `Backend/` directory:**
   ```env
   PORT=5000
   MONGO_URI=mongodb://localhost:27017/netflix
   NODE_ENV=development
   JWT_SECRET=your_jwt_secret_key_here
   TMDB_API_KEY=your_tmdb_api_key_here
   ```

4. **Start development server:**
   ```bash
   npm run dev
   ```
   Server runs on `http://localhost:5000`

### Frontend Setup

1. **Navigate to project root:**
   ```bash
   cd MoVi
   ```

2. **Install Flutter dependencies:**
   ```bash
   flutter pub get
   ```

3. **Update API URL in `lib/core/constants/api_url.dart`:**
   ```dart
   class ApiUrl {
     static const String baseURL = 'http://localhost:5000/api/v1';
   }
   ```

4. **Run the application:**
   ```bash
   # iOS
   flutter run -d iphone
   
   # Android
   flutter run -d android
   
   # Web
   flutter run -d chrome
   
   # macOS
   flutter run -d macos
   
   # Windows
   flutter run -d windows
   ```

---

## 📡 API Documentation

### Base URL
```
http://localhost:5000/api/v1
```

### Authentication Endpoints

#### **POST** `/auth/signup`
Register a new user.

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "password123"
}
```

**Response (Success):**
```json
{
  "success": true,
  "user": {
    "_id": "user_id",
    "email": "user@example.com",
    "image": "/avatar1.png",
    "token": "jwt_token"
  }
}
```

**Validations:**
- Email format validation
- Password minimum 6 characters
- Email uniqueness check

---

#### **POST** `/auth/signin`
Login with email and password.

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "password123"
}
```

**Response (Success):**
```json
{
  "success": true,
  "user": {
    "_id": "user_id",
    "email": "user@example.com",
    "image": "/avatar1.png",
    "token": "jwt_token"
  }
}
```

---

#### **POST** `/auth/logout`
Logout user and clear JWT cookie.

**Headers:**
```
Authorization: Bearer <jwt_token>
```

**Response:**
```json
{
  "success": true,
  "message": "Logged out successfully"
}
```

---

#### **GET** `/auth/authCheck` ✅ *Protected Route*
Verify if user is authenticated.

**Headers:**
```
Authorization: Bearer <jwt_token>
```

**Response:**
```json
{
  "success": true,
  "user": {
    "_id": "user_id",
    "email": "user@example.com"
  }
}
```

---

### Movie Endpoints (Protected Routes)

#### **GET** `/movie/trending`
Fetch trending movies.

#### **GET** `/movie/now-playing`
Fetch movies currently in theaters.

#### **GET** `/movie/:id`
Get movie details by ID.

#### **GET** `/movie/:id/trailer`
Get YouTube trailer for movie.

#### **GET** `/movie/:id/similar`
Get similar movies.

#### **GET** `/movie/:id/recommendations`
Get movie recommendations.

---

### TV Endpoints (Protected Routes)

#### **GET** `/tv/popular`
Fetch popular TV shows.

#### **GET** `/tv/:id`
Get TV show details.

#### **GET** `/tv/:id/similar`
Get similar TV shows.

#### **GET** `/tv/:id/recommendations`
Get TV show recommendations.

---

### Search Endpoints (Protected Routes)

#### **GET** `/search/movie`
Search for movies.

**Query Parameters:**
- `query`: Search term (string)

#### **GET** `/search/tv`
Search for TV shows.

**Query Parameters:**
- `query`: Search term (string)

---

## ✨ Features

### ✅ Authentication
- User registration with email/password
- Login with validation
- JWT-based authentication
- Logout functionality
- Session persistence

### ✅ Content Browsing
- **Movies:**
  - Trending movies
  - Now playing
  - Similar movies
  - Recommendations
  - Movie trailers (YouTube integration)

- **TV Shows:**
  - Popular shows
  - Similar shows
  - Recommendations
  - Keywords/genres

### ✅ Search
- Full-text search for movies
- Full-text search for TV shows
- Real-time search results

### ✅ User Experience
- Splash screen with app startup logic
- Auto-login if session exists
- Responsive UI for all platforms
- Image carousel for visual content
- Clean, modern design

---

## 🔐 Authentication Flow

```
┌─────────────────────────────────────┐
│   User Opens App                    │
└────────────────┬────────────────────┘
                 ↓
         ┌───────────────┐
         │ Splash Screen │
         └───────┬───────┘
                 ↓
    ┌────────────────────────┐
    │ Check IsLoggedInUseCase│
    │ (Check SharedPref)     │
    └────────────┬───────────┘
                 ↓
        ┌─────────────────┐
        │ Token Valid?    │
        └─┬──────────┬────┘
          │          │
         YES        NO
          │          │
          ↓          ↓
      ┌─────────┐  ┌────────┐
      │ Home    │  │Auth    │
      │Screen   │  │Screen  │
      └─────────┘  └───┬────┘
                       ↓
            ┌──────────────────┐
            │User Signup/Login │
            └────────┬─────────┘
                     ↓
         ┌───────────────────────┐
         │Send Email & Password  │
         │to Backend (/auth/*)   │
         └────────────┬──────────┘
                      ↓
          ┌────────────────────────┐
          │Backend Validates &     │
          │Returns JWT Token       │
          └────────────┬───────────┘
                       ↓
         ┌─────────────────────────────┐
         │Save Token in SharedPrefs    │
         │& Set Cookie in DioClient    │
         └────────────┬────────────────┘
                      ↓
            ┌─────────────────────┐
            │Navigate to Home     │
            └─────────────────────┘
```

---

## 💾 Database Schema

### User Model (MongoDB)

```javascript
{
  _id: ObjectId,
  email: String (required, unique),
  password: String (hashed with bcryptjs, required),
  image: String (random avatar from ["avatar1.png", "avatar2.png", "avatar3.png"]),
  createdAt: Date (default: now),
  updatedAt: Date (default: now)
}
```

**Example Document:**
```json
{
  "_id": "507f1f77bcf86cd799439011",
  "email": "user@example.com",
  "password": "$2a$10$encrypted_password_here",
  "image": "/avatar2.png",
  "createdAt": "2025-12-11T10:30:00Z",
  "updatedAt": "2025-12-11T10:30:00Z"
}
```

---

## 🛠 Development

### Running Backend
```bash
cd Backend
npm run dev  # Starts with nodemon
```

### Running Frontend
```bash
flutter run  # Choose device when prompted
```

### Building for Production

**Backend:**
```bash
cd Backend
npm start
```

**Frontend:**
```bash
# Android
flutter build apk

# iOS
flutter build ios

# Web
flutter build web

# Windows
flutter build windows
```

### Environment Configuration

**Backend `.env` Variables:**
- `PORT` - Server port
- `MONGO_URI` - MongoDB connection string
- `NODE_ENV` - development/production
- `JWT_SECRET` - JWT signing secret
- `TMDB_API_KEY` - TMDB API key

### Code Quality

The project follows:
- Clean Code principles
- SOLID design principles
- Proper error handling
- Input validation
- Security best practices

---

## 🔒 Security Features

✅ **Password Security:**
- Bcryptjs hashing with salt (10 rounds)
- Never stored in plain text

✅ **Authentication:**
- JWT-based token system
- HTTP-only cookies (backend)
- Token expiration

✅ **API Security:**
- Protected routes via JWT middleware
- Input validation & sanitization
- CORS configuration

✅ **Data Protection:**
- Secure password validation
- Email format verification

---

## 📝 Notes

- **TMDB API** provides all movie/TV data (requires API key)
- **MongoDB** stores only user credentials
- **Dio Client** automatically includes JWT in request headers
- **Interceptors** handle auth errors and request logging

---

## 🤝 Contributing

For contributions:
1. Create a feature branch
2. Make your changes
3. Test thoroughly
4. Submit a pull request

---

## 📄 License

This project is licensed under the ISC License.

---

**Made with ❤️ for streaming enthusiasts**
