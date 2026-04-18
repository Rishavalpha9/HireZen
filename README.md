# HireZen

HireZen is a full-stack job portal web application where candidates can discover jobs and apply, while recruiters can manage postings and applications from a dedicated dashboard.

## Features

- Browse open jobs with filters for title and location
- View a detailed job page and apply as an authenticated user
- Track candidate applications and their status
- Recruiter/company authentication with JWT-based dashboard access
- Recruiter dashboard to post jobs, toggle job visibility, and review applicants
- Resume upload support for candidates
- Clerk + webhook sync to keep user data updated in MongoDB

## Tech Stack

### Frontend (`client`)
- React + Vite
- React Router
- Tailwind CSS
- Clerk (`@clerk/clerk-react`) for candidate auth
- Axios + React Toastify

### Backend (`server`)
- Node.js + Express
- MongoDB + Mongoose
- Clerk Express middleware + Svix webhook verification
- JWT auth for company/recruiter flows
- Cloudinary + Multer for file uploads
- Sentry integration for error monitoring

## Project Structure

```text
HireZen/
  client/   # React frontend
  server/   # Express API + database logic
```

## Environment Variables

Create separate `.env` files in `client` and `server`.

### `server/.env`

```env
PORT=5000
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
CLOUDINARY_NAME=your_cloudinary_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_SECRET_KEY=your_cloudinary_secret
CLERK_WEBHOOK_SECRET=your_clerk_webhook_secret
```

### `client/.env`

```env
VITE_BACKEND_URL=http://localhost:5000
VITE_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
```

## Local Development

### 1) Install dependencies

```bash
cd client
npm install

cd ../server
npm install
```

### 2) Run backend

```bash
cd server
npm run server
```

### 3) Run frontend

```bash
cd client
npm run dev
```

Frontend runs on Vite's default port (usually `5173`), and backend runs on `5000` unless overridden.

## API Overview

### Public job routes
- `GET /api/jobs` - list visible jobs
- `GET /api/jobs/:id` - fetch job details

### User routes (Clerk-authenticated)
- `GET /api/users/user`
- `POST /api/users/apply`
- `GET /api/users/applications`
- `POST /api/users/update-resume`

### Company routes (JWT token in `headers.token`)
- `POST /api/company/register`
- `POST /api/company/login`
- `GET /api/company/company`
- `POST /api/company/post-job`
- `GET /api/company/list-jobs`
- `GET /api/company/applicants`
- `POST /api/company/change-status`
- `POST /api/company/change-visiblity`

### Webhook route
- `POST /webhooks` - handles Clerk user create/update/delete events

## Deployment Notes

- Both `client` and `server` include `vercel.json` files for Vercel deployment.
- Set the same environment variables on your hosting provider before deploying.

## License

This project is licensed under the terms of the `LICENSE` file.
