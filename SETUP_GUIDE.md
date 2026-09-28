## MERN Stack Todo Application - Setup Guide

### System Requirements
- Node.js v14 or higher
- npm v6 or higher
- MongoDB v4.0 or higher (local or Atlas)
- Modern web browser

### Step-by-Step Installation

#### 1. Install MongoDB

**Option A: Local MongoDB**
- Download from [mongodb.com](https://www.mongodb.com/try/download/community)
- Install following the platform-specific instructions
- Ensure MongoDB service is running

**Option B: MongoDB Atlas (Cloud)**
- Go to [mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas)
- Create free account
- Create a cluster
- Get connection string: `mongodb+srv://username:password@cluster.mongodb.net/mern-todo`

#### 2. Clone Repository
```bash
git clone <repository-url>
cd MERN-TODO-APP
```

#### 3. Backend Setup

```bash
# Navigate to server directory
cd server

# Install dependencies
npm install

# Create .env file
cp .env.example .env

# Edit .env with your configuration
# MONGODB_URI=mongodb://localhost:27017/mern-todo  # or your Atlas URL
# JWT_SECRET=your_super_secret_key_here
# PORT=5000
```

**Start Backend Server**
```bash
# Development mode (with nodemon)
npm run dev

# Production mode
npm start
```

The backend will run on `http://localhost:5000`

#### 4. Frontend Setup

```bash
# Navigate to client directory
cd ../client

# Install dependencies
npm install

# Start development server
npm start
```

The frontend will run on `http://localhost:3000`

### 5. Initial Test

1. Open `http://localhost:3000` in your browser
2. Register a new account
3. Login with your credentials
4. Create, edit, delete todos
5. Test filtering and search
6. Try dark mode toggle

### Configuration Tips

#### MongoDB Connection Issues
- **Local**: Ensure MongoDB daemon is running (`mongod` on Windows/Mac or check services on Windows)
- **Atlas**: Check IP whitelist, credentials, and network access

#### Port Already in Use
```bash
# Change port in .env
PORT=5001  # or any other available port

# For React (in client directory)
set PORT=3001  # Windows
export PORT=3001  # Mac/Linux
```

#### CORS Issues
- Update `CLIENT_URL` in server/.env to match your frontend URL
- Restart backend server

### Database Schema

The application uses the following MongoDB collections:
- **users** - User accounts and profiles
- **todos** - Todo items with all details
- **categories** - Custom categories
- **sharedtodos** - Sharing relationships

### Common Issues & Solutions

#### 1. "Cannot find module 'mongoose'"
```bash
cd server
npm install mongoose
```

#### 2. "MongoDB connection refused"
```bash
# Start MongoDB
mongod

# Or check if MongoDB service is running
net start MongoDB  # Windows
brew services start mongodb-community  # Mac
```

#### 3. "JWT token expired"
- Tokens expire after 7 days by default
- User needs to login again
- Change `JWT_EXPIRE` in .env if needed

#### 4. "React app blank page"
- Check browser console for errors (F12)
- Ensure backend server is running
- Clear browser cache (Ctrl+Shift+Del)

### Running in Production

#### Backend
```bash
cd server
npm install --production
export NODE_ENV=production
export MONGODB_URI=<production-mongodb-uri>
export JWT_SECRET=<strong-secret>
npm start
```

#### Frontend
```bash
cd client
npm run build
# Serve build folder with a static server
npx serve -s build
```

### Docker Setup (Optional)

Create `docker-compose.yml`:
```yaml
version: '3.8'
services:
  mongodb:
    image: mongo:5
    ports:
      - "27017:27017"
    volumes:
      - mongodb_data:/data/db

  backend:
    build: ./server
    ports:
      - "5000:5000"
    depends_on:
      - mongodb
    environment:
      - MONGODB_URI=mongodb://mongodb:27017/mern-todo

  frontend:
    build: ./client
    ports:
      - "3000:3000"
    depends_on:
      - backend

volumes:
  mongodb_data:
```

Run with: `docker-compose up`

### Deployment Recommendations

**Backend**
- Heroku, Railway, or Vercel
- Use MongoDB Atlas for database
- Set environment variables on platform

**Frontend**
- Netlify, Vercel, or GitHub Pages
- Build: `npm run build`
- Connect repository for auto-deployment

### Next Steps

1. Customize the UI (colors, fonts)
2. Add more features (recurring tasks, reminders)
3. Set up CI/CD pipeline
4. Deploy to production
5. Monitor with tools like Sentry or LogRocket

### Support & Resources

- [MERN Stack Guide](https://www.mern.io/)
- [MongoDB Docs](https://docs.mongodb.com/)
- [Express.js Docs](https://expressjs.com/)
- [React Docs](https://react.dev/)
- [Socket.io Docs](https://socket.io/docs/)

---

Happy coding! 🚀
