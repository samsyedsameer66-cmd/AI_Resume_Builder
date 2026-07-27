# AI Resume Builder

A modern, intelligent resume builder powered by AI that helps you create professional resumes with ease. This full-stack application combines a React frontend with a Node.js backend to deliver AI-enhanced resume building capabilities.

Live-ai-resume-builder-eight-ruddy.vercel.app

## ✨ Features

- **AI-Powered Enhancement**: Automatically improve your resume content with AI suggestions using Google Gemini and OpenAI
- **Real-time Preview**: See your resume as you build it
- **Multiple Templates**: Choose from various professional resume templates
- **PDF Export**: Download your resume as a high-quality PDF
- **Document Upload**: Import existing resumes from PDF or Word documents
- **Responsive Design**: Works perfectly on desktop, tablet, and mobile devices
- **User Authentication**: Secure JWT-based login and registration system
- **Resume Management**: Save, edit, and manage multiple resumes in MongoDB
- **Modern UI**: Clean, intuitive interface with smooth animations
- **File Processing**: Advanced PDF and Word document parsing

## 🚀 Tech Stack

### Frontend
- **Framework**: React 19 with Vite
- **Styling**: Tailwind CSS v4
- **Icons**: FontAwesome, Lucide React, React Icons
- **Animations**: Framer Motion
- **PDF Generation**: html2pdf.js
- **HTTP Client**: Axios
- **Routing**: React Router DOM
- **Notifications**: React Toastify

### Backend
- **Runtime**: Node.js with Express.js
- **Database**: MongoDB with Mongoose
- **Authentication**: JWT with bcryptjs
- **AI Integration**: Google Gemini AI, OpenAI
- **File Processing**: Multer, PDF-Parse, Mammoth
- **Security**: Helmet, CORS
- **Logging**: Winston, Morgan
- **Validation**: Express Validator

## 📋 Prerequisites

Before you begin, ensure you have the following installed:
- Node.js (version 16 or higher)
- npm or yarn package manager
- MongoDB (local installation or MongoDB Atlas account)
- Git

## 🛠️ Installation & Setup

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/ai-resume-builder.git
cd ai-resume-builder/Ai_Resume_Akshay
```

### 2. Backend Setup

```bash
# Navigate to server directory
cd server

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
```

Edit the `server/.env` file with your configuration:
```env
# Database
MONGODB_URI=mongodb://localhost:27017/ai-resume-builder
# or for MongoDB Atlas:
# MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/ai-resume-builder

# JWT Secret
JWT_SECRET=your-super-secret-jwt-key
JWT_REFRESH_SECRET=your-refresh-secret-key

# AI API Keys
GOOGLE_API_KEY=your-google-gemini-api-key
OPENAI_API_KEY=your-openai-api-key

# Server Configuration
PORT=5000
NODE_ENV=development

# CORS
CLIENT_URL=http://localhost:5173
```

```bash
# Start the backend server
npm run dev
# or for production
npm start
```

The server will run on `http://localhost:5000`

### 3. Frontend Setup

Open a new terminal and navigate to the client directory:

```bash
# Navigate to client directory
cd ../client

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
```

Edit the `client/.env` file:
```env
VITE_API_BASE_URL=http://localhost:5000
```

```bash
# Start the frontend development server
npm run dev
```

The client will run on `http://localhost:5173`

### 4. Database Setup

If using local MongoDB:
```bash
# Start MongoDB service
mongod
```

If using MongoDB Atlas:
- Create a cluster on [MongoDB Atlas](https://www.mongodb.com/atlas)
- Get your connection string
- Update the `MONGODB_URI` in your server `.env` file

### 5. AI API Setup

#### Google Gemini AI
1. Go to [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Create an API key
3. Add it to your server `.env` file as `GOOGLE_API_KEY`

#### OpenAI (Optional)
1. Go to [OpenAI Platform](https://platform.openai.com/api-keys)
2. Create an API key
3. Add it to your server `.env` file as `OPENAI_API_KEY`

## 📁 Project Structure

```
Ai_Resume_Akshay/
├── client/                 # Frontend React application
│   ├── public/
│   │   ├── Resume.svg      # App favicon
│   │   └── vite.svg
│   ├── src/
│   │   ├── components/
│   │   │   ├── auth/       # Authentication components
│   │   │   ├── common/     # Reusable UI components
│   │   │   ├── forms/      # Form components
│   │   │   └── resume/     # Resume-specific components
│   │   ├── pages/          # Page components
│   │   ├── services/       # API service layer
│   │   ├── utils/          # Utility functions
│   │   ├── App.jsx         # Main app component
│   │   └── main.jsx        # App entry point
│   ├── .env.example        # Environment variables template
│   ├── package.json        # Frontend dependencies
│   ├── tailwind.config.cjs # Tailwind CSS configuration
│   └── vite.config.js      # Vite configuration
├── server/                 # Backend Node.js application
│   ├── config/             # Database and app configuration
│   ├── controllers/        # Route controllers
│   ├── middleware/         # Custom middleware
│   ├── models/             # MongoDB models
│   ├── routes/             # API routes
│   ├── services/           # Business logic services
│   ├── utils/              # Utility functions
│   ├── uploads/            # File upload directory
│   ├── .env                # Environment variables
│   ├── package.json        # Backend dependencies
│   └── server.js           # Server entry point
└── test-endpoints.sh       # API testing script
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
- `node createDemoUser.js` - Create demo user for testing

## 🔧 Configuration

### Environment Variables

#### Client (.env)
```env
VITE_API_BASE_URL=http://localhost:5000
```

#### Server (.env)
```env
# Database
MONGODB_URI=mongodb://localhost:27017/ai-resume-builder

# JWT
JWT_SECRET=your-super-secret-jwt-key
JWT_REFRESH_SECRET=your-refresh-secret-key

# AI APIs
GOOGLE_API_KEY=your-google-gemini-api-key
OPENAI_API_KEY=your-openai-api-key

# Server
PORT=5000
NODE_ENV=development
CLIENT_URL=http://localhost:5173
```

### Database Configuration

The application uses MongoDB with Mongoose ODM. Models include:
- User (authentication and profile)
- Resume (resume data and metadata)
- File uploads for document processing

### AI Integration

The app supports multiple AI providers:
- **Google Gemini AI**: Primary AI service for content enhancement
- **OpenAI**: Alternative AI service for content generation

## 🎨 Features Overview

### Resume Builder
- Interactive form-based resume creation
- Real-time preview updates
- Multiple sections: Personal Info, Experience, Education, Skills, etc.
- Drag-and-drop functionality for reordering sections

### AI Enhancement
- Intelligent content suggestions using Google Gemini AI
- Grammar and style improvements
- Industry-specific optimizations
- Keyword optimization for ATS systems
- Multiple AI models support (Gemini, OpenAI)

### Document Processing
- PDF resume parsing and import
- Word document (.docx) import
- Automatic content extraction and formatting
- File upload with validation

### Authentication & Security
- JWT-based authentication
- Secure password hashing with bcryptjs
- Protected API routes
- User session management

### Templates & Export
- Professional resume templates
- Customizable layouts
- High-quality PDF generation
- Print-friendly designs
- Mobile-responsive previews

## 🚀 API Endpoints

### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `GET /api/auth/profile` - Get user profile
- `POST /api/auth/refresh` - Refresh JWT token

### Resume Management
- `GET /api/resumes` - Get all user resumes
- `POST /api/resumes` - Create new resume
- `GET /api/resumes/:id` - Get specific resume
- `PUT /api/resumes/:id` - Update resume
- `DELETE /api/resumes/:id` - Delete resume

### AI Enhancement
- `POST /api/ai/enhance` - Enhance resume content with AI

### File Upload
- `POST /api/upload` - Upload and parse resume files

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- React team for the amazing framework
- Tailwind CSS for the utility-first CSS framework
- Vite for the fast build tool
- All the open-source contributors who made this project possible

## 📞 Support

If you have any questions or need help, please:
- Open an issue on GitHub
- Contact the maintainers

---

**Made with ❤️ by Akshay**
