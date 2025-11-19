# GitHub Pages Deployment Guide

This guide will help you deploy the Visual Hierarchy Carousel to GitHub Pages.

## Prerequisites

- A GitHub account
- Repository access with write permissions
- Basic understanding of Git

## Deployment Methods

### Method 1: Automatic Deployment (Recommended)

The repository includes a GitHub Actions workflow that automatically deploys to GitHub Pages.

**Steps:**

1. **Enable GitHub Pages in Repository Settings:**
   - Go to your repository on GitHub
   - Click on **Settings** → **Pages**
   - Under **Source**, select **GitHub Actions**
   - Save the settings

2. **Merge/Push to Main Branch:**
   - When you merge this PR to the `main` branch, the workflow will automatically trigger
   - The workflow file is located at `.github/workflows/deploy-pages.yml`
   - Check the **Actions** tab to monitor deployment progress

3. **Access Your Site:**
   - After successful deployment, your site will be available at:
   - `https://[username].github.io/[repository-name]/`
   - Example: `https://anacondy.github.io/25--3-pro-test/`

### Method 2: Manual GitHub Pages Setup

If you prefer not to use GitHub Actions:

1. **Go to Repository Settings:**
   - Navigate to **Settings** → **Pages**

2. **Configure Source:**
   - Under **Source**, select **Deploy from a branch**
   - Choose the `main` branch
   - Select the `/ (root)` folder
   - Click **Save**

3. **Wait for Deployment:**
   - GitHub will automatically build and deploy your site
   - This usually takes 1-2 minutes
   - Check the Pages settings for the deployment status

## Verifying Deployment

1. **Check Deployment Status:**
   ```bash
   # View deployment URL in Actions tab
   # Or check repository settings → Pages
   ```

2. **Test the Live Site:**
   - Open the GitHub Pages URL in your browser
   - Test keyboard navigation (arrow keys)
   - Test on mobile device (swipe gestures)
   - Verify all 6 cards are accessible
   - Check color theme transitions

3. **Common Issues & Solutions:**

   **Issue:** 404 Page Not Found
   - **Solution:** Ensure `index.html` is in the root directory
   - Check that GitHub Pages is enabled in settings

   **Issue:** CSS/JS Not Loading
   - **Solution:** Check file paths are relative (not absolute)
   - Verify all files are committed and pushed

   **Issue:** Fonts Not Loading
   - **Solution:** Google Fonts should load automatically
   - Check browser console for CORS errors

## Custom Domain (Optional)

To use a custom domain:

1. **Add CNAME Record:**
   - Create a `CNAME` file in the repository root
   - Add your domain name (e.g., `www.example.com`)

2. **Configure DNS:**
   - Add DNS records at your domain provider:
   ```
   Type: CNAME
   Name: www
   Value: [username].github.io
   ```

3. **Update GitHub Settings:**
   - Go to **Settings** → **Pages**
   - Enter your custom domain
   - Enable **Enforce HTTPS**

## Performance Optimization for Production

### 1. Minify Assets (Optional)

For production, you can minify CSS and JS:

```bash
# Install minifier
npm install -g minify

# Minify (if you want to optimize further)
# Note: The current implementation is already optimized
```

### 2. Enable Caching

GitHub Pages automatically handles caching, but you can add cache headers:

```html
<!-- Add to <head> section -->
<meta http-equiv="Cache-Control" content="public, max-age=31536000">
```

### 3. Optimize Images

If you add images in the future:
- Use WebP format for better compression
- Optimize with tools like ImageOptim or TinyPNG
- Use responsive images with `srcset`

## Monitoring

### View Analytics

1. **GitHub Pages Statistics:**
   - Basic traffic data available in **Insights** → **Traffic**

2. **Google Analytics (Optional):**
   ```html
   <!-- Add to <head> section -->
   <script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
   <script>
     window.dataLayer = window.dataLayer || [];
     function gtag(){dataLayer.push(arguments);}
     gtag('js', new Date());
     gtag('config', 'GA_MEASUREMENT_ID');
   </script>
   ```

## Troubleshooting

### Workflow Fails

If the GitHub Actions workflow fails:

1. Check the **Actions** tab for error messages
2. Verify workflow permissions:
   - Go to **Settings** → **Actions** → **General**
   - Ensure "Read and write permissions" is enabled

### Content Not Updating

If changes don't appear:

1. **Clear Browser Cache:**
   - Hard reload: `Ctrl+Shift+R` (Windows) or `Cmd+Shift+R` (Mac)

2. **Check Deployment Status:**
   - Wait for the deployment to complete (check Actions tab)
   - GitHub Pages can take 1-2 minutes to update

3. **Verify Git Push:**
   ```bash
   git log --oneline -5
   git push origin main
   ```

## Security Considerations

1. **HTTPS:** Always use HTTPS (GitHub Pages provides this automatically)
2. **No Sensitive Data:** Never commit API keys or secrets
3. **Content Security Policy:** Consider adding CSP headers for additional security

## Maintenance

### Regular Updates

1. **Keep Dependencies Updated:**
   - Currently using Google Fonts (automatically updated)
   - No npm packages to maintain

2. **Monitor Browser Compatibility:**
   - Test on latest browser versions periodically
   - Check caniuse.com for feature support

3. **Backup:**
   - Repository is automatically backed up by GitHub
   - Consider maintaining a local clone

## Support

If you encounter issues:

1. Check the [Wiki](./WIKI.md) for detailed documentation
2. Open an issue on GitHub
3. Review GitHub Pages [documentation](https://docs.github.com/en/pages)

---

**Congratulations!** Your glassmorphic design carousel is now live on GitHub Pages! 🎉
