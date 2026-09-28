# 🎯 Complete Feature Documentation

## 1. Task Management

### Create Task
```javascript
POST /api/todos
{
  "title": "Task title",
  "description": "Detailed description",
  "category": "category_id",
  "priority": "high|medium|low",
  "dueDate": "2024-12-31T23:59:59Z",
  "reminders": ["1day", "1hour"],
  "tags": ["work", "urgent"],
  "recurring": {
    "enabled": true,
    "frequency": "daily|weekly|monthly|yearly",
    "endDate": "2024-12-31"
  }
}
```

### Task Priorities
- **High**: Red indicator, top in listings
- **Medium**: Orange indicator, normal priority
- **Low**: Green indicator, lower priority

### Task Status
- ✅ Completed (greyed out, strikethrough)
- ⏳ Pending (full opacity, highlighted if overdue)
- ⏰ Overdue (red left border, warning)

## 2. Categories

### Features
- Custom names
- Custom colors (hex)
- Icons (emoji support)
- Descriptions
- Organize todos by category
- Filter by category

### Example
```javascript
{
  "name": "Work",
  "color": "#3498db",
  "icon": "💼",
  "description": "Work-related tasks"
}
```

## 3. Tagging System

### Features
- Unlimited tags per task
- Search by tags
- Filter by multiple tags
- Tag suggestions
- Tag autocomplete

### Usage
- Type comma-separated tags in form
- Click tag badge to filter
- Search includes tag matching

## 4. Priority Management

### Display
- Visual color indicators
- Badge with priority level
- Sort by priority (High → Low)
- Filter by specific priority

### Integration
- Used in sorting
- Filters available
- Dashboard statistics
- Overdue calculation

## 5. Due Dates & Deadlines

### Features
- Date picker UI
- Time selection
- Relative time display (e.g., "in 2 days")
- Overdue detection
- Visual warnings

### Display
- "in 2 hours"
- "3 days ago" (if overdue)
- Red border if overdue
- Calendar icon

## 6. Reminders

### Options
- 5 minutes before
- 15 minutes before
- 1 hour before
- 1 day before
- 1 week before
- Custom times

### Implementation
- Browser notifications
- Email notifications (future)
- In-app notifications
- Socket.io real-time

## 7. Recurring Tasks

### Frequencies
- Daily
- Weekly (specific day)
- Monthly (specific date)
- Yearly (specific month/date)

### Settings
```javascript
{
  "enabled": true,
  "frequency": "weekly",
  "endDate": "2025-12-31"
}
```

### Behavior
- Auto-creates next instance when completed
- Stops on end date
- Can skip individual occurrences

## 8. Subtasks

### Features
- Create subtasks within tasks
- Track subtask completion
- Visual progress indicator
- Edit individual subtasks
- Delete subtasks

### API Endpoints
```
POST /api/todos/:id/subtask
PUT /api/todos/:id/subtask/:subtaskId
DELETE /api/todos/:id/subtask/:subtaskId
```

### Display
- Shows "2/5 subtasks complete"
- Nested indentation
- Individual checkboxes

## 9. Search & Filtering

### Search
- Full-text search on title & description
- Real-time filtering
- Case-insensitive

### Filters
- By completion status (Active/Completed)
- By priority (High/Medium/Low)
- By category
- By tags (multiple selection)
- By date range

### Sorting
- By due date (ascending)
- By priority (descending)
- By creation date (newest)
- By completion status

## 10. Real-time Updates

### Socket Events
```
user-connect
todo-created
todo-updated
todo-deleted
task-completed
todo-shared
shared-todo-updated
```

### Features
- Instant UI updates
- Multiple device sync
- Collaborative editing
- Live notifications
- Connection status

## 11. Collaboration & Sharing

### Share Permissions
- **View**: Read-only access
- **Edit**: Can modify and complete

### Features
- Share with specific users
- Revoke access
- Change permissions
- See who shared with you
- Accept/reject shared todos

### API
```
POST /api/shared/share {todoId, userId, permission}
GET /api/shared/received
DELETE /api/shared/:id
```

## 12. Dashboard & Statistics

### Metrics
- Total tasks count
- Completed tasks count
- Pending tasks count
- Overdue tasks count
- Completion percentage

### Visualizations
- Progress bars
- Stat cards with icons
- Completion rate gauge
- Task status breakdown

### Updates
- Real-time stats
- Auto-refresh every minute
- Manual refresh option

## 13. Data Export

### JSON Export
```json
{
  "exportedAt": "2024-01-01T00:00:00Z",
  "totalTodos": 42,
  "todos": [...]
}
```

### CSV Export
Columns: Title, Description, Category, Priority, Completed, Due Date, Tags

### PDF Export
- Professional format
- Page breaks for large exports
- Formatted table layout
- Export date included
- Task details included

### Features
- Batch export all
- Download with timestamp
- Preserves all metadata
- Ready for sharing

## 14. Dark Mode

### Features
- Toggle button in header
- Persistent preference
- System preference detection
- Smooth transitions
- All components themed

### Implementation
- CSS variables for colors
- `.dark-theme` class on body
- LocalStorage persistence
- Real-time switching

### Colors
- Light: #f5f5f5 background
- Dark: #1a1a1a background
- Readable contrast in both

## 15. User Authentication

### Register
```javascript
POST /api/auth/register
{
  "name": "User Name",
  "email": "email@example.com",
  "password": "secure_password"
}
```

### Login
```javascript
POST /api/auth/login
{
  "email": "email@example.com",
  "password": "password"
}
```

### Security
- Passwords hashed with bcrypt (10 salt rounds)
- JWT tokens (7-day expiry)
- Protected routes with middleware
- Secure headers

## 16. User Profile

### Settings
- Display name
- Email address
- Theme preference (light/dark)
- Notification settings
- Avatar URL

### Update Profile
```javascript
PUT /api/auth/profile
{
  "name": "New Name",
  "theme": "dark",
  "notificationsEnabled": true
}
```

## 17. Responsive Design

### Breakpoints
- Mobile: < 600px
- Tablet: 600px - 768px
- Desktop: > 768px

### Adaptations
- Stacked layout on mobile
- Collapsible sidebar
- Touch-friendly buttons
- Optimized spacing

## 18. Performance Features

### Optimization
- Lazy loading components
- Debounced search
- Efficient re-renders
- Local caching
- API response caching

### Database
- Indexed queries
- Optimized schema
- Connection pooling
- Query optimization

## 19. Accessibility

### Features
- Semantic HTML
- ARIA labels
- Keyboard navigation
- Color contrast compliance
- Screen reader support

## 20. Error Handling

### Client
- User-friendly error messages
- Retry mechanisms
- Form validation
- API error catching

### Server
- Request validation
- Error logging
- Appropriate HTTP status codes
- Error response formatting

---

## 🚀 Usage Examples

### Create Task with All Features
```bash
curl -X POST http://localhost:5000/api/todos \
  -H "Authorization: Bearer token" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Q1 Planning",
    "description": "Plan Q1 objectives",
    "category": "work_id",
    "priority": "high",
    "dueDate": "2024-03-31T17:00:00Z",
    "reminders": ["1day"],
    "tags": ["planning", "strategic"],
    "recurring": {
      "enabled": false
    }
  }'
```

### Search Tasks
```bash
curl http://localhost:5000/api/todos?search=planning&priority=high&sortBy=dueDate
```

### Export Data
```bash
# JSON
curl http://localhost:5000/api/export/json -H "Authorization: Bearer token" > todos.json

# CSV
curl http://localhost:5000/api/export/csv -H "Authorization: Bearer token" > todos.csv

# PDF
curl http://localhost:5000/api/export/pdf -H "Authorization: Bearer token" > todos.pdf
```

---

## 🔜 Future Enhancements

- [ ] Time tracking with Pomodoro
- [ ] Voice commands
- [ ] AI task suggestions
- [ ] Team workspaces
- [ ] Calendar view
- [ ] Kanban board view
- [ ] Mobile app (React Native)
- [ ] Advanced analytics
- [ ] Webhook integrations
- [ ] Third-party calendar sync

---

Last Updated: January 2024
