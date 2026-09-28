<!-- ==================== ENVIRONMENT SETUP & DEPLOYMENT GUIDE ====================
File: .env.example & DEPLOYMENT_GUIDE.md -->

# ENVIRONMENT SETUP GUIDE

## Backend Environment Variables
**File: server/.env**

```env
# Database Configuration
MONGODB_URI=mongodb://localhost:27017/mern-todo
MONGODB_USER=
MONGODB_PASSWORD=

# JWT Configuration
JWT_SECRET=your_super_secret_jwt_key_here_change_in_production
JWT_EXPIRE=7d

# Server Configuration
PORT=5000
NODE_ENV=development

# CORS Configuration
CLIENT_URL=http://localhost:3000
CORS_ORIGIN=http://localhost:3000

# Email Configuration (Optional - for future email notifications)
EMAIL_SERVICE=gmail
EMAIL_USER=your-email@gmail.com
EMAIL_PASS=your-app-password
EMAIL_FROM=noreply@todoapp.com

# AWS Configuration (Optional - for file uploads)
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_S3_BUCKET=
AWS_REGION=us-east-1

# Redis Configuration (Optional - for caching)
REDIS_URL=redis://localhost:6379

# API Keys (Optional)
GOOGLE_OAUTH_CLIENT_ID=
GOOGLE_OAUTH_CLIENT_SECRET=
```

## Frontend Environment Variables
**File: client/.env**

```env
REACT_APP_API_URL=http://localhost:5000
REACT_APP_SOCKET_URL=http://localhost:5000
REACT_APP_ENV=development

# Optional OAuth
REACT_APP_GOOGLE_CLIENT_ID=
REACT_APP_GITHUB_CLIENT_ID=
```

## Installation & Setup

### 1. Prerequisites
- Node.js (v14 or higher)
- MongoDB (local or MongoDB Atlas)
- npm or yarn

### 2. Backend Setup

```bash
cd server

# Install dependencies
npm install

# Create .env file
cp .env.example .env

# Update .env with your configuration
nano .env

# Run migrations (if using)
npm run migrate

# Start development server
npm run dev

# Or start production server
npm start
```

**Required npm packages for backend:**
```json
{
  "dependencies": {
    "express": "^4.18.2",
    "mongoose": "^7.0.0",
    "bcryptjs": "^2.4.3",
    "jsonwebtoken": "^9.0.0",
    "cors": "^2.8.5",
    "dotenv": "^16.0.3",
    "socket.io": "^4.5.4",
    "express-validator": "^7.0.0",
    "pdfkit": "^0.13.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.22"
  }
}
```

### 3. Frontend Setup

```bash
cd client

# Install dependencies
npm install

# Create .env file
cp .env.example .env

# Update .env with your configuration
nano .env

# Start development server
npm start

# Or build for production
npm run build
```

**Required npm packages for frontend:**
```json
{
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-router-dom": "^6.10.0",
    "zustand": "^4.3.7",
    "socket.io-client": "^4.5.4",
    "axios": "^1.3.0",
    "date-fns": "^2.29.3",
    "react-icons": "^4.8.0"
  },
  "devDependencies": {
    "react-scripts": "^5.0.1"
  }
}
```

## Running the Application

### Development Mode (Local)

**Terminal 1 - Backend:**
```bash
cd server
npm run dev
# Server runs on http://localhost:5000
```

**Terminal 2 - Frontend:**
```bash
cd client
npm start
# App opens on http://localhost:3000
```

### Production Deployment

#### Option 1: Heroku Deployment

**Backend:**
```bash
cd server

# Create Heroku app
heroku create your-app-name

# Set environment variables
heroku config:set JWT_SECRET=your_production_secret
heroku config:set MONGODB_URI=your_mongodb_atlas_url
heroku config:set NODE_ENV=production

# Deploy
git push heroku main
```

**Frontend:**
```bash
cd client

# Build production version
npm run build

# Deploy to Netlify (or Vercel)
# Using Netlify CLI:
npm install -g netlify-cli
netlify deploy --prod --dir=build

# Or using Vercel:
npm install -g vercel
vercel --prod
```

#### Option 2: Docker Deployment

**Dockerfile (Backend):**
```dockerfile
FROM node:18

WORKDIR /app

COPY package*.json ./
RUN npm install --production

COPY . .

EXPOSE 5000

CMD ["npm", "start"]
```

**Dockerfile (Frontend):**
```dockerfile
FROM node:18 as builder

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

FROM nginx:alpine

COPY --from=builder /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

**docker-compose.yml:**
```yaml
version: '3.8'

services:
  mongodb:
    image: mongo:5.0
    ports:
      - "27017:27017"
    volumes:
      - mongo_data:/data/db
    environment:
      - MONGO_INITDB_ROOT_USERNAME=root
      - MONGO_INITDB_ROOT_PASSWORD=password

  backend:
    build: ./server
    ports:
      - "5000:5000"
    depends_on:
      - mongodb
    environment:
      - MONGODB_URI=mongodb://root:password@mongodb:27017/mern-todo
      - JWT_SECRET=your_jwt_secret
      - NODE_ENV=production

  frontend:
    build: ./client
    ports:
      - "3000:80"
    depends_on:
      - backend
    environment:
      - REACT_APP_API_URL=http://backend:5000

volumes:
  mongo_data:
```

**Run with Docker Compose:**
```bash
docker-compose up -d
```

#### Option 3: AWS Deployment

**Backend on EC2:**
```bash
# SSH into EC2 instance
ssh -i your-key.pem ec2-user@your-instance-ip

# Install Node.js and npm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
nvm install 18
npm install -g pm2

# Clone repository
git clone your-repo-url
cd mern-todo-app/server

# Install and run
npm install --production
pm2 start server.js --name "todo-api"
pm2 startup
pm2 save
```

**Frontend on S3 + CloudFront:**
```bash
# Build application
cd client
npm run build

# Upload to S3
aws s3 sync build/ s3://your-bucket-name --delete

# Invalidate CloudFront cache
aws cloudfront create-invalidation --distribution-id YOUR_DIST_ID --paths "/*"
```

## Database Setup

### MongoDB Local Setup

```bash
# Start MongoDB locally
mongod

# In another terminal, connect to MongoDB
mongo

# Create database
use mern-todo
```

### MongoDB Atlas Setup

1. Create account at https://www.mongodb.com/cloud/atlas
2. Create a cluster
3. Get connection string
4. Add to `.env` as `MONGODB_URI`

## API Endpoints Reference

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/me` - Get current user
- `PUT /api/auth/profile` - Update profile

### Todos
- `GET /api/todos` - Get all todos with filters
- `POST /api/todos` - Create todo
- `GET /api/todos/:id` - Get single todo
- `PUT /api/todos/:id` - Update todo
- `DELETE /api/todos/:id` - Delete todo
- `PATCH /api/todos/:id/toggle` - Toggle completion
- `POST /api/todos/:id/subtask` - Add subtask
- `PUT /api/todos/:id/subtask/:subtaskId` - Update subtask
- `DELETE /api/todos/:id/subtask/:subtaskId` - Delete subtask

### Categories
- `GET /api/categories` - Get all categories
- `POST /api/categories` - Create category
- `PUT /api/categories/:id` - Update category
- `DELETE /api/categories/:id` - Delete category

### Sharing
- `POST /api/shared/share` - Share todo
- `GET /api/shared/received` - Get received shares
- `DELETE /api/shared/:id` - Remove share

### Export
- `GET /api/export/json` - Export as JSON
- `GET /api/export/csv` - Export as CSV
- `GET /api/export/pdf` - Export as PDF

## Troubleshooting

### MongoDB Connection Error
```
MongooseError: Cannot connect to MongoDB
```
**Solution:** Ensure MongoDB is running and connection string is correct

### CORS Error
```
Access to XMLHttpRequest blocked by CORS policy
```
**Solution:** Update `CLIENT_URL` in `.env` to match frontend URL

### JWT Token Expired
```
TokenExpiredError: jwt expired
```
**Solution:** User needs to login again

### Port Already in Use
```
EADDRINUSE: address already in use :::5000
```
**Solution:** 
```bash
# Find process using port
lsof -i :5000

# Kill process
kill -9 <PID>
```

## Performance Optimization

### Database Optimization
```javascript
// Add indexes in models
TodoSchema.index({ userId: 1, createdAt: -1 });
TodoSchema.index({ userId: 1, completed: 1 });
TodoSchema.index({ dueDate: 1 });
```

### Caching
```javascript
// Implement Redis caching
const redis = require('redis');
const client = redis.createClient();

router.get('/cached-todos/:userId', async (req, res) => {
  const cached = await client.get(`todos:${req.userId}`);
  if (cached) return res.json(JSON.parse(cached));
  
  const todos = await Todo.find({ userId: req.userId });
  await client.setex(`todos:${req.userId}`, 300, JSON.stringify(todos));
  res.json(todos);
});
```

### Frontend Optimization
```javascript
// Implement code splitting
const Dashboard = React.lazy(() => import('./pages/Dashboard'));
const TodoList = React.lazy(() => import('./components/TodoList'));

// Use Suspense
<Suspense fallback={<Loading />}>
  <Dashboard />
</Suspense>
```

## Security Checklist

- [ ] Change JWT_SECRET to a strong random string
- [ ] Enable HTTPS in production
- [ ] Set NODE_ENV=production
- [ ] Implement rate limiting
- [ ] Add input validation on all endpoints
- [ ] Enable CORS only for trusted domains
- [ ] Store sensitive data in environment variables
- [ ] Implement password reset functionality
- [ ] Add authentication to all protected routes
- [ ] Use prepared statements for database queries

## Maintenance

### Monitoring
```bash
# Monitor application logs
pm2 logs

# Monitor system resources
pm2 monit
```

### Backups
```bash
# Backup MongoDB database
mongodump --uri "mongodb://connection-string" --out ./backups

# Restore database
mongorestore ./backups
```

### Updates
```bash
# Check for outdated packages
npm outdated

# Update packages
npm update

# Update to latest major versions
npm install -g npm-check-updates
ncu -u
npm install
```
