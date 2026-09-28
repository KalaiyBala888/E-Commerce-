# Development & Testing Guide

## 🧪 Testing

### Manual Testing Checklist

#### Authentication
- [ ] Register new account
- [ ] Login with credentials
- [ ] Logout clears session
- [ ] Expired token handled
- [ ] Profile update works

#### Todo CRUD
- [ ] Create new todo
- [ ] Edit todo details
- [ ] Complete/uncomplete todo
- [ ] Delete todo (with confirmation)
- [ ] Add subtasks
- [ ] Edit subtasks
- [ ] Delete subtasks

#### Filtering & Search
- [ ] Search by title
- [ ] Search by description
- [ ] Filter by status (Active/Completed)
- [ ] Filter by priority
- [ ] Filter by category
- [ ] Sort by due date
- [ ] Sort by priority
- [ ] Multiple filters together

#### Categories
- [ ] Create category
- [ ] Assign to todo
- [ ] Edit category
- [ ] Delete category
- [ ] Filter by category

#### Reminders
- [ ] Set reminders
- [ ] Multiple reminders per task
- [ ] Reminders display correctly

#### Sharing
- [ ] Share todo with user
- [ ] Share with view permission
- [ ] Share with edit permission
- [ ] Accept shared todos
- [ ] Receive notifications

#### Export
- [ ] Export as JSON
- [ ] Export as CSV
- [ ] Export as PDF
- [ ] Open exported files
- [ ] Data integrity in export

#### UI/UX
- [ ] Dark mode toggle
- [ ] Responsive on mobile
- [ ] Responsive on tablet
- [ ] Keyboard navigation
- [ ] Smooth animations
- [ ] Loading states
- [ ] Error messages

#### Performance
- [ ] App loads in < 2s
- [ ] Filters respond instantly
- [ ] No memory leaks
- [ ] Smooth scrolling

## 🔧 Development Setup

### Recommended Tools

1. **VSCode Extensions**
   - ES7+ React/Redux/React-Native snippets
   - MongoDB for VSCode
   - Thunder Client or REST Client
   - Git Lens

2. **Browser Tools**
   - React Developer Tools
   - Redux DevTools (if using Redux)
   - Network tab (F12 > Network)
   - Console (F12 > Console)

3. **Desktop Apps**
   - MongoDB Compass (for database)
   - Postman (for API testing)
   - VS Code

### Debugging Tips

#### Frontend
```javascript
// Add console logs
console.log('Data:', todo);

// Use React DevTools
// Inspect component props and state

// Check Network tab
// Monitor API requests/responses

// Check Console for errors
// Fix warnings for performance
```

#### Backend
```javascript
// Add logging
console.log('Creating todo:', req.body);

// Use MongoDB Compass
// View data in real-time

// Use Postman
// Test endpoints with different payloads

// Monitor server logs
// Check for errors during requests
```

## 📊 Database Queries

### MongoDB Compass

```javascript
// Count todos
db.todos.countDocuments({ userId: ObjectId("...") })

// Find pending tasks
db.todos.find({ completed: false, userId: ObjectId("...") })

// Find overdue tasks
db.todos.find({ 
  dueDate: { $lt: new Date() },
  completed: false
})

// Find by category
db.todos.find({ category: ObjectId("...") })

// Count by priority
db.todos.aggregate([
  { $match: { userId: ObjectId("...") } },
  { $group: { _id: "$priority", count: { $sum: 1 } } }
])
```

## 🚀 Performance Tips

### Frontend Optimization
```javascript
// Use React.memo for expensive components
const TodoItem = React.memo(({ todo }) => (...))

// Lazy load routes
const Dashboard = lazy(() => import('./pages/Dashboard'))

// Debounce search input
const debouncedSearch = debounce(handleSearch, 300)

// Use useCallback for stable functions
const handleClick = useCallback(() => {...}, [])
```

### Backend Optimization
```javascript
// Add database indexes
TodoSchema.index({ userId: 1, createdAt: -1 })

// Use select() to limit fields
Todo.find().select('title priority completed')

// Paginate large results
const todos = await Todo.find().limit(20).skip(pageNum * 20)

// Use lean() for read-only queries
Todo.find().lean()
```

## 📝 Code Style Guide

### Component Structure
```javascript
import React, { useState } from 'react';
import { useStore } from '../store';
import '../styles/component.css';

function ComponentName({ prop1, prop2 }) {
  const [state, setState] = useState('');
  const { data } = useStore();

  const handleClick = () => {
    // Logic here
  };

  return (
    <div className="container">
      {/* JSX here */}
    </div>
  );
}

export default ComponentName;
```

### File Naming
- Components: `PascalCase` (e.g., `TodoItem.js`)
- Utils: `camelCase` (e.g., `helpers.js`)
- Styles: `lowercase` (e.g., `todoitem.css`)
- Routes: `camelCase` (e.g., `todos.js`)

### CSS Naming
- BEM: `.component__element--modifier`
- Example: `.todo-item__title--completed`

## 🐛 Common Development Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| API 404 errors | Wrong endpoint | Check route in server |
| CORS errors | Frontend/backend mismatch | Set CLIENT_URL in .env |
| Styles not loading | CSS import path | Check path is correct |
| State not updating | Zustand not subscribed | Verify store usage |
| Slow queries | Missing indexes | Add indexes to schema |

## 📦 Adding New Dependencies

### Backend
```bash
cd server
npm install package-name
# Update package.json automatically
```

### Frontend
```bash
cd client
npm install package-name
# Update package.json automatically
```

## 🔄 Git Workflow

```bash
# Create feature branch
git checkout -b feature/task-name

# Make changes and commit
git add .
git commit -m "Add feature: description"

# Push to remote
git push origin feature/task-name

# Create pull request on GitHub
```

## 📋 PR Checklist

Before submitting a PR:
- [ ] Code follows project style
- [ ] Tests pass locally
- [ ] No console errors/warnings
- [ ] Comments added where needed
- [ ] README updated if needed
- [ ] No sensitive data in commit

## 🚢 Pre-deployment Checklist

### Backend
- [ ] Remove console.log() statements
- [ ] Set NODE_ENV=production
- [ ] Update .env with production values
- [ ] Run all tests
- [ ] Check database backups
- [ ] Enable CORS for production domain
- [ ] Set secure JWT_SECRET

### Frontend
- [ ] Run build: `npm run build`
- [ ] Check bundle size
- [ ] Test all features
- [ ] Remove debug code
- [ ] Update API URL
- [ ] Test on multiple browsers

## 📞 Support & Documentation

- Inline comments for complex logic
- JSDoc for functions
- README for setup
- API documentation
- Architecture diagrams (future)

---

## 🎓 Learning Resources

- [React Patterns](https://reactpatterns.com/)
- [Express Best Practices](https://expressjs.com/en/advanced/best-practice-performance.html)
- [MongoDB Performance](https://docs.mongodb.com/manual/administration/analyzing-mongodb-performance/)
- [Socket.io Guide](https://socket.io/docs/v4/socket-io-protocol/)

Happy coding! 💻
