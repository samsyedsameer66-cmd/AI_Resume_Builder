# AI Resume Builder

A modern, intelligent resume builder powered by AI that helps you create professional resumes with ease. This full-stack application combines a React frontend with a Node.js/Express backend and a PostgreSQL database to deliver AI-enhanced resume building capabilities.

Live: https://resume-builder-ai30.vercel.app

## ✨ Features

- **AI-Powered Enhancement**: Automatically improve your resume content with AI suggestions using Google Gemini
- **Real-time Preview**: See your resume as you build it
- **Multiple Templates**: Choose from 20+ professional resume templates
- **PDF Export**: Download your resume as a high-quality PDF
- **Document Upload**: Import existing resumes from PDF or Word documents
- **Responsive Design**: Works perfectly on desktop, tablet, and mobile devices
- **User Authentication**: Secure JWT-based login and registration system
- **Resume Management**: Save, edit, and manage multiple resumes in PostgreSQL
- **Modern UI**: Clean, intuitive interface with smooth animations
- **File Processing**: Advanced PDF and Word document parsing

## 🚀 Tech Stack

### Frontend
- **Framework**: React 19 with Vite
- **Styling**: Tailwind CSS
- **Icons**: FontAwesome, Lucide React, React Icons
- **PDF Generation**: html2pdf.js
- **HTTP Client**: Axios
- **Routing**: React Router DOM
- **Notifications**: React Toastify

### Backend
- **Runtime**: Node.js with Express.js
- **Database**: PostgreSQL, accessed with the `pg` (node-postgres) library — no ORM, raw parameterised SQL queries
- **Authentication**: JWT with bcryptjs
- **AI Integration**: Google Gemini AI (official API and an OpenRouter-based fallback path)
- **File Processing**: Multer, PDF-Parse, Mammoth
- **Security**: Helmet, CORS
- **Logging**: Morgan
- **Validation**: Express Validator

## 📋 Prerequisites

Before you begin, ensure you have the following installed:
- Node.js (v18 or higher recommended)
- npm
- PostgreSQL (local installation, e.g. via postgresql.org, or a hosted instance like Neon/Supabase)
- (Optional) Git, if you're cloning from a repository instead of using a downloaded zip

## 🛠️ Installation & Setup

### 1. Get the project

```bash
git clone https://github.com/yourusername/ai-resume-builder.git
cd Ai_ResumeBuilder-main
```
(Or simply unzip the downloaded project folder and open it.)

### 2. Database Setup

Create the database and load the schema (run these once):

```bash
psql -U postgres
```
At the `postgres=#` prompt:
```sql
CREATE DATABASE resume_builder;
\q
```
Then load the tables:
```bash
psql -U postgres -d resume_builder -f server/config/schema.sql
```

### 3. Backend Setup

```bash
cd server
npm install
```

Edit the `server/.env` file with your configuration:
```env
# Database
DB_HOST=localhost
DB_PORT=5432
DB_NAME=resume_builder
DB_USER=postgres
DB_PASSWORD=your_postgres_password

# JWT
JWT_SECRET=your-super-secret-jwt-key
JWT_REFRESH_SECRET=your-refresh-secret-key
JWT_EXPIRES_IN=7d

# Server
PORT=5000

# AI (Google Gemini)
USE_OFFICIAL_GEMINI=true
GEMINI_API_KEY=your-google-gemini-api-key
```

```bash
npm run dev
```

The server will run on `http://localhost:5000`

### 4. Frontend Setup

Open a **new** terminal (keep the backend terminal running):

```bash
cd client
npm install
```

Create a `client/.env` file (there's a `.env.example` to copy from):
```env
VITE_API_BASE_URL=http://localhost:5000
```

```bash
npm run dev
```

The client will run on `http://localhost:5173`

### 5. AI API Setup — Google Gemini

1. Go to [Google AI Studio](https://aistudio.google.com/apikey)
2. Create an API key
3. Add it to your `server/.env` file as `GEMINI_API_KEY`, and set `USE_OFFICIAL_GEMINI=true`

Without this key, the rest of the app works fine — only the "Enhance with AI" feature will fail.

## 📁 Project Structure

```
Ai_ResumeBuilder-main/
├── client/                 # Frontend React application
│   ├── public/             # Static assets (favicon, logos)
│   ├── src/
│   │   ├── components/     # Reusable UI pieces
│   │   │   ├── auth/               # Login/signup UI pieces
│   │   │   ├── ai-resume-templates/ # 20+ resume template designs
│   │   │   └── templateCard/        # Template picker cards
│   │   ├── pages/          # Screens (Home, BuildOption, details/*, auth/*)
│   │   ├── context/        # AuthContext, ResumeContext (app-wide shared state)
│   │   ├── hooks/          # Custom React hooks
│   │   ├── services/       # API calls to the backend (apiService, authService, resumeService, geminiService)
│   │   ├── routes/         # AppRoutes, PrivateRoute, PublicRoute
│   │   ├── utils/          # File parsing, formatting helpers
│   │   ├── App.jsx         # Root app component
│   │   └── main.jsx        # App entry point
│   ├── .env                # Environment variables (create from .env.example)
│   ├── package.json        # Frontend dependencies
│   ├── tailwind.config.cjs # Tailwind CSS configuration
│   └── vite.config.js      # Vite configuration
├── server/                 # Backend Node.js application
│   ├── config/              # database.js (PostgreSQL pool), schema.sql, initDb.js
│   ├── controllers/         # authController, resumeController, geminiController
│   ├── middleware/          # auth.js (JWT check), validate.js
│   ├── models/               # resumeModel.js (raw SQL queries)
│   ├── routes/               # authRoutes, resumeRoutes, geminiRoutes, dynamic/template routes
│   ├── services/             # geminiService.js (calls the Gemini API)
│   ├── utils/                 # errorHandler.js
│   ├── uploads/               # Uploaded files saved here
│   ├── scripts/                # One-off DB migration/seed scripts
│   ├── .env                    # Environment variables (secrets — not committed to Git)
│   ├── package.json            # Backend dependencies
│   └── server.js               # Server entry point
```

## 🎯 Available Scripts

### Frontend (client/)
- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build
- `npm run lint` - Run ESLint

### Backend (server/)
- `npm run dev` - Start development server with nodemon
- `npm start` - Start production server
- `node createDemoUser.js` - Create a demo user for testing

## 🔧 Configuration

### Environment Variables

#### Client (.env)
```env
VITE_API_BASE_URL=http://localhost:5000
```

#### Server (.env)
```env
DB_HOST=localhost
DB_PORT=5432
DB_NAME=resume_builder
DB_USER=postgres
DB_PASSWORD=your_postgres_password

JWT_SECRET=your-super-secret-jwt-key
JWT_REFRESH_SECRET=your-refresh-secret-key
JWT_EXPIRES_IN=7d

PORT=5000

USE_OFFICIAL_GEMINI=true
GEMINI_API_KEY=your-google-gemini-api-key
```

### Database Configuration

The application uses **PostgreSQL**, connected directly via the `pg` library (no ORM — queries are written in raw SQL). Main tables:
- `users` — accounts and hashed passwords
- `resumes` — resume content, including JSONB columns for flexible sections like skills/experience
- `enhancement_history` — a log of every AI enhancement (before/after text)
- `resume_templates` — template metadata
- `file_uploads` — tracks uploaded files linked to a resume

### AI Integration

The app is built around **Google Gemini** for content enhancement, with the request flow: client → backend `/api/enhance` route → `geminiController.js` builds a prompt → `geminiService.js` calls the Gemini API → response is logged to `enhancement_history` and returned to the client.

## 🎨 Features Overview

### Resume Builder
- Interactive form-based resume creation, one page per section (Personal Info, Experience, Education, Skills, Projects, Languages)
- Real-time preview updates
- Context-based state shared across every step (`ResumeContext`)

### AI Enhancement
- Content suggestions and rewrites using Google Gemini
- Section-specific prompts (summary, skills, experience are enhanced differently)
- Every enhancement is logged to the database for tracking

### Document Processing
- PDF resume parsing and import (`pdf-parse`, `pdfjs-dist`)
- Word document (.docx) import (`mammoth`)
- Automatic content extraction to pre-fill the resume form

### Authentication & Security
- JWT-based authentication (7-day token expiry by default)
- Secure password hashing with bcryptjs
- Protected API routes via `middleware/auth.js`
- Parameterised SQL queries (prevents SQL injection)

### Templates & Export
- 20+ professional resume templates (React components)
- High-quality PDF generation via html2pdf.js
- Mobile-responsive previews

## 🚀 API Endpoints

### Authentication (`/api/auth`)
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `GET /api/auth/profile` - Get user profile (requires token)
- `PUT /api/auth/profile` - Update user profile (requires token)
- `POST /api/auth/logout` - Log out (requires token)

### Resume Management (`/api/resumes`)
- `GET /api/resumes/my-resumes` - Get all resumes for the logged-in user
- `POST /api/resumes` - Create a new resume
- `GET /api/resumes/:id` - Get a specific resume
- `PUT /api/resumes/:id` - Update a resume
- `DELETE /api/resumes/:id` - Delete a resume
- `GET /api/resumes/suggestions` - Get resume suggestions
- `GET /api/resumes/stats/enhancements` - Enhancement usage stats

### AI Enhancement (`/api/enhance`)
- `POST /api/enhance` - Enhance a resume section with AI

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- React team for the framework
- Tailwind CSS for the utility-first CSS framework
- Vite for the fast build tool
- PostgreSQL and the node-postgres (`pg`) maintainers
- All the open-source contributors who made this project possible
