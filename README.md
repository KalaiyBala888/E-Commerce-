# MERN Stack Todo Application

A comprehensive, full-featured Todo application built with the MERN stack (MongoDB, Express, React, Node.js).

## Features

### ✅ Core CRUD Operations
- Create, Read, Update, Delete todos
- Bulk operations support
- Undo/Redo functionality

### 📋 Advanced Task Management
- **Categories**: Organize tasks by custom categories with colors and icons
- **Priority Levels**: Low, Medium, High priority indicators
- **Due Dates**: Set deadlines with visual indicators for overdue tasks
- **Subtasks**: Break down complex tasks into subtasks
- **Tags**: Organize tasks with custom tags
- **Recurring Tasks**: Create daily, weekly, monthly, or yearly recurring tasks
- **Reminders**: Set reminders (5 min, 15 min, 1 hour, 1 day, 1 week before due date)

### 🔍 Search & Filtering
- Full-text search across title and description
- Filter by completion status
- Filter by priority level
- Filter by category
- Filter by tags
- Sort by due date, priority, or creation date

### 👥 Collaboration & Sharing
- Share todos with other users
- Set granular permissions (View, Edit)
- Real-time notifications for shared items
- View shared todos from other users

### 📊 Dashboard & Analytics
- Overview statistics (Total, Completed, Pending, Overdue)
- Completion rate progress
- Visual charts and graphs
- Task completion trends

### 📤 Data Export
- Export to JSON format
- Export to CSV format
- Export to PDF format
- Batch export functionality

### 🌓 Dark Mode
- Toggle between light and dark themes
- Persistent theme preference
- Eye-friendly dark interface

### 🔐 Authentication & Security
- User registration and login
- JWT-based authentication
- Secure password hashing with bcrypt
- Session management
- Protected routes

### 🔔 Real-time Updates
- Socket.io integration for real-time updates
- Live notifications for shared todos
- Instant UI updates across multiple devices
- Collaborative task updates

### 📱 Responsive Design
- Mobile-friendly interface
- Tablet optimization
- Desktop experience
- Adaptive layouts

### ⚙️ User Preferences
- Customizable theme (Light/Dark)
- Notification settings
- User profile management

## Tech Stack

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **MongoDB** - Database
- **Mongoose** - ODM
- **JWT** - Authentication
- **bcryptjs** - Password hashing
- **Socket.io** - Real-time communication
- **PDFKit** - PDF generation

### Frontend
- **React** - UI framework
- **React Router** - Navigation
- **Zustand** - State management
- **Axios** - HTTP client
- **Socket.io Client** - Real-time communication
- **React Icons** - Icon library
- **Date-fns** - Date utilities
- **React Quill** - Rich text editor
- **React DatePicker** - Date selection

## Installation

### Prerequisites
- Node.js (v14 or higher)
- npm or yarn
- MongoDB (local or cloud)

### Setup

1. **Clone the repository**
```bash
git clone <repository-url>
cd MERN-TODO-APP
```

2. **Backend Setup**
```bash
cd server
npm install
cp .env.example .env
# Edit .env file with your MongoDB URI and JWT secret
npm run dev
```

3. **Frontend Setup**
```bash
cd client
npm install
npm start
```

The application will be available at `http://localhost:3000`

## Environment Variables

### Server (.env)
```
PORT=5000
MONGODB_URI=mongodb://localhost:27017/mern-todo
JWT_SECRET=your_jwt_secret_key_here
JWT_EXPIRE=7d
NODE_ENV=development
CLIENT_URL=http://localhost:3000
```

### Client (.env)
```
REACT_APP_API_URL=http://localhost:5000
```

## Project Structure

```
MERN-TODO-APP/
├── server/
│   ├── models/
│   │   ├── User.js
│   │   ├── Todo.js
│   │   ├── Category.js
│   │   └── SharedTodo.js
│   ├── routes/
│   │   ├── auth.js
│   │   ├── todos.js
│   │   ├── categories.js
│   │   ├── shared.js
│   │   └── export.js
│   ├── middleware/
│   │   └── auth.js
│   ├── socket/
│   │   └── socketHandlers.js
│   ├── server.js
│   └── package.json
├── client/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Header.js
│   │   │   ├── Sidebar.js
│   │   │   ├── TodoForm.js
│   │   │   ├── TodoList.js
│   │   │   ├── TodoItem.js
│   │   │   ├── FilterBar.js
│   │   │   └── Dashboard.js
│   │   ├── pages/
│   │   │   ├── LoginPage.js
│   │   │   ├── RegisterPage.js
│   │   │   └── Dashboard.js
│   │   ├── store/
│   │   │   └── index.js
│   │   ├── styles/
│   │   ├── App.js
│   │   └── index.js
│   ├── public/
│   ├── package.json
│   └── .gitignore
└── README.md
```

## API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/me` - Get current user
- `PUT /api/auth/profile` - Update user profile

### Todos
- `GET /api/todos` - Get all todos with filters
- `POST /api/todos` - Create new todo
- `GET /api/todos/:id` - Get single todo
- `PUT /api/todos/:id` - Update todo
- `DELETE /api/todos/:id` - Delete todo
- `POST /api/todos/:id/subtask` - Add subtask
- `PUT /api/todos/:id/subtask/:subtaskId` - Update subtask
- `DELETE /api/todos/:id/subtask/:subtaskId` - Delete subtask
- `GET /api/todos/stats/dashboard` - Get dashboard stats

### Categories
- `GET /api/categories` - Get all categories
- `POST /api/categories` - Create category
- `PUT /api/categories/:id` - Update category
- `DELETE /api/categories/:id` - Delete category

### Shared Todos
- `POST /api/shared/share` - Share todo with user
- `GET /api/shared/received` - Get shared todos
- `DELETE /api/shared/:sharedTodoId` - Remove share

### Export
- `GET /api/export/json` - Export todos as JSON
- `GET /api/export/csv` - Export todos as CSV
- `GET /api/export/pdf` - Export todos as PDF

## Socket Events

### Client → Server
- `user-connect` - User connects to socket
- `todo-updated` - Todo is updated
- `todo-created` - Todo is created
- `todo-deleted` - Todo is deleted
- `todo-shared` - Todo is shared
- `task-completed` - Task is completed
- `shared-todo-updated` - Shared todo is updated

### Server → Client
- Same events above are emitted to relevant users

## Usage

### Create a Todo
1. Click "New Task" button
2. Fill in the task details (title, description, category, priority, due date, tags)
3. Click "Create Task"

### Manage Todos
- **Complete**: Click the checkbox next to the task
- **Edit**: Click the edit button
- **Delete**: Click the trash button
- **Filter**: Use the filter bar to search and sort tasks
- **Share**: Click share to collaborate with others

### Use Dashboard
- View task statistics
- Monitor completion rate
- Track overdue tasks
- Analyze productivity trends

### Export Data
- Go to export options
- Choose format (JSON, CSV, PDF)
- Download your todos

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## Future Enhancements

- [ ] Time tracking
- [ ] Pomodoro timer integration
- [ ] Multi-language support
- [ ] Mobile app (React Native)
- [ ] Calendar view
- [ ] Kanban board view
- [ ] Team workspaces
- [ ] Advanced analytics
- [ ] AI-powered task suggestions
- [ ] Voice commands

## License

MIT License - feel free to use this project for personal or commercial use.

## Support

For support, email support@todosapp.com or open an issue in the repository.

---

Made with ❤️ by the Todo Team
