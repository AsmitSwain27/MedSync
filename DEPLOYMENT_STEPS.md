# MedSync Deployment Steps - Vercel + Render

## 🎯 Current Status
✅ Frontend built successfully
✅ Git repository ready
✅ Environment files configured

---

## Step 1: Deploy Backend to Render (Do This First!)

### 1.1 Push to GitHub (if not already done)
```bash
git push origin main
```

### 1.2 Create Render Account & Deploy
1. **Go to**: https://render.com
2. **Sign up** using your GitHub account
3. **Click**: "New +" button → "Web Service"
4. **Connect Repository**: 
   - Click "Connect account" if first time
   - Find and select your MedSync repository
5. **Configure Service**:
   ```
   Name: medsync-backend
   Region: Oregon (US West) or Singapore (closest to you)
   Branch: main
   Root Directory: backend
   Runtime: Node
   Build Command: npm install
   Start Command: npm start
   Instance Type: Free
   ```

### 1.3 Add Environment Variables
Click **"Advanced"** → **"Add Environment Variable"**, then add these one by one:

```env
NODE_ENV=production
PORT=5000
MONGODB_URI=mongodb+srv://abhijeetsoren222_db_user:hTxcNlZMkRJrt0eI@cluster0.mgq85ip.mongodb.net/medsync?retryWrites=true&w=majority&appName=Cluster0
JWT_SECRET=medsync_jwt_secret_key_2024_change_in_production_12345
JWT_EXPIRE=7d
JWT_REFRESH_SECRET=medsync_refresh_token_secret_key_2024_67890
JWT_REFRESH_EXPIRE=30d
CLIENT_URL=https://your-app-name.vercel.app
FRONTEND_URL=https://your-app-name.vercel.app
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX_REQUESTS=100
```

⚠️ **IMPORTANT**: 
- For `CLIENT_URL` and `FRONTEND_URL`, use placeholder for now
- We'll update this after deploying frontend to Vercel

### 1.4 Deploy
1. Click **"Create Web Service"**
2. Wait 2-3 minutes for deployment
3. **COPY YOUR BACKEND URL**: `https://medsync-backend-xxxx.onrender.com`
4. ✅ Test it: Open `https://medsync-backend-xxxx.onrender.com/api` in browser

---

## Step 2: Deploy Frontend to Vercel

### 2.1 Create Vercel Account
1. **Go to**: https://vercel.com
2. **Sign up** with GitHub
3. **Authorize** Vercel to access your repositories

### 2.2 Import Project
1. Click **"Add New..."** → **"Project"**
2. **Import** your GitHub repository
3. **Configure**:
   ```
   Framework Preset: Vite
   Root Directory: frontend
   Build Command: npm run build
   Output Directory: dist
   Install Command: npm install
   ```

### 2.3 Add Environment Variables
Before deploying, click **"Environment Variables"** and add:

```env
VITE_API_URL=https://medsync-backend-xxxx.onrender.com/api
VITE_GROQ_API_KEY=your_groq_api_key_here
```

⚠️ Replace `medsync-backend-xxxx.onrender.com` with YOUR actual Render URL!

### 2.4 Deploy
1. Click **"Deploy"**
2. Wait 2-3 minutes
3. **COPY YOUR FRONTEND URL**: `https://your-app-name.vercel.app`
4. Click on the URL to open your app!

---

## Step 3: Update CORS (Critical!)

Now that you have your Vercel URL, update backend:

1. **Go back to Render Dashboard**
2. **Click** on your backend service
3. **Go to**: "Environment" tab
4. **Update** these two variables:
   ```
   CLIENT_URL=https://your-app-name.vercel.app
   FRONTEND_URL=https://your-app-name.vercel.app
   ```
   (Use your actual Vercel URL - NO trailing slash!)
5. Click **"Save Changes"**
6. Service will **auto-redeploy** (wait ~1 minute)

---

## Step 4: Configure MongoDB Access

1. **Go to**: https://cloud.mongodb.com
2. **Login** to your MongoDB Atlas account
3. **Click** on your cluster → "Network Access"
4. **Add IP Address**: `0.0.0.0/0` (allows connections from anywhere)
5. **Confirm**: This allows Render to connect to your database

---

## Step 5: Test Your Deployed App! 🎉

### Test Checklist:
1. ✅ Open your Vercel URL
2. ✅ Homepage loads correctly
3. ✅ Logo appears (check navbar)
4. ✅ Click "Get Started" or "Login"
5. ✅ Register a new user
6. ✅ Login with your credentials
7. ✅ Go to "Find Doctors"
8. ✅ Test map (should show your location)
9. ✅ Search for doctors by radius
10. ✅ Test AI doctor recommendations
11. ✅ Book an appointment
12. ✅ Test AI prescription assistant (if logged in as doctor)

---

## Troubleshooting

### "Cannot connect to backend"
**Check**:
1. Backend URL is correct in Vercel environment variables
2. Backend is running on Render (check dashboard)
3. CORS is updated with exact Vercel URL

**Fix**: Redeploy frontend on Vercel after fixing environment variables

### "CORS Error"
**Fix**:
1. Go to Render → Environment
2. Make sure `CLIENT_URL` matches your Vercel URL EXACTLY
3. NO trailing slash: ✅ `https://app.vercel.app` ❌ `https://app.vercel.app/`

### "Map not showing"
**Check**: Browser console for errors
**Fix**: Leaflet CSS should be loaded (already configured)

### "AI features not working"
**Check**: 
1. Groq API key is in Vercel environment variables
2. Browser console for API errors

### "Render service is slow"
**Reason**: Free tier spins down after 15 minutes of inactivity
**Solution**: First request will wake it up (~30 seconds)

---

## Optional: Custom Domain

### Vercel:
1. Go to Project Settings → Domains
2. Add your domain
3. Update DNS records as instructed

### Render:
1. Go to Service Settings → Custom Domain
2. Add your domain
3. Update DNS CNAME record

---

## Cost Summary

- ✅ **Vercel**: FREE (unlimited deployments)
- ✅ **Render**: FREE (750 hours/month = 24/7 for one service)
- ✅ **MongoDB**: FREE (512MB storage)
- ✅ **Groq AI**: FREE tier available
- **Total**: $0/month 🎉

### When to Upgrade?

**Render Standard** ($7/month):
- No cold starts
- Always-on
- Better for production traffic

**Vercel Pro** ($20/month):
- Team features
- Better analytics
- Priority support

---

## Quick Commands Reference

### Redeploy Frontend (if you make changes):
```bash
git add .
git commit -m "Update frontend"
git push origin main
```
Then Vercel auto-deploys!

### Check Logs:
- **Render**: Dashboard → Logs tab
- **Vercel**: Dashboard → Deployments → View Function Logs

### Force Redeploy:
- **Render**: Click "Manual Deploy" → "Deploy latest commit"
- **Vercel**: Click "Redeploy" on latest deployment

---

## Your Deployment URLs

**Frontend (Vercel)**: `_________________` (fill this in)
**Backend (Render)**: `_________________` (fill this in)

---

## Next Steps After Deployment

1. ✅ Test all features thoroughly
2. ✅ Share your app with friends/testers
3. ⚠️ Monitor error logs for issues
4. 🔒 Consider moving Groq API to backend (security)
5. 📈 Set up analytics (Google Analytics)
6. 🎨 Customize branding/colors
7. 📧 Configure email notifications (optional)

---

**Need Help?** 
- Render Docs: https://render.com/docs
- Vercel Docs: https://vercel.com/docs
- MongoDB Docs: https://docs.mongodb.com

**Estimated Time**: 15-20 minutes total
**Difficulty**: Easy ⭐⭐☆☆☆

Good luck! 🚀
