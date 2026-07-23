<div align="center">

# WorkAdda

### Job Discovery & Networking Platform for Developers

[![Node.js](https://img.shields.io/badge/Node.js-20-339933?style=flat-square&logo=node.js)](https://nodejs.org/)
[![Express.js](https://img.shields.io/badge/Express.js-4.19-000000?style=flat-square)](https://expressjs.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-8-47A248?style=flat-square&logo=mongodb)](https://www.mongodb.com/)
[![EJS](https://img.shields.io/badge/EJS-3.1-A91E50?style=flat-square)](https://ejs.co/)
[![Passport.js](https://img.shields.io/badge/Passport.js-0.7-34A853?style=flat-square)](https://www.passportjs.org/)
[![Bootstrap](https://img.shields.io/badge/Bootstrap-3.4-7952B3?style=flat-square&logo=bootstrap)](https://getbootstrap.com/)

**WorkAdda** is a full-stack web platform that connects developers with job opportunities, notes, and study resources. Built with the MVC pattern using Express.js, MongoDB, and EJS templating.

[Report Bug](https://github.com/harshity322-cpu/WorkAdda/issues) &nbsp;|&nbsp; [Request Feature](https://github.com/harshity322-cpu/WorkAdda/issues)

</div>

---

## Table of Contents

- [About](#about)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [API Routes](#api-routes)
- [Environment Variables](#environment-variables)
- [Author](#author)
- [License](#license)

---

## About

WorkAdda is a collaborative learning and job discovery platform built as a full-stack project. It allows users to:

- Share and discover **study notes** organized by programs and subjects
- Upload files with **Cloudinary** integration
- Leave **reviews and ratings** on content
- Manage content with **authorization** (only owners can edit/delete)
- Authenticate securely with **Passport.js** and session management

The project follows the **MVC (Model-View-Controller)** architecture with proper middleware, validation, and error handling.

---

## Features

| Feature | Description |
|---------|-------------|
| **User Authentication** | Register & login with Passport.js + express-session |
| **Session Management** | Persistent sessions stored in MongoDB via connect-mongo |
| **Notes System** | Create, read, update, and share study notes |
| **Program Management** | Organize content under academic programs |
| **Subject Management** | Categorize notes by subjects within programs |
| **File Uploads** | Upload images via Multer → Cloudinary |
| **Reviews & Ratings** | 5-star rating system with comments |
| **Authorization** | Owner-only edit/delete with middleware protection |
| **Input Validation** | Joi schema validation for all forms |
| **Flash Messages** | Success/error feedback for user actions |
| **Responsive UI** | Mobile-friendly design with custom CSS |
| **Error Handling** | Custom ExpressError class with proper HTTP codes |

---

## Tech Stack

| Category | Technology |
|----------|-----------|
| Runtime | Node.js 20 |
| Framework | Express.js 4.19 |
| Database | MongoDB + Mongoose 8 |
| Templating | EJS + ejs-mate |
| Authentication | Passport.js + passport-local-mongoose |
| Session Store | connect-mongo (MongoDB) |
| Validation | Joi |
| File Upload | Multer + Multer-Storage-Cloudinary |
| Cloud Storage | Cloudinary |
| Styling | Custom CSS + Bootstrap 3.4 |
| HTTP Methods | method-override (PUT/DELETE via forms) |

---

## Project Structure

```
WorkAdda/
├── app.js                      # Express app entry point
├── package.json
├── .env.example                # Environment variable template
├── Schema.js                   # Joi validation schemas
├── middleware.js                # Auth, validation & ownership middleware
├── cloudinaryConfigure.js      # Cloudinary + Multer config
│
├── models/                     # Mongoose Models
│   ├── user.js                 # User schema (Passport local)
│   ├── List.js                 # Notes schema
│   ├── Program.js              # Program schema
│   ├── Subject.js              # Subject schema
│   └── Review.js               # Review schema
│
├── routes/                     # Express Routers
│   ├── user.js                 # Auth routes (signup, login, logout)
│   ├── List.js                 # Notes CRUD routes
│   ├── Program.js              # Program CRUD routes
│   ├── Subject.js              # Subject CRUD routes
│   └── Review.js               # Review routes
│
├── views/                      # EJS Templates
│   ├── layouts/
│   │   ├── boilerplate.ejs     # Base layout
│   │   └── navbar.ejs          # Navigation bar
│   ├── includes/
│   │   └── flash.ejs           # Flash message partial
│   ├── users/
│   │   ├── signup.ejs
│   │   └── login.ejs
│   ├── Notes/
│   │   └── Home.ejs
│   ├── Program/
│   │   ├── index.ejs
│   │   ├── new.ejs
│   │   ├── show.ejs
│   │   └── edit.ejs
│   └── Subject/
│       ├── index.ejs
│       ├── new.ejs
│       ├── show.ejs
│       └── edit.ejs
│
├── public/                     # Static Assets
│   ├── css/
│   │   ├── main.css
│   │   ├── navbar.css
│   │   ├── index.css
│   │   ├── show.css
│   │   ├── edit.css
│   │   ├── login.css
│   │   ├── add-post.css
│   │   ├── flash.css
│   │   ├── rating.css
│   │   └── all.css
│   └── js/
│       └── flash.js
│
└── init/                       # Database Seed Data
    ├── index.js
    ├── data.js
    └── data2.js
```

---

## Getting Started

### Prerequisites

- **Node.js** v20 or higher
- **MongoDB** (local or MongoDB Atlas)
- **Cloudinary** account (for image uploads)

### Installation

1. **Clone the repository**

```bash
git clone https://github.com/harshity322-cpu/WorkAdda.git
cd WorkAdda
```

2. **Install dependencies**

```bash
npm install
```

3. **Set up environment variables**

```bash
cp .env.example .env
```

Edit `.env` with your actual credentials.

4. **Start the server**

```bash
npm start
```

Or with nodemon (if installed globally):

```bash
npx nodemon app.js
```

5. **Open in browser**

```
http://localhost:8080
```

---

## API Routes

### Authentication

| Method | Route | Description |
|--------|-------|-------------|
| `GET` | `/signup` | Show signup form |
| `POST` | `/signup` | Register new user |
| `GET` | `/login` | Show login form |
| `POST` | `/login` | Authenticate user |
| `GET` | `/logout` | Destroy session & logout |

### Notes

| Method | Route | Description |
|--------|-------|-------------|
| `GET` | `/Notes` | List all notes |
| `POST` | `/Notes` | Create new note (auth required) |
| `GET` | `/Notes/:id` | View single note |
| `PUT` | `/Notes/:id` | Update note (owner only) |
| `DELETE` | `/Notes/:id` | Delete note (owner only) |

### Programs

| Method | Route | Description |
|--------|-------|-------------|
| `GET` | `/Program` | List all programs |
| `GET` | `/Program/new` | New program form (auth) |
| `POST` | `/Program` | Create program (auth + validation) |
| `GET` | `/Program/:id` | View program details |
| `GET` | `/Program/:id/edit` | Edit form (owner only) |
| `PUT` | `/Program/:id` | Update program (owner only) |
| `DELETE` | `/Program/:id` | Delete program (owner only) |

### Subjects

| Method | Route | Description |
|--------|-------|-------------|
| `GET` | `/Subject` | List all subjects |
| `GET` | `/Subject/new` | New subject form (auth) |
| `POST` | `/Subject` | Create subject (auth + validation) |
| `GET` | `/Subject/:id` | View subject details |
| `GET` | `/Subject/:id/edit` | Edit form (owner only) |
| `PUT` | `/Subject/:id` | Update subject (owner only) |
| `DELETE` | `/Subject/:id` | Delete subject (owner only) |

### Reviews

| Method | Route | Description |
|--------|-------|-------------|
| `POST` | `/:id/reviews` | Add review (auth + validation) |
| `DELETE` | `/:id/reviews/:reviewId` | Delete review (author only) |

---

## Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `ATLAS_URL` | MongoDB connection string | `mongodb+srv://user:pass@cluster.mongodb.net/db` |
| `CLOUD_NAME` | Cloudinary cloud name | `your_cloud_name` |
| `CLOUD_API_KEY` | Cloudinary API key | `1234567890` |
| `CLOUD_API_SECRET` | Cloudinary API secret | `your_api_secret` |
| `SECRET` | Session secret key | `your-super-secret-key` |

---

## Middleware

The project uses custom middleware for:

- **`isLoggedIn`** — Checks if user is authenticated
- **`saveRedirectUrl`** — Saves original URL for post-login redirect
- **`validateProgram`** — Joi validation for program data
- **`validateSubject`** — Joi validation for subject data
- **`validateReview`** — Joi validation for review data
- **`isProgramOwner`** — Checks if current user owns the program
- **`isSubjectOwner`** — Checks if current user owns the subject
- **`isProgramReviewAuthor`** — Checks if user wrote the review
- **`isSubjectReviewAuthor`** — Checks if user wrote the review

---

## Author

**Harshit Yadav**

- GitHub: [@harshity322-cpu](https://github.com/harshity322-cpu)
- Email: [harshity322@gmail.com](mailto:harshity322@gmail.com)

---

## License

Distributed under the MIT License. See `LICENSE` for more information.

---

<div align="center">

**Built with passion by Harshit Yadav**

</div>
