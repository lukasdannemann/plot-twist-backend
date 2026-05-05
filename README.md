# Plot Twist – Backend

REST API for Plot Twist, a neighborhood plant-swap platform that lets users list houseplants they want to give away and trade them with neighbors. Built with Node.js, Express and MongoDB.

**Live app:** https://plot-twist-fe.vercel.app
**API base URL:** https://webbshop-2026-be-sigma.vercel.app

---

## About the project

This was the final project for the Backend 1 course of my Fullstack Web Development education at Nackademin. We were a team of five – three backend developers (myself included) and two frontend developers – who built the entire app in three weeks using Scrum.

The idea behind Plot Twist is simple: instead of throwing away cuttings or duplicate plants, users can post them and offer them up to neighbors. Other users can request a trade, agree on a meeting time and place, and complete the exchange. Once a trade is done, both users see it in their history.

## Tech stack

- **Runtime:** Node.js (≥20)
- **Framework:** Express 4
- **Database:** MongoDB with Mongoose
- **Auth:** JWT with separate access and refresh tokens, bcrypt for password hashing
- **Image uploads:** Cloudinary via multer
- **Validation:** express-validator
- **Rate limiting:** express-rate-limit
- **Testing:** Vitest + mongodb-memory-server + Supertest
- **Deployment:** Vercel

## My contributions

I worked across the backend with two teammates, but the parts I was mainly responsible for were:

- **Auth and token system** – registration, login, password hashing with bcrypt, and a dual-token JWT setup with access tokens and refresh tokens (`/auth/refresh`)
- **Product model and routes** - built the mongoose schema for products, database functions and all routes for products


## Project structure

```
src/
├── config/        # DB and Cloudinary configuration
├── db/            # Data-access layer (Mongoose queries)
├── middleware/    # Auth, validation, rate limiting
├── models/        # Mongoose schemas
├── routes/        # Express routers (auth, products, trades, me)
├── scripts/       # Database seeding
├── utils/         # Token helpers
├── app.js         # Express app setup
└── server.js      # Entry point
```

## API endpoints

| Method | Endpoint                  | Auth     | Description                          |
|--------|---------------------------|----------|--------------------------------------|
| POST   | `/auth/register`          | –        | Register a new user (with image)     |
| POST   | `/auth/login`             | –        | Log in, get access & refresh tokens  |
| POST   | `/auth/refresh`           | –        | Refresh an expired access token      |
| POST   | `/auth/logout`            | –        | Log out                              |
| GET    | `/me`                     | required | Get the current user's profile       |
| PATCH  | `/me`                     | required | Update profile (name, image, about)  |
| GET    | `/me/plants`              | required | Get the current user's plants        |
| GET    | `/me/trades`              | required | Get the current user's trades        |
| GET    | `/me/trades/history`      | required | Get completed trades                 |
| GET    | `/me/notifications`       | required | Get notifications                    |
| GET    | `/products`               | –        | List all plants                      |
| GET    | `/products/:id`           | –        | Get a single plant                   |
| POST   | `/products`               | required | Create a plant (with image)          |
| PATCH  | `/products/:id`           | required | Update your own plant                |
| DELETE | `/products/:id`           | required | Delete your own plant                |
| GET    | `/trades`                 | required | List trades                         |
| GET    | `/trades/:id`             | required | Get a single trade (participants only) |
| POST   | `/trades`                 | required | Request a trade for a plant         |
| PUT    | `/trades/:id`             | required | Update trade status                 |
| DELETE | `/trades/:id`             | required | Delete a trade (requester only)     |

## Getting started

### Prerequisites

- Node.js 20 or higher
- A MongoDB instance (local or Atlas)
- A Cloudinary account (free tier works)

### Setup

```bash
# Clone the repo
git clone https://github.com/lukasdannemann/plot-twist-backend.git
cd plot-twist-backend

# Install dependencies (mongodb-memory-server takes a while)
npm install

# Configure environment
cp .env.example .env
# Then edit .env and fill in MongoDB URI, JWT secrets, Cloudinary keys
```

### Running

```bash
npm run dev      # Development with auto-reload
npm start        # Production
npm run seed     # Populate the database with sample data
npm test         # Run the test suite
```

The server starts on `http://localhost:3000` by default.

### Environment variables

```
PORT=3000
MONGODB_URI=mongodb://localhost:27017/plot-twist
JWT_ACCESS_SECRET=your_access_secret
JWT_REFRESH_SECRET=your_refresh_secret
JWT_ACCESS_EXPIRES=1d
JWT_REFRESH_EXPIRES=7d
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
```

## Team

- **Backend:** Lukas Dannemann, Oscar Frykedal, Philip Dale
- **Frontend:** Jenna Viirtanen, Simon Mayr

Built as a group project during the Backend 1 course at Nackademin, april 2026.
