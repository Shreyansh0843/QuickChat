# 💬 EchoChat - Real-Time MERN Stack Chat Application

A comprehensive full-stack real-time messaging platform built with the MERN stack and Socket.io, enabling instant communication with user authentication, profile management, and image sharing capabilities.

![MERN Stack](https://img.shields.io/badge/Stack-MERN-green)
![Socket.io](https://img.shields.io/badge/Real--time-Socket.io-blue)
![License](https://img.shields.io/badge/License-MIT-blue)
![Node Version](https://img.shields.io/badge/node-%3E%3D14.0.0-brightgreen)

## 📋 Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [System Architecture](#system-architecture)
- [Installation](#installation)
- [Environment Variables](#environment-variables)
- [API Documentation](#api-documentation)
- [Project Structure](#project-structure)
- [Usage Guide](#usage-guide)
- [Screenshots](#screenshots)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)
- [License](#license)

## ✨ Features

### 💬 Real-Time Messaging
- **Instant Message Delivery**: Socket.io-powered real-time message synchronization
- **Message Status Tracking**: See when messages are delivered and read
- **Typing Indicators**: Real-time typing status display
- **Unseen Message Count**: Track unread messages across conversations
- **Image Sharing**: Upload and share images in conversations via Cloudinary
- **Message Timestamps**: Automatic timestamp generation for all messages

### 👤 User Management
- **Secure Authentication**: JWT-based registration and login system
- **Profile Creation**: Customizable user profiles with name and bio
- **Profile Pictures**: Upload and manage profile pictures with Cloudinary
- **Online Status**: Real-time online/offline status indicators
- **User Search**: Search functionality to find and connect with users
- **User Discovery**: Browse all registered users

### 🎨 User Experience
- **Responsive Design**: Mobile-first design with Tailwind CSS
- **Dynamic UI**: Conditional rendering based on user selection
- **Smooth Scrolling**: Auto-scroll to latest messages with smooth animations
- **Toast Notifications**: Real-time feedback for user actions
- **Profile Navigation**: Easy access to user profiles and settings
- **Status Indicators**: Visual indicators for online/offline and message status

### 🔐 Security & Performance
- **JWT Authentication**: Secure token-based authentication
- **Password Encryption**: Bcrypt-based password hashing
- **Protected Routes**: Authentication middleware for secured endpoints
- **Real-time Synchronization**: Efficient Socket.io event handling
- **Context-Based State**: Optimized global state management
- **Local Storage Persistence**: Maintain authentication across sessions

## 🛠️ Tech Stack

### Frontend
- **React.js**: Component-based UI development with functional components
- **React Router**: Client-side routing and navigation
- **Context API**: Global state management for users, messages, and authentication
- **Tailwind CSS**: Utility-first CSS framework for responsive design
- **Axios**: HTTP client for API requests
- **React Toastify**: User notification system
- **Socket.io Client**: Real-time WebSocket communication

### Backend
- **Node.js**: JavaScript runtime environment
- **Express.js**: Web application framework
- **MongoDB**: NoSQL database for users and messages
- **Mongoose**: MongoDB object modeling and validation
- **Socket.io**: Real-time bidirectional event-based communication
- **JWT**: JSON Web Token for authentication
- **Bcrypt**: Password hashing library

### Third-Party Services
- **Cloudinary**: Cloud-based image upload and storage
- **MongoDB Atlas**: Cloud database hosting
- **Vercel**: Deployment platform for frontend and backend

## 🏗️ System Architecture

### Real-Time Communication Flow

```
Client 1 → Socket.io Client → Socket.io Server → Socket.io Client → Client 2
    ↓                              ↓                                    ↓
React UI              Express.js + MongoDB                        React UI
```

### Authentication Flow

```
User Registration → Password Hash → MongoDB Storage
User Login → Password Verify → JWT Token → Local Storage → Protected Routes
```

### Message Flow

```
User Input → Socket Emit → Server Processing → MongoDB Storage → Socket Broadcast → All Connected Clients
```

## 📦 Installation

### Prerequisites
- Node.js (v14 or higher)
- MongoDB Atlas account
- Cloudinary account
- npm or yarn package manager

### Steps

1. **Clone the repository**
```bash
git clone https://github.com/Shreyansh0843/echochat.git
cd echochat
```

2. **Install Backend Dependencies**
```bash
cd backend
npm install
```

3. **Install Frontend Dependencies**
```bash
cd ../frontend
npm install
```

4. **Configure Environment Variables** (see below)

5. **Start MongoDB**
- Ensure MongoDB Atlas connection string is configured
- Database will auto-create collections on first run

6. **Start the Backend Server**
```bash
cd backend
npm run dev
# or
node server.js
```

7. **Start the Frontend**
```bash
cd frontend
npm run dev
```

8. **Access the Application**
- Frontend: `http://localhost:5173`
- Backend: `http://localhost:4000`

## 🔐 Environment Variables

### Backend (.env)
```env
PORT=4000
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret_key

CLOUDINARY_CLOUD_NAME=your_cloudinary_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_secret_key
```

### Frontend (.env)
```env
VITE_BACKEND_URL=http://localhost:4000
```

## 📚 API Documentation

### Authentication Endpoints

#### User Routes
| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/api/user/register` | Register new user with name, email, password | No |
| POST | `/api/user/login` | User login with email and password | No |
| GET | `/api/user/profile` | Get current user profile | Yes |
| POST | `/api/user/update-profile` | Update user profile (name, bio, avatar) | Yes |
| POST | `/api/user/logout` | Logout user and clear session | Yes |

#### Message Routes
| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/api/messages/:userId` | Get all messages with specific user | Yes |
| POST | `/api/messages/send` | Send a new message (text or image) | Yes |
| PUT | `/api/messages/mark-seen/:messageId` | Mark message as seen | Yes |
| GET | `/api/messages/unseen-count` | Get unseen message count | Yes |

#### User Discovery Routes
| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/api/users` | Get all registered users | Yes |
| GET | `/api/users/search?q=query` | Search users by name | Yes |
| GET | `/api/users/online` | Get list of online users | Yes |

### Socket.io Events

#### Client → Server Events
| Event | Payload | Description |
|-------|---------|-------------|
| `setup` | `{ userId }` | Initialize user connection |
| `join_chat` | `{ chatId }` | Join specific chat room |
| `new_message` | `{ receiverId, message, image? }` | Send new message |
| `typing` | `{ chatId }` | User started typing |
| `stop_typing` | `{ chatId }` | User stopped typing |
| `disconnect` | - | User disconnected |

#### Server → Client Events
| Event | Payload | Description |
|-------|---------|-------------|
| `connected` | - | Connection established |
| `message_received` | `{ message }` | New message received |
| `message_seen` | `{ messageId }` | Message marked as seen |
| `user_online` | `{ userId }` | User came online |
| `user_offline` | `{ userId }` | User went offline |
| `typing_indicator` | `{ userId, chatId }` | User is typing |

## 📁 Project Structure

```
echochat/
│
├── backend/
│   ├── config/
│   │   ├── mongodb.js          # Database connection
│   │   ├── cloudinary.js       # Cloudinary configuration
│   │   └── socket.js           # Socket.io setup
│   ├── controllers/
│   │   ├── userController.js   # User authentication & profile
│   │   └── messageController.js # Message handling
│   ├── middleware/
│   │   ├── authMiddleware.js   # JWT verification
│   │   └── multer.js           # File upload handling
│   ├── models/
│   │   ├── userModel.js        # User schema
│   │   └── messageModel.js     # Message schema
│   ├── routes/
│   │   ├── userRoutes.js       # User routes
│   │   └── messageRoutes.js    # Message routes
│   ├── .env
│   ├── server.js               # Entry point
│   └── package.json
│
├── frontend/
│   ├── src/
│   │   ├── assets/             # Images, icons, backgrounds
│   │   ├── components/
│   │   │   ├── Navbar.jsx      # Navigation bar
│   │   │   ├── LeftSidebar.jsx # User list sidebar
│   │   │   ├── ChatBox.jsx     # Chat message container
│   │   │   ├── RightSidebar.jsx # User profile sidebar
│   │   │   ├── MessageInput.jsx # Message input field
│   │   │   └── UserProfile.jsx  # User profile display
│   │   ├── context/
│   │   │   ├── AppContext.jsx  # Global app state
│   │   │   └── ChatContext.jsx # Chat-specific state
│   │   ├── pages/
│   │   │   ├── Chat.jsx        # Main chat interface
│   │   │   ├── Login.jsx       # Login page
│   │   │   ├── ProfileUpdate.jsx # Profile update page
│   │   │   └── Signup.jsx      # Registration page
│   │   ├── lib/
│   │   │   └── socket.js       # Socket.io client setup
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   └── index.css
│   ├── .env
│   └── package.json
│
└── README.md
```

## 📖 Usage Guide

### Getting Started

#### 1. User Registration
1. Click on "Sign Up" from the login page
2. Enter your name, email, and password
3. Add a bio (optional)
4. Upload a profile picture (optional)
5. Click "Create Account"

#### 2. Profile Setup
1. After registration, you'll be redirected to profile update page
2. Add/update your profile picture via Cloudinary upload
3. Update your name and bio
4. Save changes

#### 3. Starting a Conversation
1. Browse the user list on the left sidebar
2. Search for users using the search bar
3. Click on a user to open chat
4. Start messaging instantly!

#### 4. Sending Messages
1. Type your message in the input field
2. Press Enter or click Send button
3. Upload images using the image icon
4. Messages are delivered instantly via Socket.io

#### 5. Managing Conversations
- **Online Status**: Green dot indicates user is online
- **Unseen Messages**: Red badge shows unread message count
- **Message Status**: Double check marks for seen messages
- **Scroll Behavior**: Auto-scrolls to latest messages
- **Image Preview**: Click on images to view full size

### Features in Action

#### Real-Time Updates
- Messages appear instantly without page refresh
- Online/offline status updates automatically
- Typing indicators show when someone is typing
- Unseen message count updates in real-time

#### Profile Management
- Update profile picture anytime
- Modify name and bio
- Changes reflect immediately across all conversations
- Logout to end session securely


## 🚀 Deployment

### Backend Deployment (Vercel)

1. **Prepare for Deployment**
```bash
# Ensure vercel.json is configured
{
  "version": 2,
  "builds": [
    {
      "src": "server.js",
      "use": "@vercel/node"
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "dest": "server.js"
    }
  ]
}
```

2. **Deploy to Vercel**
```bash
cd backend
vercel --prod
```

3. **Set Environment Variables**
- Add all .env variables in Vercel dashboard
- Update MONGODB_URI, JWT_SECRET, Cloudinary credentials

### Frontend Deployment (Vercel)

1. **Update Backend URL**
```env
VITE_BACKEND_URL=https://your-backend-url.vercel.app
```

2. **Build and Deploy**
```bash
cd frontend
npm run build
vercel --prod
```

3. **Configure Vercel**
- Set build command: `npm run build`
- Set output directory: `dist`
- Add environment variables



## 🔮 Future Enhancements

- [ ] **Group Chat**: Create and manage group conversations
- [ ] **Voice Messages**: Record and send voice notes
- [ ] **Video Calls**: Integrate WebRTC for video calling
- [ ] **Message Reactions**: React to messages with emojis
- [ ] **Message Search**: Search within conversations
- [ ] **File Sharing**: Support for document uploads
- [ ] **Push Notifications**: Browser/mobile push notifications
- [ ] **Message Encryption**: End-to-end encryption
- [ ] **Dark Mode**: User preference for dark theme
- [ ] **Message Deletion**: Delete messages for everyone
- [ ] **User Blocking**: Block/unblock users
- [ ] **Last Seen**: Show last seen timestamp
- [ ] **Multi-language Support**: Internationalization
- [ ] **Mobile App**: React Native mobile application
- [ ] **Desktop App**: Electron desktop application

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines
- Follow existing code style and conventions
- Write meaningful commit messages
- Update documentation for new features
- Test thoroughly before submitting PR
- Ensure all existing tests pass

## 🐛 Known Issues

- Socket.io reconnection may cause duplicate messages (working on fix)
- Large image uploads may timeout on slower connections (implementing compression)
- Mobile browser notification support limited (progressive enhancement in progress)

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

**Shreyansh Priyadarshi**
- GitHub: [@Shreyansh0843](https://github.com/Shreyansh0843)
- LinkedIn: [Shreyansh Priyadarshi](https://linkedin.com/in/shreyansh20)
- Email: shreyansh12361@gmail.com

## 🙏 Acknowledgments

- **Socket.io** for real-time communication framework
- **MongoDB Atlas** for cloud database hosting
- **Cloudinary** for image management and CDN
- **Vercel** for seamless deployment platform
- **Tailwind CSS** for utility-first CSS framework
- All open-source libraries used in this project

## 📞 Support

If you encounter any issues or have questions:
- Open an issue on GitHub
- Contact via email: shreyansh12361@gmail.com
- Connect on LinkedIn for professional queries

---

<div align="center">

### ⭐ Star this repository if you find it helpful!

**Built with ❤️ using MERN Stack & Socket.io**

[Report Bug](https://github.com/Shreyansh0843/echochat/issues) • [Request Feature](https://github.com/Shreyansh0843/echochat/issues)

</div>
