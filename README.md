XRP Mining App - Backend
A robust Node.js, Express.js, and MongoDB backend for the XRP Mining App that manages authentication, mining records, wallet balance, rewards, reports, and withdrawal requests through secure REST APIs.

Table of Contents
Features
Tech Stack
Prerequisites
Installation
Environment Variables
Running the Application
API Endpoints
Project Structure
Database Schema
Error Handling
Security Features
Contributing
License
Features
User Authentication: Secure user registration and login with JWT token-based authentication
Mining Records Management: Track and manage mining activities and historical records
Wallet Management: Monitor user wallet balances and XRP holdings
Rewards System: Automatic reward calculation and distribution for miners
Reports Generation: Generate detailed mining reports and performance analytics
Withdrawal Requests: Handle user withdrawal requests with validation and processing
Secure REST APIs: All endpoints protected with JWT authentication
Error Handling: Comprehensive error handling and validation
Database Persistence: MongoDB integration for reliable data storage
Tech Stack
Runtime: Node.js
Framework: Express.js
Database: MongoDB
Authentication: JWT (JSON Web Tokens)
Language: JavaScript (100%)
Prerequisites
Node.js (v14.0.0 or higher)
npm or yarn package manager
MongoDB (v4.0 or higher)
Git
Installation
Clone the repository

git clone https://github.com/Swapnil454/XRP_Mining_APP_BE.git
cd XRP_Mining_APP_BE
Install dependencies

npm install
Set up environment variables (see Environment Variables section)

Environment Variables
Create a .env file in the root directory with the following variables:

# Server Configuration
PORT=5000
NODE_ENV=development

# Database Configuration
MONGODB_URI=mongodb://localhost:27017/xrp_mining_app
MONGODB_USER=your_db_user
MONGODB_PASSWORD=your_db_password

# JWT Configuration
JWT_SECRET=your_jwt_secret_key
JWT_EXPIRE=7d

# Email Configuration (if applicable)
SMTP_HOST=your_smtp_host
SMTP_PORT=587
SMTP_USER=your_email
SMTP_PASSWORD=your_email_password

# XRP Network Configuration
XRP_NETWORK=testnet
XRP_SEED=your_xrp_seed
Important: Never commit the .env file to version control. Add it to .gitignore.

Running the Application
Development Mode
npm run dev
This starts the server with nodemon for automatic restarts on file changes.

Production Mode
npm start
API Endpoints
Authentication
POST /api/auth/register - Register a new user
POST /api/auth/login - Login user and get JWT token
POST /api/auth/logout - Logout user
POST /api/auth/refresh-token - Refresh JWT token
GET /api/auth/me - Get current user profile
Mining Records
GET /api/mining - Get all mining records for the user
POST /api/mining/start - Start a new mining session
POST /api/mining/stop - Stop the current mining session
GET /api/mining/:id - Get specific mining record details
Wallet & Balance
GET /api/wallet - Get wallet information and balance
GET /api/wallet/balance - Get current wallet balance
POST /api/wallet/deposit - Deposit funds to wallet
Rewards
GET /api/rewards - Get rewards summary
GET /api/rewards/history - Get rewards history
POST /api/rewards/claim - Claim available rewards
Reports
GET /api/reports - Get mining reports
GET /api/reports/daily - Get daily report
GET /api/reports/monthly - Get monthly report
GET /api/reports/export - Export report as PDF/CSV
Withdrawal
POST /api/withdrawals - Request a withdrawal
GET /api/withdrawals - Get withdrawal requests
GET /api/withdrawals/:id - Get withdrawal status
PUT /api/withdrawals/:id/cancel - Cancel a withdrawal request
Project Structure
XRP_Mining_APP_BE/
├── src/
│   ├── models/              # Database models
│   │   ├── User.js
│   │   ├── MiningRecord.js
│   │   ├── Wallet.js
│   │   ├── Reward.js
│   │   ├── Report.js
│   │   └── Withdrawal.js
│   ├── routes/              # API routes
│   │   ├── auth.js
│   │   ├── mining.js
│   │   ├── wallet.js
│   │   ├── rewards.js
│   │   ├── reports.js
│   │   └── withdrawals.js
│   ├── controllers/         # Route handlers
│   │   ├── authController.js
│   │   ├── miningController.js
│   │   ├── walletController.js
│   │   ├── rewardsController.js
│   │   ├── reportsController.js
│   │   └── withdrawalController.js
│   ├── middleware/          # Custom middleware
│   │   ├── auth.js
│   │   └── errorHandler.js
│   ├── utils/               # Utility functions
│   │   ├── validators.js
│   │   ├── helpers.js
│   │   └── constants.js
│   ├── config/              # Configuration files
│   │   ├── database.js
│   │   └── jwt.js
│   └── index.js             # Main application entry point
├── .env                     # Environment variables (not in repo)
├── .env.example             # Example environment variables
├── .gitignore              # Git ignore file
├── package.json            # Dependencies and scripts
├── package-lock.json       # Locked dependency versions
└── README.md               # This file
Database Schema
User Schema
{
  _id: ObjectId,
  username: String,
  email: String,
  password: String (hashed),
  walletAddress: String,
  createdAt: Date,
  updatedAt: Date
}
Mining Record Schema
{
  _id: ObjectId,
  userId: ObjectId,
  startTime: Date,
  endTime: Date,
  hashRate: Number,
  difficulty: Number,
  blocksFound: Number,
  earnings: Number,
  status: String,
  createdAt: Date
}
Wallet Schema
{
  _id: ObjectId,
  userId: ObjectId,
  balance: Number,
  totalDeposited: Number,
  totalWithdrawn: Number,
  currency: String,
  lastUpdated: Date
}
Reward Schema
{
  _id: ObjectId,
  userId: ObjectId,
  amount: Number,
  rewardType: String,
  claimed: Boolean,
  claimedAt: Date,
  createdAt: Date
}
Withdrawal Schema
{
  _id: ObjectId,
  userId: ObjectId,
  amount: Number,
  walletAddress: String,
  status: String,
  transactionHash: String,
  requestedAt: Date,
  processedAt: Date
}
Error Handling
The API implements comprehensive error handling:

400 Bad Request: Invalid input or malformed request
401 Unauthorized: Missing or invalid authentication token
403 Forbidden: Insufficient permissions
404 Not Found: Resource not found
500 Internal Server Error: Server-side error
All errors return a JSON response with the following structure:

{
  "success": false,
  "error": "Error message",
  "statusCode": 400
}
Security Features
JWT Authentication: Secure token-based authentication for all protected endpoints
Password Hashing: Bcrypt for secure password storage
Input Validation: Comprehensive input validation and sanitization
CORS Protection: Cross-Origin Resource Sharing configuration
Rate Limiting: API rate limiting to prevent abuse
Environment Variables: Sensitive data stored in environment variables
HTTPS: Recommended for production deployments
SQL/NoSQL Injection Prevention: Parameterized queries and input validation
Contributing
Contributions are welcome! Please follow these steps:

Fork the repository
Create a feature branch (git checkout -b feature/AmazingFeature)
Commit your changes (git commit -m 'Add some AmazingFeature')
Push to the branch (git push origin feature/AmazingFeature)
Open a Pull Request
License
This project is licensed under the MIT License - see the LICENSE file for details.

Need Help?

Check the Issues page
Create a new issue for bugs or feature requests
Contact the maintainers for support
Happy Mining! 🚀
