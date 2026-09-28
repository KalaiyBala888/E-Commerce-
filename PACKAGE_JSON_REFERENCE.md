// ==================== COMPLETE PACKAGE.JSON ====================
// File: server/package.json

{
  "name": "mern-todo-server",
  "version": "1.0.0",
  "description": "MERN Stack Todo Application - Backend Server",
  "main": "server.js",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js",
    "test": "jest",
    "test:watch": "jest --watch"
  },
  "keywords": [
    "todo",
    "mern",
    "express",
    "mongodb",
    "nodejs"
  ],
  "author": "Your Name",
  "license": "MIT",
  "dependencies": {
    "express": "^4.18.2",
    "mongoose": "^7.1.0",
    "bcryptjs": "^2.4.3",
    "jsonwebtoken": "^9.0.0",
    "cors": "^2.8.5",
    "dotenv": "^16.0.3",
    "socket.io": "^4.6.1",
    "express-validator": "^7.0.0",
    "pdfkit": "^0.13.0",
    "nodemailer": "^6.9.1"
  },
  "devDependencies": {
    "nodemon": "^2.0.22",
    "jest": "^29.5.0",
    "supertest": "^6.3.3"
  },
  "engines": {
    "node": ">=14.0.0",
    "npm": ">=6.0.0"
  }
}

// ==================== COMPLETE PACKAGE.JSON ====================
// File: client/package.json

{
  "name": "mern-todo-client",
  "version": "1.0.0",
  "description": "MERN Stack Todo Application - Frontend Client",
  "homepage": ".",
  "private": true,
  "proxy": "http://localhost:5000",
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-router-dom": "^6.11.0",
    "react-scripts": "5.0.1",
    "zustand": "^4.3.7",
    "socket.io-client": "^4.6.1",
    "axios": "^1.3.5",
    "date-fns": "^2.29.3",
    "react-icons": "^4.8.0",
    "react-datepicker": "^4.11.0",
    "react-quill": "^2.0.0",
    "classnames": "^2.3.2"
  },
  "devDependencies": {
    "@testing-library/react": "^13.4.0",
    "@testing-library/jest-dom": "^5.16.5",
    "@testing-library/user-event": "^13.5.0"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
  "engines": {
    "node": ">=14.0.0",
    "npm": ">=6.0.0"
  }
}
