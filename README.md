# MedSync - Medical Appointment Platform

![MedSync Logo](frontend/public/logo.jpeg)

## 🏥 Overview

MedSync is a modern medical appointment platform that connects patients with healthcare providers. Built with cutting-edge AI technology, it offers intelligent doctor recommendations, smart scheduling, and AI-assisted prescription writing.

## ✨ Key Features

### For Patients
- 🗺️ **Interactive Map**: Find nearby doctors using Leaflet.js and OpenStreetMap
- 🤖 **AI Doctor Recommendations**: Get personalized doctor suggestions based on symptoms
- 📅 **Smart Scheduling**: AI-optimized appointment booking with availability detection
- 🔍 **Advanced Search**: Filter by specialization, rating, distance, and experience
- 📱 **Responsive Design**: Seamless experience across all devices
- 🔐 **Secure Authentication**: JWT-based user authentication

### For Doctors
- 📋 **Digital Prescriptions**: Create and manage prescriptions
- 🤖 **AI Prescription Assistant**: Get diagnosis and medication suggestions
- 📊 **Appointment Management**: View and manage patient appointments
- 👥 **Patient Dashboard**: Track patient history and visits

### AI-Powered Features (Groq Integration)
- **Doctor Matching**: Llama 3.3 70B model analyzes patient requirements
- **Prescription Assistance**: AI-generated diagnosis and medication recommendations
- **Smart Scheduling**: Intelligent time slot optimization

## 🛠️ Tech Stack

### Frontend
- **Framework**: React 18 + TypeScript
- **Build Tool**: Vite
- **UI Library**: shadcn/ui + Tailwind CSS
- **Routing**: React Router v6
- **Maps**: Leaflet.js + react-leaflet
- **Animation**: Framer Motion
- **Forms**: React Hook Form + Zod validation

### Backend
- **Runtime**: Node.js
- **Framework**: Express.js
- **Database**: MongoDB with Mongoose
- **Authentication**: JWT + bcrypt
- **File Upload**: Cloudinary integration
- **Security**: Helmet, CORS, Rate Limiting

### AI Integration
- **Provider**: Groq AI
- **Model**: Llama 3.3 70B Versatile
- **SDK**: groq-sdk

## 📁 Project Structure

```
MedSync_JK1/
├── backend/
│   ├── src/
│   │   ├── controllers/      # Request handlers
│   │   ├── models/           # MongoDB schemas
│   │   ├── routes/           # API routes
│   │   ├── middlewares/      # Auth, validation, error handling
│   │   ├── validators/       # Input validation
│   │   ├── utils/            # Helper functions
│   │   └── config/           # Database config
│   ├── server.js            # Entry point
│   ├── Dockerfile           # Docker configuration
│   └── .env.production      # Production environment template
├── frontend/
│   ├── src/
│   │   ├── components/       # React components
│   │   ├── pages/           # Page components
│   │   ├── services/        # API services + Groq AI
│   │   ├── contexts/        # React Context (Auth)
│   │   ├── hooks/           # Custom hooks
│   │   └── lib/             # Utilities
│   ├── public/              # Static assets
│   ├── Dockerfile           # Docker configuration
│   ├── nginx.conf           # Nginx configuration
│   └── .env.production      # Production environment template
├── docker-compose.yml       # Multi-container setup
├── build.sh                 # Linux/Mac build script
├── build.bat                # Windows build script
├── DEPLOYMENT_GUIDE.md      # Comprehensive deployment guide
├── GROQ_AI_INTEGRATION.md   # AI features documentation
└── PROJECT_DOCUMENTATION.md # Full project documentation
```

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ and npm
- MongoDB (local or Atlas)
- Groq API key (for AI features)

### Installation

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd MedSync_JK1
   ```

2. **Install dependencies**
   ```bash
   # Install all dependencies
   npm run install:all
   
   # Or install separately
   cd backend && npm install
   cd ../frontend && npm install
   ```

3. **Configure environment variables**
   
   **Backend** (`backend/.env`):
   ```env
   PORT=5000
   MONGODB_URI=mongodb://localhost:27017/medsync
   JWT_SECRET=your_secret_key
   CLIENT_URL=http://localhost:8080
   ```
   
   **Frontend** (`frontend/.env`):
   ```env
   VITE_API_URL=http://localhost:5000/api
   VITE_GROQ_API_KEY=your_groq_api_key
   ```

4. **Run development servers**
   ```bash
   # Terminal 1 - Backend
   cd backend
   npm run dev
   
   # Terminal 2 - Frontend
   cd frontend
   npm run dev
   ```

5. **Access the application**
   - Frontend: http://localhost:8080
   - Backend API: http://localhost:5000

## 🐳 Docker Deployment

### Using Docker Compose (Recommended)
```bash
# Build and start all services
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```

### Individual Containers
```bash
# Backend
cd backend
docker build -t medsync-backend .
docker run -p 5000:5000 --env-file .env medsync-backend

# Frontend
cd frontend
docker build -t medsync-frontend .
docker run -p 8080:80 medsync-frontend
```

## 📦 Production Build

### Windows
```bash
build.bat
```

### Linux/Mac
```bash
chmod +x build.sh
./build.sh
```

### Manual Build
```bash
# Backend
cd backend
npm install --production

# Frontend
cd frontend
npm install
npm run build
```

## 🌐 Deployment

See [DEPLOYMENT_GUIDE.md](DEPLOYMENT_GUIDE.md) for comprehensive deployment instructions including:
- Vercel + Render deployment
- Railway deployment
- Heroku deployment
- Docker deployment
- Environment configuration
- Security checklist
- Monitoring setup

## 🤖 AI Features

See [GROQ_AI_INTEGRATION.md](GROQ_AI_INTEGRATION.md) for details on:
- AI doctor recommendations
- Smart prescription assistant
- Intelligent appointment scheduling
- Groq API configuration
- Fallback strategies

## 📚 API Documentation

### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `GET /api/auth/me` - Get current user

### Doctors
- `GET /api/doctors` - Get all doctors
- `GET /api/doctors/:id` - Get doctor by ID
- `POST /api/doctors` - Create doctor (protected)

### Appointments
- `GET /api/appointments` - Get appointments (protected)
- `POST /api/appointments` - Book appointment (protected)
- `PUT /api/appointments/:id` - Update appointment (protected)

### Prescriptions
- `GET /api/prescriptions` - Get prescriptions (protected)
- `POST /api/prescriptions` - Create prescription (doctor only)

## 🔒 Security Features

- JWT authentication with httpOnly cookies
- Password hashing with bcrypt
- Rate limiting on API endpoints
- CORS configuration
- Input validation and sanitization
- XSS protection
- MongoDB injection prevention

## 🧪 Testing

```bash
# Backend tests
cd backend
npm test

# Frontend tests
cd frontend
npm test
```

## 📄 License

MIT License - see LICENSE file for details

## 👥 Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

## 📞 Support

For issues and questions:
- Create an issue on GitHub
- Check existing documentation
- Review DEPLOYMENT_GUIDE.md

## 🎯 Roadmap

- [ ] Mobile app (React Native)
- [ ] Video consultations
- [ ] Payment integration
- [ ] Multi-language support
- [ ] Advanced analytics dashboard
- [ ] Email/SMS notifications
- [ ] Insurance integration

## ⚡ Performance

- Lighthouse Score: 95+
- First Contentful Paint: <1.5s
- Time to Interactive: <3s
- Optimized bundle size with code splitting
- Image optimization with Cloudinary

## 🙏 Acknowledgments

- Groq AI for powerful LLM capabilities
- OpenStreetMap for free map data
- shadcn/ui for beautiful components
- MongoDB Atlas for database hosting

---

**Built with ❤️ by the MedSync Team**

**Last Updated**: December 17, 2025
