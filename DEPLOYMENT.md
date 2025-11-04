# Deployment Guide for Earthquake Monitor

## 🚀 Quick Start - Deploy to Render

### Step 1: Prepare Your Repository

If you haven't already initialized git:

```bash
git init
git add .
git commit -m "Initial commit - Earthquake Monitor ready for deployment"
```

### Step 2: Push to GitHub

1. Create a new repository on GitHub (https://github.com/new)
2. **Don't** initialize with README (your project already has one)
3. Copy the repository URL
4. Run these commands:

```bash
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git branch -M main
git push -u origin main
```

### Step 3: Deploy on Render

1. Go to **https://render.com** and sign up (free, no credit card needed)

2. Click **"New +"** in the top right → Select **"Web Service"**

3. Click **"Connect GitHub"** and authorize Render to access your repositories

4. Select your **earthquake-monitor** repository

5. Render will auto-detect the configuration from `render.yaml`:
   - **Name**: earthquake-monitor (or customize)
   - **Runtime**: Python 3
   - **Build Command**: `pip install -r requirements.txt`
   - **Start Command**: `python main.py`

6. Click **"Create Web Service"**

7. Wait 2-3 minutes for the build to complete

8. Your app will be live at: **`https://your-app-name.onrender.com`**

### Step 4: Test Your Deployment

Once deployed, visit your URL and check:
- ✅ Map loads correctly
- ✅ Status shows "Monitoring Active"
- ✅ Click "Check Now" to fetch earthquake data
- ✅ Browser console has no errors (F12 → Console tab)

## 📊 Monitoring Your Deployment

### Render Dashboard
- View logs: Click on your service → "Logs" tab
- See requests, errors, and app output
- Monitor uptime and performance

### Common Issues

**Problem**: App shows "Service Unavailable"
- **Solution**: Check logs for errors, ensure all dependencies are in requirements.txt

**Problem**: Map doesn't load
- **Solution**: Check browser console for errors, verify Leaflet CDN is accessible

**Problem**: No earthquake data appears
- **Solution**: Check logs to ensure USGS API is accessible, verify API endpoint works

## 🔄 Updating Your Deployment

To deploy changes:

```bash
git add .
git commit -m "Description of your changes"
git push origin main
```

Render will automatically detect the push and redeploy your app!

## 💰 Free Tier Limitations

Render's free tier includes:
- ✅ 750 hours per month (sufficient for one app)
- ✅ Automatic HTTPS
- ✅ Auto-deploy on git push
- ❌ App sleeps after 15 minutes of inactivity
- ❌ First request after sleep takes ~30 seconds

To keep app awake, you can:
- Use a service like UptimeRobot to ping your app every 10 minutes
- Upgrade to paid tier ($7/month) for always-on service

## 🌐 Custom Domain (Optional)

To use your own domain:
1. Go to your service settings on Render
2. Click "Custom Domain"
3. Add your domain
4. Update DNS records as instructed
5. Render provides free SSL certificates

## 🛠️ Environment Variables (If Needed)

If you want to add configuration:
1. Go to your service on Render
2. Click "Environment" tab
3. Add variables like:
   - `SF_LAT` - Override San Francisco latitude
   - `SF_LON` - Override San Francisco longitude
   - `RADIUS_KM` - Override monitoring radius

Then update your code to read from environment:
```python
SF_LAT = float(os.environ.get('SF_LAT', 37.7749))
SF_LON = float(os.environ.get('SF_LON', -122.4194))
RADIUS_KM = int(os.environ.get('RADIUS_KM', 200))
```

## ✅ You're Done!

Your earthquake monitor is now live and accessible to the world! 🌍

Share your URL with friends and colleagues to show off your real-time earthquake monitoring system.

