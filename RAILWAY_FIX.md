# 🚀 Railway Deployment Fix

## ❌ Current Errors Fixed:
1. `DisallowedHost at /` - Invalid HTTP_HOST header
2. `Forbidden (403)` - CSRF verification failed

## ✅ Quick Fix for Railway:

### **Option 1: Set Environment Variables in Railway Dashboard** (Recommended)

1. Go to your Railway project dashboard
2. Click on your service
3. Go to **Variables** tab
4. Add these environment variables:

```bash
DEBUG=False
SECRET_KEY=django-insecure-#p=3h@bj%&4cd(^y8gh655ey8q_q^&tl+l_=pt70wjljc3sw8_
GOOGLE_GENERATIVE_AI_API_KEY=AIzaSyDsafmVLoPv1MU9LyThO1vomC6beik9gh0
ALLOWED_HOSTS=web-production-6a99d.up.railway.app,*.railway.app
```

### **Option 2: Update settings.py for Railway** ✅ **APPLIED**

Added Railway-specific settings to handle HTTPS and CSRF:

```python
# Railway specific settings
if 'RAILWAY_ENVIRONMENT' in os.environ:
    ALLOWED_HOSTS = ['*']  # Allow all hosts on Railway
    DEBUG = False
    # CSRF settings for Railway
    CSRF_TRUSTED_ORIGINS = ['https://*.railway.app', 'https://web-production-6a99d.up.railway.app']
    SECURE_PROXY_SSL_HEADER = ('HTTP_X_FORWARDED_PROTO', 'https')
    SECURE_SSL_REDIRECT = False  # Railway handles SSL
```

## 🔄 After Making Changes:

1. **Redeploy**: Railway will automatically redeploy when you push changes
2. **Check Variables**: Make sure environment variables are set in Railway dashboard
3. **Test**: Visit your Railway URL again

## 🎯 Your Railway URL:
`https://web-production-6a99d.up.railway.app/`

The app should work after setting the environment variables correctly in Railway!
