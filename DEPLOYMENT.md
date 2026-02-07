# GitHub Pages Deployment Guide

## Quick Deploy Steps

### 1. Initialize Git Repository
```bash
cd c:\p\doc-cleaner
git init
git add index.html README.md .gitignore
git commit -m "Initial commit: DocPure AI static app"
```

### 2. Create GitHub Repository
1. Go to https://github.com/new
2. Name: `doc-cleaner` or `docpure-ai`
3. Don't initialize with README (we already have one)
4. Click "Create repository"

### 3. Push to GitHub
```bash
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO-NAME.git
git branch -M main
git push -u origin main
```

### 4. Enable GitHub Pages
1. Go to your repository on GitHub
2. Click "Settings" → "Pages"
3. Under "Source", select "Deploy from a branch"
4. Select branch: `main`
5. Select folder: `/ (root)`
6. Click "Save"

### 5. Access Your Site
Your site will be live at:
```
https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/
```

## Files Included for Deployment

✅ `index.html` - Main application (fully static, no server needed)
✅ `README.md` - Project documentation
✅ `.gitignore` - Git ignore rules

## Files NOT Needed (Excluded)

❌ `server.js` - Old Node.js backend (not needed anymore)
❌ `node_modules/` - Server dependencies (not needed)
❌ `package.json` - Server config (not needed)
❌ `uploads/`, `processed/` - Server directories (not needed)

## How It Works

The application now runs **100% in the browser**:

1. **Document Upload**: Uses HTML5 FileReader API
2. **Text Extraction**:
   - TXT: Native browser `.text()` method
   - DOCX: `mammoth.js` from CDN
   - PDF: `pdfjs-dist` from CDN
3. **Cleaning**: Pure JavaScript regex and string manipulation
4. **Document Generation**:
   - TXT: Blob API
   - DOCX: `docx` library from CDN
   - PDF: `pdf-lib` from CDN
5. **Download**: Blob URLs with `<a download>`

## Testing Locally

You can test the static version by simply opening `index.html` in your browser:

```bash
# Option 1: Direct open
start index.html

# Option 2: Python server (if you want a local server)
python -m http.server 8000

# Option 3: Node.js server (if you have npx)
npx http-server
```

Then visit `http://localhost:8000`

## Troubleshooting

### Issue: Libraries not loading
**Solution**: Check your internet connection. The app loads libraries from CDN.

### Issue: CORS errors
**Solution**: Use a local server (Python or npx http-server) instead of opening the file directly.

### Issue: PDF processing fails
**Solution**: Ensure the PDF is text-based, not scanned images.

## Performance Notes

- First load may be slower (downloading libraries from CDN)
- Subsequent loads are faster (browser caching)
- Large documents (>10MB) may take longer to process
- All processing is client-side, so performance depends on user's device

## Privacy & Security

✅ **No data leaves the user's browser**
✅ **No server-side processing**
✅ **No analytics or tracking**
✅ **Works offline after first load (with service worker)**

---

**Ready to deploy!** 🚀
