# MedSync - Easy Deployment Without Docker

## 🚀 Recommended: Vercel (Frontend) + Render (Backend)

This is the **easiest and fastest** way to deploy MedSync with **free tiers** available!

---

## Part 1: Deploy Backend to Render (5 minutes)

### Step 1: Create Render Account
1. Go to https://render.com
2. Sign up with GitHub (recommended)

### Step 2: Create Web Service
1. Click **"New +"** → **"Web Service"**
2. Connect your GitHub repository (or use manual deploy)
3. Configure:
   - **Name**: `medsync-backend`
   - **Region**: Choose closest to you
   - **Branch**: `main` (or your default branch)
   - **Root Directory**: `backend`
   - **Runtime**: `Node`
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
   - **Instance Type**: `Free`

### Step 3: Add Environment Variables
Click **"Advanced"** → **"Add Environment Variable"** and add:

```
NODE_ENV=production
PORT=5000
MONGODB_URI=mongodb+srv://abhijeetsoren222_db_user:hTxcNlZMkRJrt0eI@cluster0.mgq85ip.mongodb.net/medsync?retryWrites=true&w=majority&appName=Cluster0
JWT_SECRET=medsync_jwt_secret_key_2024_change_in_production_12345
JWT_EXPIRE=7d
CLIENT_URL=https://your-frontend-url.vercel.app
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX_REQUESTS=100
```

⚠️ **Note**: You'll update `CLIENT_URL` after deploying frontend

### Step 4: Deploy
1. Click **"Create Web Service"**
2. Wait for deployment (2-3 minutes)
3. Copy your backend URL: `https://medsync-backend-xxxx.onrender.com`

---

## Part 2: Deploy Frontend to Vercel (3 minutes)

### Option A: Using Vercel Dashboard (Easiest)

1. **Go to https://vercel.com**
2. **Sign up** with GitHub
3. **Import Project**:
   - Click "Add New" → "Project"
   - Import your GitHub repository
   - Select the repository
4. **Configure**:
   - **Framework Preset**: Vite
   - **Root Directory**: `frontend`
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
5. **Environment Variables**:
   Click "Environment Variables" and add:
   ```
   VITE_API_URL=https://medsync-backend-xxxx.onrender.com/api
   VITE_GROQ_API_KEY=your_groq_api_key_here
   ```
   (Replace with your actual Render backend URL)
6. **Deploy**: Click "Deploy"
7. **Copy your URL**: `https://your-app.vercel.app`

### Option B: Using Vercel CLI (Alternative)

1. **Install Vercel CLI**:
   ```bash
   npm install -g vercel
   ```

2. **Login**:
   ```bash
   vercel login
   ```

3. **Deploy**:
   ```bash
   cd frontend
   vercel
   ```
   Follow the prompts:
   - Link to existing project? `No`
   - Project name: `medsync`
   - Directory: `./`
   - Override settings? `Yes`
     - Build command: `npm run build`
     - Output directory: `dist`
     - Development command: `npm run dev`

4. **Add Environment Variables** (in Vercel Dashboard):
   - Go to your project settings
   - Add `VITE_API_URL` and `VITE_GROQ_API_KEY`

5. **Deploy to Production**:
   ```bash
   vercel --prod
   ```

---

## Part 3: Update CORS Settings

### Update Backend Environment on Render
1. Go to Render Dashboard → Your backend service
2. Go to **Environment** tab
3. Update `CLIENT_URL` to your Vercel URL:
   ```
   CLIENT_URL=https://your-app.vercel.app
   ```
4. Click **"Save Changes"**
5. Service will auto-redeploy

---

## Alternative Option: Netlify (Frontend) + Railway (Backend)

### Deploy Backend to Railway

1. **Go to https://railway.app**
2. **Sign up** with GitHub
3. **New Project** → **Deploy from GitHub repo**
4. **Select** your repository
5. **Add variables**:
   - Click "Variables" tab
   - Add same environment variables as above
6. **Generate Domain**:
   - Click "Settings" → "Generate Domain"
   - Copy: `https://medsync-backend-production.up.railway.app`

### Deploy Frontend to Netlify

1. **Go to https://netlify.com**
2. **Sign up** with GitHub
3. **Add new site** → **Import from Git**
4. **Configure**:
   - **Base directory**: `frontend`
   - **Build command**: `npm run build`
   - **Publish directory**: `frontend/dist`
5. **Environment variables**:
   - Go to Site settings → Environment variables
   - Add `VITE_API_URL` with Railway URL
6. **Deploy**

---

## Quick Deploy Script (Vercel)

Save this as `deploy-vercel.bat` in your project root:

```batch
@echo off
echo ========================================
echo   MedSync - Vercel Deployment
echo ========================================
echo.

echo [1/3] Building frontend...
cd frontend
call npm install
call npm run build

echo.
echo [2/3] Deploying to Vercel...
call vercel --prod

echo.
echo [3/3] Deployment complete!
echo.
echo IMPORTANT: Update backend CORS with your Vercel URL
echo.
pause
```

Run: `deploy-vercel.bat`

---

## Free Tier Limits

### Vercel Free Tier
- ✅ Unlimited deployments
- ✅ 100GB bandwidth/month
- ✅ Automatic HTTPS
- ✅ Instant rollbacks
- ✅ Custom domains

### Render Free Tier
- ✅ 750 hours/month (enough for one service)
- ⚠️ Spins down after 15 min inactivity
- ⚠️ Cold start ~30 seconds
- ✅ Automatic HTTPS
- ✅ Custom domains

### Railway Free Trial
- 💰 $5 free credit
- Pay-as-you-go after credit

---

## Post-Deployment Checklist

- [ ] Backend deployed and accessible
- [ ] Frontend deployed and accessible
- [ ] Environment variables configured
- [ ] CORS updated with frontend URL
- [ ] Test user registration
- [ ] Test user login
- [ ] Test doctor search
- [ ] Test AI features
- [ ] Verify map works
- [ ] Check all API endpoints

---

## Troubleshooting

### "CORS Error"
**Fix**: Update `CLIENT_URL` in backend environment variables with exact Vercel URL (no trailing slash)

### "API Not Found"
**Fix**: Verify `VITE_API_URL` in frontend includes `/api` at the end

### "Render Service Slow"
**Reason**: Free tier spins down after inactivity
**Solution**: Upgrade to paid tier ($7/month) or use Railway

### "Build Failed on Vercel"
**Fix**: 
1. Check build logs
2. Ensure all dependencies are in `package.json`
3. Run `npm run build` locally to test

### "Environment Variables Not Working"
**Fix**:
- Vercel: Redeploy after adding variables
- Render: Service auto-redeploys when you save variables

---

## Upgrade to Paid Plans (Optional)

### When to Upgrade?

**Render Standard ($7/month)**:
- No cold starts
- Always-on service
- Better performance

**Vercel Pro ($20/month)**:
- Team collaboration
- Better analytics
- Priority support

---

## MongoDB Atlas Reminder

Your MongoDB is already configured in the backend `.env`:
```
mongodb+srv://abhijeetsoren222_db_user:hTxcNlZMkRJrt0eI@cluster0.mgq85ip.mongodb.net/medsync
```

Make sure to:
1. Go to MongoDB Atlas → Network Access
2. Add IP: `0.0.0.0/0` (allow from anywhere)
3. This allows Render/Railway to connect

---

## Next Steps

1. ✅ Choose deployment platform (Vercel + Render recommended)
2. ✅ Deploy backend first
3. ✅ Deploy frontend with backend URL
4. ✅ Update CORS settings
5. ✅ Test all features
6. 🎉 Share your live app!

**Total Time**: ~10-15 minutes
**Cost**: FREE (with free tier limitations)
