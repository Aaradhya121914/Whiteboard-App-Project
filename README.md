# WhiteSync - Collaborative Whiteboard App Project Documentation
## Overview
WhiteSync is a full-stack collaborative whiteboard application with real-time canvas editing, user authentication, and canvas management features.

Project Structure

White-Board-App/
├── Backend/
│   ├── controllers/
│   │   ├── canvasController.js
│   │   └── userController.js
│   ├── middlewares/
│   │   ├── authorization.js
│   │   └── validation.js
│   ├── models/
│   │   ├── canvasModel.js
│   │   ├── otpModel.js
│   │   └── userModel.js
│   ├── routes/
│   │   ├── canvasRoutes.js
│   │   └── userRoutes.js
│   ├── .env
│   ├── db.js
│   ├── index.js
│   ├── package-lock.json
│   └── package.json
├── Frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Authentication/
│   │   │   │   ├── index.css
│   │   │   │   └── index.js
│   │   │   ├── Board/
│   │   │   │   ├── index.js
│   │   │   │   └── index.module.css
│   │   │   ├── Dashboard/
│   │   │   │   ├── index.css
│   │   │   │   └── index.js
│   │   │   ├── Toolbox/
│   │   │   │   ├── index.js
│   │   │   │   └── index.module.css
│   │   │   └── VerifyEmail.js
│   │   ├── store/
│   │   │   ├── board-context.js
│   │   │   ├── board-provider.js
│   │   │   ├── toolbox-context.js
│   │   │   └── toolbox-provider.js
│   │   ├── utils/
│   │   │   ├── api.js
│   │   │   ├── element.js
│   │   │   └── math.js
│   │   ├── constants.js
│   │   ├── App.js
│   │   ├── App.css
│   │   └── index.js
│   ├── public/
│   ├── package.json
│   ├── tailwind.config.js
│   └── postcss.config.js
└── package-lock.json

## Backend Components
### 1. Models (Backend/models/)
- userModel.js : Defines user schema (name, email, password, isVerified, timestamps) with static methods for creating, logging in, and retrieving users.
- canvasModel.js : Defines canvas schema (owner, shared_with, elements, name, timestamps) with static methods for CRUD operations and sharing.
- otpModel.js : Temporary storage for email verification codes (expires after 10 minutes).
### 2. Controllers (Backend/controllers/)
- userController.js : Handles user registration, email verification, login, and Google OAuth login.
- canvasController.js : Handles canvas creation, deletion, update, retrieval, and sharing.
### 3. Middleware (Backend/middlewares/)
- authorization.js : Verifies JWT tokens for protected routes.
- validation.js : Validates registration form inputs using express-validator.
### 4. Routes (Backend/routes/)
- userRoutes.js : /login , /register , /verify , /google-login , /user
- canvasRoutes.js : / , /create , /delete , /update , /:id , /share/:id (all protected)
### 5. Entry Files
- db.js : Connects to MongoDB (fix: uses MONGODB_URI instead of MONGO_URI ).
- index.js : Initializes Express server, Socket.IO for real-time updates, CORS, and routes.
## Frontend Components
### 1. Pages & Components (Frontend/src/components/)
- Authentication/index.js : Login/Signup form with Google OAuth button.
- VerifyEmail.js : Email verification page (uses OTP sent via Resend).
- Dashboard/index.js : Lists user's canvases, allows creating, deleting, and sharing canvases.
- Board/index.js : Main canvas drawing interface with real-time sync.
- Toolbox/index.js : Color, fill, and size controls for active tool.
- Toolbar/index.js : Tool selector (brush, line, rect, circle, arrow, eraser, text, undo, redo, download).
### 2. State Management (Frontend/src/store/)
- board-context.js / board-provider.js : Manages canvas elements, drawing history, tool selection, and real-time sync via Socket.IO.
- toolbox-context.js / toolbox-provider.js : Manages tool properties (stroke, fill, size) per tool.
### 3. Utilities (Frontend/src/utils/)
- api.js : API call to update canvas on server.
- element.js : Creates rough.js elements, checks point proximity for eraser, converts brush points to SVG path.
- math.js : Calculates arrow coordinates, distances between points.
### 4. Constants (Frontend/src/constants.js)
- Tool types, board actions, action types, colors, config types, toolbox actions, and thresholds.
## Key Features
1. User Authentication : Email/password (with verification) + Google OAuth login.
2. Canvas Management : Create, delete, share canvases.
3. Drawing Tools : Brush, line, rectangle, circle, arrow, eraser, text.
4. Customization : Stroke color, fill color, brush size, font size.
5. History : Undo/Redo functionality.
6. Real-time Collaboration : Socket.IO for live canvas sync across users.
7. Download : Save canvas as JPEG image.
## Environment Variables (Backend/.env)
## Setup Instructions
1. Backend Setup :
   - cd Backend
   - npm install
   - Create .env with above variables
   - Fix db.js line 8: process.env.MONGODB_URI
   - npm run dev (uses nodemon) or npm start
2. Frontend Setup :
   - cd Frontend
   - npm install
   - Replace all Render URLs in frontend files with http://localhost:5000
   - Update GOOGLE_CLIENT_ID in Frontend/src/index.js
   - npm start
3. Google Cloud Setup :
   - Create OAuth Client ID in Google Cloud Console
   - Add http://localhost:3000 to Authorized JavaScript Origins
