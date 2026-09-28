# Project Structure Guide

## Backend (/server)

```
server/
├── models/              # MongoDB schemas
│   ├── User.js         # User model with password hashing
│   ├── Todo.js         # Todo model with all fields
│   ├── Category.js     # Category model
│   └── SharedTodo.js   # Sharing relationships
│
├── routes/             # API endpoints
│   ├── auth.js         # Authentication routes
│   ├── todos.js        # Todo CRUD and operations
│   ├── categories.js   # Category management
│   ├── shared.js       # Sharing functionality
│   └── export.js       # Data export (JSON/CSV/PDF)
│
├── middleware/         # Custom middleware
│   └── auth.js         # JWT verification
│
├── socket/             # Real-time communication
│   └── socketHandlers.js  # Socket.io events
│
├── server.js           # Express server setup
├── package.json        # Dependencies
├── .env.example        # Environment template
└── .gitignore
```

## Frontend (/client)

```
client/
├── public/
│   ├── index.html      # HTML entry point
│   └── favicon.ico
│
├── src/
│   ├── components/     # Reusable components
│   │   ├── Header.js      # Top navigation bar
│   │   ├── Sidebar.js     # Side navigation
│   │   ├── TodoForm.js    # Create/Edit form
│   │   ├── TodoList.js    # List display
│   │   ├── TodoItem.js    # Individual todo
│   │   ├── FilterBar.js   # Search & filters
│   │   └── Dashboard.js   # Statistics view
│   │
│   ├── pages/          # Page components
│   │   ├── LoginPage.js
│   │   ├── RegisterPage.js
│   │   └── Dashboard.js
│   │
│   ├── store/          # State management (Zustand)
│   │   └── index.js    # All stores
│   │
│   ├── styles/         # CSS files
│   │   ├── index.css       # Global styles
│   │   ├── auth.css        # Auth pages
│   │   ├── dashboard.css   # Dashboard
│   │   ├── header.css      # Header
│   │   ├── sidebar.css     # Sidebar
│   │   ├── form.css        # Forms
│   │   ├── todolist.css    # Todo list
│   │   ├── todoitem.css    # Individual todo
│   │   ├── filterbar.css   # Filters
│   │   └── App.css         # App-wide
│   │
│   ├── App.js          # Main app component
│   ├── index.js        # React entry point
│   └── .gitignore
│
├── package.json        # Dependencies
└── .env.example        # Environment template
```

## Key Features Implementation

### Authentication
- **Files**: `server/models/User.js`, `server/routes/auth.js`
- **Implementation**: JWT tokens, bcrypt hashing, middleware protection

### Todo Management
- **Files**: `server/models/Todo.js`, `server/routes/todos.js`
- **Features**: CRUD, filters, search, priority, due dates, tags

### Real-time Updates
- **Files**: `server/socket/socketHandlers.js`
- **Implementation**: Socket.io events for instant notifications

### Data Export
- **Files**: `server/routes/export.js`
- **Formats**: JSON, CSV, PDF with PDFKit

### Dark Mode
- **Files**: `client/src/store/index.js`, `client/src/components/Header.js`
- **Implementation**: Theme toggle with local storage persistence

### Categories & Organization
- **Files**: `server/models/Category.js`, `server/routes/categories.js`
- **Features**: Custom colors, icons, organization

## Data Flow

### Creating a Todo
1. User fills form in `TodoForm.js`
2. Submit → API call to `POST /api/todos`
3. Backend validates and saves to MongoDB
4. Socket.io broadcasts update
5. `useTodoStore` updates state
6. UI re-renders with new todo

### Real-time Collaboration
1. User A shares todo with User B
2. Socket event sent to User B
3. User B gets notification
4. Changes from User B sync back via Socket.io
5. User A sees live updates

## Environment Variables

### Server
```
PORT - Server port (default: 5000)
MONGODB_URI - MongoDB connection string
JWT_SECRET - Secret for token signing
JWT_EXPIRE - Token expiration (default: 7d)
NODE_ENV - development/production
CLIENT_URL - Frontend URL for CORS
```

### Client
```
REACT_APP_API_URL - Backend API URL
```

## Deployment Checklist

- [ ] Update environment variables
- [ ] Set secure JWT_SECRET
- [ ] Configure MongoDB connection
- [ ] Enable CORS for production domain
- [ ] Build frontend: `npm run build`
- [ ] Test all features
- [ ] Set up monitoring
- [ ] Configure backups
- [ ] Enable HTTPS
- [ ] Set up CI/CD pipeline

---

For more details, see README.md and SETUP_GUIDE.md
