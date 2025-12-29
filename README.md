# Blog Engine

A full-stack blog application built with React, Node.js, MongoDB, and Docker. Features user authentication via Clerk and image storage with ImageKit.

## 🚀 Features

- **User Authentication**: Secure authentication powered by Clerk
- **Image Management**: Image upload and storage via ImageKit
- **RESTful API**: Express.js backend with MongoDB
- **Responsive Frontend**: React with Vite for fast development
- **Dockerized**: Complete Docker setup for easy deployment
- **Webhooks**: Integrated webhook support for Clerk events

## 🛠️ Tech Stack

### Frontend
- React 18
- Vite
- React Router
- TanStack Query
- Clerk React
- ImageKit React SDK
- Tailwind CSS

### Backend
- Node.js
- Express.js
- MongoDB with Mongoose
- Clerk SDK
- ImageKit SDK
- Nodemon (development)

### Infrastructure
- Docker & Docker Compose
- MongoDB (containerized)
- ngrok (for webhook testing)

## 📋 Prerequisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop) installed
- [Git](https://git-scm.com/downloads) installed
- [Clerk Account](https://clerk.com) (free tier available)
- [ImageKit Account](https://imagekit.io) (free tier available)
- [ngrok Account](https://ngrok.com) (optional, for webhooks)

## 🔧 Installation

### 1. Clone the repository

```bash
git clone https://github.com/codinglearningnovice/blogEngine.git
cd blogEngine
```

### 2. Set up Backend Environment Variables

Create a `.env` file in the `backend/` directory:

```bash
cd backend
cp .env.example .env
```

Edit `backend/.env` and add your credentials:

```env
# ImageKit Configuration
IK_URL_ENDPOINT=https://ik.imagekit.io/your_imagekit_id
IK_PUBLIC_KEY=your_imagekit_public_key
IK_PRIVATE_KEY=your_imagekit_private_key

# Clerk Configuration
CLERK_WEBHOOK_SECRET=your_clerk_webhook_secret

# MongoDB (Docker handles this)
DATABASE_URI=mongodb://admin:password@mongo:27017/myapp?authSource=admin

# Frontend URL
CLIENT_URL=http://localhost:5173

# Svix (for webhooks)
SVIX_API_KEY=your_svix_api_key
```

### 3. Set up Frontend Environment Variables

Create a `.env` file in the `frontend/vite-project/` directory:

```bash
cd ../frontend/vite-project
cp .env.example .env
```

Edit `frontend/vite-project/.env` and add your credentials:

```env
# Clerk Configuration
VITE_CLERK_PUBLISHABLE_KEY=pk_test_your_clerk_publishable_key

# ImageKit Configuration
VITE_IK_URL_ENDPOINT=https://ik.imagekit.io/your_imagekit_id
VITE_IK_PUBLIC_KEY=your_imagekit_public_key

# Backend API URL
VITE_API_URL=http://localhost:3000
```

### 4. Set up ngrok (Optional - for webhooks)

If you want to test webhooks locally, create `ngrok.yml` in the project root:

```yaml
version: "2"
authtoken: your_ngrok_auth_token_here
tunnels:
  backend:
    proto: http
    addr: node_backend:5000
  frontend:
    proto: http
    addr: react_frontend:5173
```

Get your ngrok authtoken from: https://dashboard.ngrok.com/get-started/your-authtoken

## 🚀 Running the Application

### Start all services with Docker

```bash
docker-compose up --build
```

This will start:
- **Frontend**: http://localhost:5173
- **Backend API**: http://localhost:3000
- **MongoDB**: localhost:27017
- **ngrok Dashboard**: http://localhost:4040 (if configured)

### Stop all services

```bash
docker-compose down
```

### View logs

```bash
docker-compose logs -f
```

## 📝 Getting API Keys

### Clerk Setup

1. Go to https://clerk.com and sign up
2. Create a new application
3. Go to **API Keys** section
4. Copy your **Publishable Key** (starts with `pk_test_` or `pk_live_`)
5. For webhooks, go to **Webhooks** → Create endpoint
6. Copy the **Signing Secret** for `CLERK_WEBHOOK_SECRET`

### ImageKit Setup

1. Go to https://imagekit.io and sign up
2. Go to **Developer Options** → **API Keys**
3. Copy:
   - **URL Endpoint** (e.g., `https://ik.imagekit.io/your_id`)
   - **Public Key**
   - **Private Key** (keep this secret!)

### ngrok Setup (Optional)

1. Go to https://ngrok.com and sign up
2. Go to **Your Authtoken** page
3. Copy your authtoken



## 📂 Project Structure

```
blog_engine/
├── backend/
│   ├── controllers/      # Request handlers
│   ├── models/          # MongoDB schemas
│   ├── routes/          # API routes
│   ├── config/          # Configuration files
│   ├── .env             # Backend environment variables (not in git)
│   ├── server.js        # Entry point
│   └── Dockerfile
├── frontend/
│   └── vite-project/
│       ├── src/
│       │   ├── components/
│       │   ├── pages/
│       │   └── main.jsx
│       ├── .env         # Frontend environment variables (not in git)
│       └── Dockerfile
├── docker-compose.yml    # Docker orchestration
├── ngrok.yml            # ngrok configuration (not in git)
└── README.md
```




## 📚 API Endpoints

### Posts
- `GET /posts` - Get all posts
- `GET /posts/:slug` - Get single post
- `POST /posts` - Create new post (authenticated)
- `PUT /posts/:id` - Update post (authenticated)
- `DELETE /posts/:id` - Delete post (authenticated)

### Users
- `GET /users/:username` - Get user profile
- `GET /users/saved` - Get saved posts (authenticated)

### Comments
- `GET /posts/:postId/comments` - Get post comments
- `POST /comments` - Create comment (authenticated)
- `DELETE /comments/:id` - Delete comment (authenticated)

### Webhooks
- `POST /webhooks/clerk` - Clerk webhook endpoint



## 👤 Author

**codinglearningnovice**
- GitHub: [@codinglearningnovice](https://github.com/codinglearningnovice)

## 🙏 Acknowledgments

- [Clerk](https://clerk.com) for authentication
- [ImageKit](https://imagekit.io) for image storage
- [MongoDB](https://www.mongodb.com) for database
- [ngrok](https://ngrok.com) for webhook tunneling

---

**Note**: This is a development setup. For production deployment, additional security measures and optimizations are recommended.