# MERN Todo App - Quick Start

## 🚀 Get Running in 5 Minutes

### Prerequisites
- Node.js installed
- MongoDB running locally OR MongoDB Atlas account

### 1️⃣ Backend Setup
```bash
cd server
npm install
# Edit .env file:
# MONGODB_URI=mongodb://localhost:27017/mern-todo
# JWT_SECRET=super_secret_key
npm run dev
```
✅ Backend running at http://localhost:5000

### 2️⃣ Frontend Setup (new terminal)
```bash
cd client
npm install
npm start
```
✅ Frontend running at http://localhost:3000

### 3️⃣ Test the App
- Register new account
- Create a todo
- Try filtering, editing, deleting
- Toggle dark mode
- Export data

## 📋 All Features at a Glance

| Feature | Status | Used In |
|---------|--------|---------|
| Create/Edit/Delete Todos | ✅ | TodoForm, TodoItem |
| Categories & Tags | ✅ | TodoForm, FilterBar |
| Priority Levels | ✅ | TodoForm, TodoItem |
| Due Dates & Reminders | ✅ | TodoForm, Dashboard |
| Subtasks | ✅ | TodoForm, TodoItem |
| Search & Filter | ✅ | FilterBar |
| Sorting | ✅ | FilterBar |
| Dark Mode | ✅ | Header, Stores |
| Dashboard Stats | ✅ | Dashboard Component |
| Real-time Updates | ✅ | Socket.io Integration |
| Share Todos | ✅ | ShareTodo Routes |
| Export (JSON/CSV/PDF) | ✅ | Export Routes |
| User Auth (JWT) | ✅ | Auth Routes |
| Responsive Design | ✅ | All Styles |

## 🔌 API Quick Reference

### Auth
- `POST /api/auth/register` - Sign up
- `POST /api/auth/login` - Sign in
- `GET /api/auth/me` - Get profile

### Todos
- `POST /api/todos` - Create
- `GET /api/todos` - List (with filters)
- `PUT /api/todos/:id` - Update
- `DELETE /api/todos/:id` - Delete

### Categories
- `POST /api/categories` - Create
- `GET /api/categories` - List
- `PUT /api/categories/:id` - Update
- `DELETE /api/categories/:id` - Delete

### Export
- `GET /api/export/json` - Export as JSON
- `GET /api/export/csv` - Export as CSV
- `GET /api/export/pdf` - Export as PDF

## 🎨 Customize

### Change Colors
Edit `/client/src/styles/index.css`:
```css
:root {
  --primary: #3498db;      /* Main color */
  --secondary: #2c3e50;    /* Secondary */
  --success: #27ae60;      /* Success */
  --danger: #e74c3c;       /* Danger */
}
```

### Add New Category Types
Edit `/server/models/Category.js` and add to schema

### Extend TodoForm
Edit `/client/src/components/TodoForm.js` to add new fields

## 🐛 Common Issues

| Issue | Solution |
|-------|----------|
| MongoDB connection error | Check `MONGODB_URI` in .env |
| Port 5000 in use | Change `PORT` in .env |
| API not responding | Ensure backend is running on :5000 |
| Blank React page | Check console (F12), clear cache |

## 📱 Responsive Design

- ✅ Desktop (1024px+)
- ✅ Tablet (768px - 1023px)
- ✅ Mobile (< 768px)

## 🔐 Security Notes

- JWT tokens expire in 7 days
- Passwords hashed with bcrypt
- Environment variables keep secrets safe
- Always use HTTPS in production

## 🚢 Deploy

### Deploy Backend
- Heroku, Railway, Vercel
- Set env variables on platform
- Use MongoDB Atlas

### Deploy Frontend
- Netlify, Vercel
- Build: `npm run build`
- Deploy `/build` folder

## 📚 Learn More

- [Express.js](https://expressjs.com)
- [React](https://react.dev)
- [MongoDB](https://www.mongodb.com)
- [Socket.io](https://socket.io)
- [JWT](https://jwt.io)

## 💡 Next Steps

1. ✅ Get running
2. 📝 Create your first todo
3. 🎨 Customize colors
4. 📦 Add more features
5. 🚀 Deploy!

---

**Questions?** Check SETUP_GUIDE.md or README.md
