# Flash SEO Website - Deployment Guide

## 📁 Your Files

This package contains your complete website ready for GitHub Pages deployment:

- **index.html** - Your homepage (marketing website home)
- **feature-showcase-page-1.html** - Feature showcase page 1
- **feature-showcase-page-2.html** - Feature showcase page 2
- **flash-seo-testimonials---light.html** - Testimonials (light theme)
- **flash-seo-testimonials---dark.html** - Testimonials (dark theme)
- **flash-seo-vs-competitors---light.html** - Competitors comparison (light)
- **flash-seo-vs-competitors---dark-1.html** - Competitors comparison (dark v1)
- **flash-seo-vs-competitors---dark-2.html** - Competitors comparison (dark v2)

## 🚀 Step 1: Deploy to GitHub Pages

### Upload to GitHub:

1. Go to https://github.com and sign in
2. Click **+** (top right) → **New repository**
3. Name it: `flash-seo-website` (or your preferred name)
4. Choose **Public**
5. Check **Add a README file**
6. Click **Create repository**

### Add Your Files:

1. In your new repository, click **Add file** → **Upload files**
2. Drag ALL files from this folder (including index.html)
3. Click **Commit changes**

### Enable GitHub Pages:

1. Go to **Settings** (in your repository)
2. Click **Pages** (left sidebar)
3. Under **Source**, select **Deploy from a branch**
4. Choose **main** branch and **/ (root)**
5. Click **Save**
6. Wait 1-2 minutes, then visit: `https://YOUR-USERNAME.github.io/flash-seo-website/`

## 🗄️ Step 2: Set Up Supabase Backend

### Create Supabase Project:

1. Go to https://supabase.com and sign up/sign in
2. Click **New project**
3. Fill in:
   - **Project name**: flash-seo-backend
   - **Database Password**: (create a strong password and SAVE IT!)
   - **Region**: Choose closest to your users
4. Click **Create new project**
5. Wait ~2 minutes for setup

### Get Your Credentials:

1. In Supabase, go to **Settings** → **API**
2. Copy these two values:
   - **Project URL** (looks like: `https://xxxxx.supabase.co`)
   - **anon public** key (long string)

### Update Your Website:

1. Open `index.html` in a text editor
2. Find these lines near the bottom:
   ```javascript
   const SUPABASE_URL = 'YOUR-SUPABASE-PROJECT-URL'
   const SUPABASE_ANON_KEY = 'YOUR-SUPABASE-ANON-KEY'
   ```
3. Replace with your actual values:
   ```javascript
   const SUPABASE_URL = 'https://xxxxx.supabase.co'
   const SUPABASE_ANON_KEY = 'eyJhbGc...(your key here)'
   ```
4. Save the file
5. Re-upload to GitHub (replace the old index.html)

## 📊 Step 3: Create Database Tables

### Example: Contact Form Table

1. In Supabase, go to **Table Editor**
2. Click **Create a new table**
3. Name it: `contacts`
4. Add columns:
   - `id` (int8, primary key) - auto-generated
   - `created_at` (timestamptz) - auto-generated
   - `name` (text)
   - `email` (text)
   - `message` (text)
5. Click **Save**

### Example: Newsletter Subscribers Table

1. Click **Create a new table**
2. Name it: `subscribers`
3. Add columns:
   - `id` (int8, primary key)
   - `created_at` (timestamptz)
   - `email` (text)
4. Click **Save**

## 🔒 Step 4: Set Up Security (Row Level Security)

For each table:

1. Click on the table name
2. Click **RLS** tab
3. Click **Enable RLS**
4. Add policies:

**For public read access:**
- Click **New Policy** → **Select a template**
- Choose **Enable read access for all users**
- Click **Review** → **Save**

**For public insert (e.g., contact form):**
- Click **New Policy** → **Custom**
- Name: "Allow public insert"
- Policy command: INSERT
- Target roles: public
- Using expression: `true`
- Click **Save**

## 💡 Using Supabase in Your Website

### Example: Save Contact Form

```javascript
async function saveContact(name, email, message) {
  const { data, error } = await supabase
    .from('contacts')
    .insert([
      { name: name, email: email, message: message }
    ])
  
  if (error) {
    console.error('Error:', error)
    alert('Failed to send message')
  } else {
    alert('Message sent successfully!')
  }
}
```

### Example: Add Newsletter Subscriber

```javascript
async function subscribeNewsletter(email) {
  const { data, error } = await supabase
    .from('subscribers')
    .insert([{ email: email }])
  
  if (error) {
    console.error('Error:', error)
    alert('Subscription failed')
  } else {
    alert('Subscribed successfully!')
  }
}
```

## 🎨 Customization Tips

- All pages use **Tailwind CSS** - they're already styled!
- Colors are defined in the `<script id="tailwind-config">` section
- Primary blue: `#2563eb`
- Accent yellow: `#facc15`

## 📱 Your Website Will Be Live At:

```
https://YOUR-GITHUB-USERNAME.github.io/REPOSITORY-NAME/
```

Example: `https://johnsmith.github.io/flash-seo-website/`

## 🆘 Need Help?

- **GitHub Pages not working?** Make sure repository is Public and index.html is in the root
- **Supabase not connecting?** Check browser console (F12) for errors
- **Want custom domain?** Go to GitHub repo → Settings → Pages → Custom domain

## ✅ Checklist

- [ ] Files uploaded to GitHub
- [ ] GitHub Pages enabled
- [ ] Supabase project created
- [ ] Supabase credentials added to index.html
- [ ] Database tables created
- [ ] RLS policies configured
- [ ] Website is live!

---

**Your website is ready to go! 🚀**
