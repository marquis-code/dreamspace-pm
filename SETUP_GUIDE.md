# 🚀 DreamSpace PM - Complete Setup Guide

## 📋 Prerequisites

- **Python 3.8+** installed
- **Node.js 18+** and npm installed
- **Git** (optional, for version control)

---

## 🔧 Backend Setup (Django)

### 1. Navigate to server directory
```powershell
cd server
```

### 2. Create virtual environment
```powershell
python -m venv venv
```

### 3. Activate virtual environment
```powershell
.\venv\Scripts\Activate.ps1
```

### 4. Install dependencies
```powershell
pip install -r requirements.txt
```

### 5. Install django-environ (if not in requirements.txt)
```powershell
pip install django-environ
```

### 6. Configure environment variables
The `.env` file is already set up with:
- Django secret key
- Cloudinary credentials (for image uploads)
- CORS settings

**Note**: The Cloudinary credentials are already configured. If you need to use your own:
1. Sign up at https://cloudinary.com
2. Update the credentials in `.env`

### 7. Run migrations
```powershell
python manage.py migrate
```

### 8. Create superuser (optional - for admin access)
```powershell
python manage.py createsuperuser
```

### 9. Load seed data (Nigerian market data)
```powershell
python manage.py seed_data
```

### 10. Start the backend server
```powershell
python manage.py runserver
```

Backend will run on: **http://127.0.0.1:8000**
- API: http://127.0.0.1:8000/api
- Admin: http://127.0.0.1:8000/admin

---

## 🎨 Frontend Setup (Next.js)

### 1. Navigate to client directory (new terminal)
```powershell
cd client
```

### 2. Install dependencies
```powershell
npm install
```

### 3. Configure environment variables
The `.env.local` file is already set up with:
```
NEXT_PUBLIC_API_URL=http://127.0.0.1:8000/api
```

### 4. Start the development server
```powershell
npm run dev
```

Frontend will run on: **http://localhost:3000**

---

## 🔐 Login Credentials (from seed data)

### Designers:
- **Email**: adaeze.okonkwo@example.com | **Password**: password123
- **Email**: chidi.nnamdi@example.com | **Password**: password123
- **Email**: amina.yusuf@example.com | **Password**: password123

### Artisans (All Verified):
- **Email**: oluwaseun.adeyemi@example.com | **Password**: password123
- **Email**: fatima.bello@example.com | **Password**: password123
- **Email**: emeka.okoro@example.com | **Password**: password123
- **Email**: blessing.nwosu@example.com | **Password**: password123
- **Email**: yusuf.ibrahim@example.com | **Password**: password123
- **Email**: chisom.okafor@example.com | **Password**: password123

### Clients:
- **Email**: ngozi.eze@example.com | **Password**: password123
- **Email**: tunde.adebayo@example.com | **Password**: password123

---

## 🐛 Troubleshooting

### Backend Issues

#### "No module named django"
```powershell
# Make sure virtual environment is activated
.\venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

#### "ModuleNotFoundError: No module named 'environ'"
```powershell
pip install django-environ
```

#### Port 8000 already in use
```powershell
# Kill the process using port 8000
netstat -ano | findstr :8000
taskkill /PID <PID> /F

# Or run on a different port
python manage.py runserver 8001
```

#### Database issues
```powershell
# Reset database (WARNING: This deletes all data)
Remove-Item db.sqlite3
python manage.py migrate
python manage.py seed_data
```

### Frontend Issues

#### "Module not found" errors
```powershell
# Delete node_modules and reinstall
Remove-Item -Recurse -Force node_modules
Remove-Item package-lock.json
npm install
```

#### Port 3000 already in use
```powershell
# Next.js will automatically suggest port 3001
# Or set a custom port:
# In package.json, change: "dev": "next dev -p 3001"
```

#### API connection errors
1. Check that backend is running on http://127.0.0.1:8000
2. Verify `.env.local` has: `NEXT_PUBLIC_API_URL=http://127.0.0.1:8000/api`
3. Check browser console for CORS errors

#### "Logout on refresh" issue
This was fixed by improving token refresh logic. If it still occurs:
1. Clear browser localStorage: `localStorage.clear()`
2. Log in again

---

## 🎯 Quick Start (Automated)

### Backend Quick Start
```powershell
cd server
.\venv\Scripts\Activate.ps1
python manage.py runserver
```

### Frontend Quick Start
```powershell
cd client
npm run dev
```

---

## 📊 Features

✅ **Dark Theme** - Modern black/zinc color scheme
✅ **Email Authentication** - No username required
✅ **Nigerian Market Data** - Locations, Naira pricing, local context
✅ **Project Management** - Create and manage interior design projects
✅ **Task Tracking** - Kanban board (To Do, In Progress, Done)
✅ **Moodboards** - Visual inspiration boards with drag-and-drop
✅ **Artisan Marketplace** - Find verified Nigerian artisans
✅ **Reviews & Ratings** - Rate artisans and view portfolios
✅ **JWT Authentication** - Secure token-based auth with refresh

---

## 🔄 Resetting Database

If you need to start fresh:

```powershell
cd server
.\venv\Scripts\Activate.ps1
Remove-Item db.sqlite3
python manage.py migrate
python manage.py seed_data
```

---

## 📝 Notes

- **Backend runs on port 8000** - Django REST API
- **Frontend runs on port 3000** - Next.js application
- **Database**: SQLite (file-based, no server needed)
- **Image Storage**: Cloudinary (already configured)
- **Seed Data**: Comprehensive Nigerian market data included

---

## 🆘 Need Help?

1. Check this guide first
2. Review error messages in terminal
3. Check browser console (F12) for frontend errors
4. Ensure both servers are running
5. Verify environment variables are set correctly

---

## 📦 What's Included

### Backend (Django)
- User authentication (email-based)
- Projects, Tasks, Moodboards APIs
- Artisan marketplace with portfolios
- Reviews and ratings system
- Nigerian-specific seed data

### Frontend (Next.js)
- Dark theme UI
- Dashboard with all features
- Responsive design
- Form validation
- Image uploads
- Drag-and-drop moodboards

---

**Happy Building! 🎨✨**
