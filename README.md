# Sales Analysis Dashboard

A modern, professional sales analysis dashboard with Firebase authentication and real-time data management powered by Firestore.

## 🎯 Features

- ✅ **Firebase Authentication** - Secure login and registration
- ✅ **Real-time Data** - Firestore integration for instant data sync
- ✅ **Dashboard Analytics** - KPI cards and charts
- ✅ **Sales Management** - Add, view, and delete sales records
- ✅ **Charts & Visualizations** - Revenue trends, top products, region analytics
- ✅ **Dark Mode** - Night-friendly interface
- ✅ **CSV Export** - Export sales data
- ✅ **Responsive Design** - Works on all devices
- ✅ **Modern UI** - Beautiful gradient-based design with smooth animations

## 🚀 Quick Start

### Prerequisites

- Modern web browser (Chrome, Firefox, Safari, Edge)
- Firebase account
- Text editor or IDE

### 1. Setup Firebase

1. Go to [Firebase Console](https://console.firebase.google.com)
2. Create a new project
3. Enable Authentication (Email/Password)
4. Create a Firestore database (Start in test mode for development)
5. Copy your Firebase config

### 2. Configure Firebase Credentials

The Firebase credentials are already configured in `frontend/js/auth.js`:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSyD9I6jWVvD-LuNIqMsmVTjlX8piXku-Q8s",
  authDomain: "sales-analysis-dashboard-6cd0c.firebaseapp.com",
  projectId: "sales-analysis-dashboard-6cd0c",
  storageBucket: "sales-analysis-dashboard-6cd0c.firebasestorage.app",
  messagingSenderId: "670846720070",
  appId: "1:670846720070:web:a58934bf83951f694d1247",
  measurementId: "G-E7CHZ3DD0S"
};
```

**To use your own Firebase project:**
1. Replace the `firebaseConfig` object in `frontend/js/auth.js` with your credentials
2. Update the Firebase rules in your console for Firestore

### 3. Firestore Security Rules

Add these rules to your Firestore for user-specific data protection:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Users collection
    match /users/{uid} {
      allow read, write: if request.auth.uid == uid;
      
      // Sales subcollection
      match /sales/{document=**} {
        allow read, write: if request.auth.uid == uid;
      }
    }
  }
}
```

### 4. Run the Application

#### Option 1: Direct Browser Access (Recommended for Development)
Simply open `frontend/index.html` in your web browser. No server required!

#### Option 2: Local Development Server
```bash
# Python
python -m http.server 8000

# Node.js
npx http-server

# Then visit: http://localhost:8000
```

### 5. First Login

1. Open the application
2. Click "Sign Up" to create a new account
3. Enter your email and password
4. Start adding sales data!

## 📱 Usage

### Adding a Sale
1. Click the "+ Add Sale" button
2. Fill in the required information:
   - Product Name
   - Category
   - Amount
   - Quantity
   - Region
   - Customer Name (optional)
3. Sale is automatically saved to Firestore

### Viewing Dashboard
- See real-time KPIs: Total Sales, Total Orders, Avg Order Value, Growth
- Charts show revenue trends, top products, region sales, and customer purchases

### Exporting Data
- Click "Export CSV" in the Reports section
- Your sales data will be downloaded as a CSV file

### Dark Mode
- Toggle dark mode using the button in the sidebar
- Setting is saved to local storage

## 📂 Project Structure

```
Sales Analysis Dashboard/
├── frontend/
│   ├── index.html           # Main authentication & dashboard page
│   ├── js/
│   │   ├── auth.js          # Firebase authentication logic
│   │   ├── login.js         # Login/signup form handlers
│   │   └── dashboard.js     # Dashboard & data management
│   └── css/
│       └── style.css        # Modern responsive styling
├── backend/                 # Optional: Backend API (not required for Firebase version)
├── README.md
└── CHANGELOG.md
```

## 🔐 Security

- ✅ Firebase Authentication handles password hashing and security
- ✅ Firestore Security Rules ensure users can only access their own data
- ✅ No sensitive data stored in browser local storage
- ✅ All data encrypted in transit (HTTPS)

## 🎨 Customization

### Change Colors
Edit the CSS variables in `frontend/css/style.css`:
```css
:root {
  --primary-color: #3b82f6;      /* Change primary color */
  --secondary-color: #10b981;    /* Change secondary color */
  --danger-color: #ef4444;       /* Change danger color */
}
```

### Modify Firestore Structure
Edit the data structure in `frontend/js/dashboard.js` in the `openAddSaleModal()` function.

## 🐛 Troubleshooting

### Authentication not working
- Check Firebase credentials in `frontend/js/auth.js`
- Enable Email/Password authentication in Firebase Console
- Check browser console for errors (F12)

### Data not saving
- Verify Firestore Security Rules are correctly set
- Check Firestore quota usage in Firebase Console
- Ensure user is authenticated

### Charts not displaying
- Check browser console for errors
- Verify Chart.js is loading from CDN
- Ensure sales data exists

## 📊 Tech Stack

- **Frontend**: HTML5, CSS3, Vanilla JavaScript
- **Authentication**: Firebase Authentication
- **Database**: Firebase Firestore
- **Charts**: Chart.js 3.9.1
- **Styling**: Modern CSS with CSS Variables
- **Fonts**: Inter (Google Fonts)

## 🚢 Production Deployment

### Deploy to Firebase Hosting
```bash
npm install -g firebase-tools
firebase login
firebase init hosting
firebase deploy
```

### Deploy to Vercel
```bash
npm install -g vercel
vercel
```

### Deploy to GitHub Pages
1. Push to GitHub
2. Enable GitHub Pages in repository settings
3. Select `main` branch as source

## 📝 License

This project is open source and available for personal and commercial use.

## 🤝 Contributing

Contributions are welcome! Feel free to submit issues and pull requests.

## 📞 Support

For issues and questions:
1. Check the troubleshooting section
2. Review Firebase Documentation
3. Check browser console for error messages

---

**Built with ❤️ for modern sales teams**

2. Login with:
   - Username: admin
   - Password: password

### Database

The application uses SQLite by default. To use MySQL:

1. Install MySQL and create a database named `sales_db`

2. Update `backend/config.py`:
   ```python
   SQLALCHEMY_DATABASE_URI = 'mysql://username:password@localhost/sales_db'
   ```

3. Install MySQL connector:
   ```
   pip install pymysql
   ```

## Project Structure

```
/
├── backend/
│   ├── app.py          # Flask application
│   ├── models.py       # Database models
│   ├── routes.py       # API routes
│   ├── config.py       # Configuration
│   └── requirements.txt
└── frontend/
    ├── index.html      # Login page
    ├── dashboard.html  # Main dashboard
    ├── css/
    │   └── style.css   # Styles
    └── js/
        ├── login.js    # Login functionality
        └── dashboard.js # Dashboard functionality
```

## API Endpoints

- `POST /api/login` - User login
- `POST /api/logout` - User logout
- `GET /api/sales` - Get all sales
- `POST /api/sales` - Add new sale
- `PUT /api/sales/<id>` - Update sale
- `DELETE /api/sales/<id>` - Delete sale
- `GET /api/dashboard-summary` - Get dashboard summary data

## Default User

- Username: admin
- Password: password

## Sample Data

The application includes sample sales data for demonstration purposes.