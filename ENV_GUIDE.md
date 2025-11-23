# Environment Variables Guide 🌍

## ✅ Your Setup is Correct!

### Backend (.env in `server/` folder)
```bash
# Django Settings
SECRET_KEY=your-secret-key
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1

# Cloudinary (for image uploads)
CLOUDINARY_CLOUD_NAME=dkkx6vrkk
CLOUDINARY_API_KEY=767546217217349
CLOUDINARY_API_SECRET=u9jCIe-4g0tWa_hQBKcrWNpdrGE

# CORS (frontend URLs that can access the API)
CORS_ALLOWED_ORIGINS=http://localhost:3000,http://localhost:5173
```

### Frontend (.env.local in `client/` folder)
```bash
# Backend API URL (must start with NEXT_PUBLIC_ to be accessible in browser)
NEXT_PUBLIC_API_URL=http://127.0.0.1:8000/api
```

---

## 📖 How Environment Variables Work

### Backend (Django)
1. **File**: `server/.env`
2. **Library**: `django-environ`
3. **Usage in code**:
   ```python
   # In settings.py
   from pathlib import Path
   import os
   import environ
   
   BASE_DIR = Path(__file__).resolve().parent.parent
   
   # Initialize environ
   env = environ.Env(
       DEBUG=(bool, True),
       ALLOWED_HOSTS=(list, []),
   )
   
   # Read .env file
   env_file = os.path.join(BASE_DIR, '.env')
   if os.path.exists(env_file):
       environ.Env.read_env(env_file)
   
   # Use variables
   DEBUG = env.bool('DEBUG', default=True)
   ALLOWED_HOSTS = env.list('ALLOWED_HOSTS', default=['localhost'])
   SECRET_KEY = env('SECRET_KEY')
   ```

4. **Important Methods**:
   - `env('VAR_NAME')` - Get string value
   - `env.bool('VAR_NAME')` - Get boolean (True/False)
   - `env.list('VAR_NAME')` - Get comma-separated list
   - `env.int('VAR_NAME')` - Get integer
   - All accept `default=` parameter

### Frontend (Next.js)
1. **File**: `client/.env.local` (or `.env`)
2. **Built-in**: Next.js automatically loads env files
3. **Important Rules**:
   - Variables starting with `NEXT_PUBLIC_` are accessible in browser code
   - Other variables are only available server-side
   
4. **Usage in code**:
   ```typescript
   // In any file
   const API_URL = process.env.NEXT_PUBLIC_API_URL || 'http://localhost:8000/api';
   ```

---

## 🔍 Troubleshooting

### Backend Not Reading .env File?
1. **Check file location**: Must be in `server/` folder (same level as `manage.py`)
2. **Check file name**: Must be exactly `.env` (no extra extensions)
3. **Restart server**: Changes require server restart
4. **Check syntax**: No spaces around `=`, use commas for lists

### Frontend Not Reading .env.local File?
1. **Check file location**: Must be in `client/` folder (same level as `package.json`)
2. **Check variable prefix**: Must start with `NEXT_PUBLIC_`
3. **Restart dev server**: Run `npm run dev` again
4. **Check Next.js version**: Older versions might need different setup

### Common Issues

**Issue**: `ModuleNotFoundError: No module named 'environ'`
**Solution**: 
```bash
cd server
.\venv\Scripts\Activate.ps1
pip install django-environ
```

**Issue**: CORS errors in browser console
**Solution**: 
1. Check `CORS_ALLOWED_ORIGINS` includes your frontend URL
2. Restart Django server
3. Check browser is accessing from listed URL (not a different port)

**Issue**: Frontend can't connect to backend
**Solution**:
1. Check `NEXT_PUBLIC_API_URL` matches Django server address
2. Ensure Django server is running (`python manage.py runserver`)
3. Check CORS settings allow the frontend origin

---

## 📝 Best Practices

### Development
- Use `.env` for backend local development
- Use `.env.local` for frontend local development
- Never commit these files to git (already in `.gitignore`)

### Production
- Set environment variables through hosting platform (Vercel, Heroku, etc.)
- Use strong `SECRET_KEY` for Django
- Set `DEBUG=False` in production
- Use environment-specific URLs

### Security
- ✅ Keep `.env` files in `.gitignore`
- ✅ Use different credentials for development/production
- ✅ Don't hardcode secrets in code
- ✅ Share credentials securely (not via email/Slack)

---

## 🚀 Quick Reference

### Start Development Servers

**Backend**:
```powershell
cd server
.\venv\Scripts\Activate.ps1
python manage.py runserver
# Server runs at http://127.0.0.1:8000
```

**Frontend**:
```powershell
cd client
npm run dev
# Server runs at http://localhost:3000
```

### Verify Environment Loading

**Backend**:
```powershell
cd server
.\venv\Scripts\Activate.ps1
python manage.py shell
```
```python
from django.conf import settings
print(f"DEBUG: {settings.DEBUG}")
print(f"ALLOWED_HOSTS: {settings.ALLOWED_HOSTS}")
print(f"CLOUDINARY: {settings.CLOUDINARY_STORAGE}")
```

**Frontend** (check browser console):
```javascript
console.log('API URL:', process.env.NEXT_PUBLIC_API_URL);
```

---

## 📌 Current Configuration Summary

✅ **Backend** (`server/.env`):
- Django environment properly configured
- Cloudinary credentials loaded
- CORS allowing localhost:3000 and localhost:5173

✅ **Frontend** (`client/.env.local`):
- API URL pointing to http://127.0.0.1:8000/api
- Properly prefixed with NEXT_PUBLIC_

✅ **Code** (`server/project/settings.py`):
- Using `django-environ` correctly
- Proper type casting (`.bool()`, `.list()`)
- Fallback defaults provided

✅ **Code** (`client/lib/api.ts`):
- Reading NEXT_PUBLIC_API_URL correctly
- Has fallback to localhost

**Everything is configured correctly! 🎉**
