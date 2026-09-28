# 🗄️ MongoDB Setup Guide

## ✅ Current Status
- ✅ **Backend Server**: Running on port 5000
- ✅ **Frontend Server**: Running on port 3000
- ❌ **Database**: MongoDB not connected (local installation failed)

---

## 🚀 Solution: MongoDB Atlas (Free Cloud Database)

Since local MongoDB installation isn't available, we'll use **MongoDB Atlas** - the official managed MongoDB cloud service. It's **100% free** for development.

### Step 1: Create MongoDB Atlas Account

1. **Go to**: https://www.mongodb.com/cloud/atlas
2. **Click**: "Try Free" button
3. **Sign up** with your email (or GitHub)
4. **Verify** your email address

---

### Step 2: Create a Free Cluster

1. **Login** to MongoDB Atlas
2. **Click**: "Create" → "New Project"
3. **Project Name**: `MERN-TODO-APP`
4. **Click**: "Create Project"
5. **Click**: "Create" → "Cluster"
6. **Choose**: Shared (Free tier)
7. **Select Region**: Choose closest to you (e.g., `US-East-1`)
8. **Cluster Name**: `mern-cluster`
9. **Click**: "Create Cluster" (wait 2-3 minutes)

---

### Step 3: Configure Database Access

1. **Go to**: "Security" → "Database Access"
2. **Click**: "+ Add New Database User"
3. **Username**: `mern_user`
4. **Password**: Generate a strong password or enter your own
5. **Database User Privileges**: `Read and write to any database`
6. **Click**: "Add User"
7. **Copy and save** the username and password somewhere safe

---

### Step 4: Configure Network Access

1. **Go to**: "Security" → "Network Access"
2. **Click**: "+ Add IP Address"
3. **Access From**: `0.0.0.0/0` (Allow access from anywhere - OK for development)
4. **Click**: "Confirm"

---

### Step 5: Get Connection String

1. **Go to**: "Databases"
2. **Click**: "Connect" on your cluster
3. **Choose**: "Drivers" → "Node.js"
4. **Copy the connection string**
   - It looks like: `mongodb+srv://mern_user:password@mern-cluster.xxxxx.mongodb.net/?retryWrites=true&w=majority`

---

### Step 6: Update `.env` File

Update the `.env` file in your server directory:

```bash
# Old (local MongoDB)
MONGODB_URI=mongodb://localhost:27017/mern-todo

# New (MongoDB Atlas)
MONGODB_URI=mongodb+srv://mern_user:YOUR_PASSWORD@mern-cluster.xxxxx.mongodb.net/mern-todo?retryWrites=true&w=majority
JWT_SECRET=your_secure_jwt_secret_key_12345
JWT_EXPIRE=7d
PORT=5000
CLIENT_URL=http://localhost:3000
NODE_ENV=development
```

**Replace:**
- `YOUR_PASSWORD` with your actual password
- `mern-cluster.xxxxx` with your actual cluster name

---

### Step 7: Restart Backend Server

```powershell
# In the terminal where backend is running, press Ctrl+C to stop
# Then restart with:
cd server
npm start
```

---

## ✅ Quick Test After Setup

```powershell
# Test Registration
$body = @{
    name = "Test User"
    email = "test@example.com"
    password = "Test@123"
} | ConvertTo-Json

Invoke-RestMethod -Uri "http://localhost:5000/api/auth/register" `
  -Method POST -Body $body -ContentType "application/json"
```

If you see a response with `userId`, `token`, and `user` data - **Success! ✅**

---

## 📚 Alternative: Local MongoDB (Requires Admin)

If you prefer local MongoDB and can run as Administrator:

1. Download: https://www.mongodb.com/try/download/community
2. Run installer with **Administrator privileges**
3. Choose "Install as a Service"
4. After installation, MongoDB will auto-start
5. Verify with: `mongod --version`

---

## 🔗 Useful MongoDB Atlas Links

- **Dashboard**: https://cloud.mongodb.com
- **Documentation**: https://docs.mongodb.com/atlas/
- **Connection String Help**: https://docs.mongodb.com/atlas/driver-connection

---

## 💡 Troubleshooting

### "Connection Timed Out"
- Check your IP address is whitelisted in "Network Access"
- Verify password is correct
- Ensure internet connection is working

### "Authentication Failed"
- Double-check username and password in connection string
- Verify user has correct privileges (Read/Write)

### "Connection String Not Working"
- Copy exact connection string from Atlas dashboard
- Replace `<password>` with actual password
- Don't wrap in quotes

---

## 🎯 Next Steps

1. ✅ Create MongoDB Atlas account
2. ✅ Get connection string
3. ✅ Update `.env` with connection string
4. ✅ Restart backend server
5. ✅ Run test registration (see above)
6. ✅ Create test data (see IMPORT_TEST_DATA.md)
