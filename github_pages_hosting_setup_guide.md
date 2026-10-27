# Comprehensive Guide: Hosting ViaVika on GitHub Pages

This guide provides step-by-step instructions for publishing **ViaVika** (or any static web application) for free using **GitHub Pages**, configuring a custom domain, and managing updates.

---

## 🛠️ Step 1: Create a GitHub Repository

1. Log into your account at [GitHub](https://github.com).
2. Click the **`+`** icon in the top right corner and select **New repository**.
3. Set your repository details:
   - **Repository name:** `viavika` (or `username.github.io` for a default root site).
   - **Visibility:** Select **Public** (GitHub Pages requires a public repository on free accounts).
   - **Initialize:** Leave "Add a README file" unchecked if you already have local files, or check it if you're uploading via browser.
4. Click **Create repository**.

---

## 📤 Step 2: Upload Application Files

### Option A: Upload via Web Interface (Easiest)
1. On your empty repository page, click **uploading an existing file**.
2. Drag and drop your file (`index.html`) into the file uploader.
3. Ensure the main HTML file is named exactly **`index.html`** in the root directory.
4. Click **Commit changes**.

### Option B: Push via Git CLI (Recommended for Developers)
Open your terminal in your project directory and run:

```bash
git init
git add index.html
git commit -m "Initial commit - ViaVika app"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/viavika.git
git push -u origin main
```

---

## ⚙️ Step 3: Enable GitHub Pages

1. Navigate to your repository on GitHub.
2. Click on the **Settings** tab at the top.
3. In the left sidebar, under **Code and automation**, click **Pages**.
4. Under **Build and deployment**:
   - **Source:** Select `Deploy from a branch`.
   - **Branch:** Select `main` (or `master`) and set folder to `/ (root)`.
5. Click **Save**.

> ⏳ **Deployment Time:** GitHub Actions will take 1–2 minutes to build your site. Refresh the page until you see a green banner displaying your published link:  
> `https://YOUR-USERNAME.github.io/viavika/`

---

## 🌐 Step 4: Configure a Custom Domain (Optional)

If you own a custom domain name (e.g., `viavika.com` or `app.yourdomain.com`):

### 1. Add Domain in GitHub Settings
1. Go to **Settings** > **Pages**.
2. Under **Custom domain**, enter your domain name (e.g., `viavika.com`).
3. Click **Save**. (GitHub will generate a `CNAME` file in your main branch automatically).

### 2. Configure DNS Records with your Domain Registrar
Add the following records in your DNS provider (Cloudflare, Namecheap, GoDaddy, etc.):

#### Apex Domain (`viavika.com`):
Add **4 A Records** pointing to GitHub’s IP addresses:
- `185.199.108.153`
- `185.199.109.153`
- `185.199.110.153`
- `185.199.111.153`

#### Subdomain (`app.viavika.com` or `www.viavika.com`):
Add a **CNAME Record**:
- **Name/Host:** `www` or `app`
- **Target/Value:** `YOUR-USERNAME.github.io`

### 3. Enforce HTTPS
Once DNS propagation completes (usually 5–15 minutes), check the **Enforce HTTPS** box under **Settings** > **Pages** to enable free SSL/TLS encryption.

---

## 🔒 Security & LocalStorage Notes

- **Offline Support:** GitHub Pages serves files over HTTPS by default, enabling Web Speech API (Voice Logging) and LocalStorage persistence without browser security blocks.
- **Privacy:** Since ViaVika stores data entirely inside browser `localStorage`, no financial or personal data is transmitted back to GitHub's servers.

---

## ❓ Frequently Asked Questions & Troubleshooting

| Issue | Cause | Solution |
| :--- | :--- | :--- |
| **404 Not Found** | Main file missing or misnamed | Verify the entry file is named `index.html` (lowercase) in the root directory. |
| **Changes not updating** | Browser caching or pending build | Check the **Actions** tab in GitHub for build status, or hard refresh (`Ctrl + Shift + R` or `Cmd + Shift + R`). |
| **Voice recognition failing** | Insecure context | Ensure you access the app over `https://` and not `http://`. |