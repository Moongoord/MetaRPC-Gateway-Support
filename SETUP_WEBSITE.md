# How to Run the Documentation Website Locally

This guide explains how to preview the documentation website on your local machine.

## Prerequisites

You need to install Ruby and Jekyll to run the site locally.

### Option 1: Using Ruby (Recommended)

#### Windows:

1. **Install Ruby:**
   - Download RubyInstaller from: https://rubyinstaller.org/downloads/
   - Get the **Ruby+Devkit** version (e.g., Ruby+Devkit 3.2.X)
   - Run the installer and check "Add Ruby to PATH"
   - In the final step, run `ridk install` and press Enter

2. **Install Bundler:**
   ```bash
   gem install bundler
   ```

3. **Install dependencies:**
   ```bash
   cd c:\Users\malin\Support-for-your-code
   bundle install
   ```

4. **Run the site:**
   ```bash
   bundle exec jekyll serve
   ```

5. **Open in browser:**
   ```
   http://localhost:4000
   ```

#### Linux/Mac:

1. **Install Ruby:**
   ```bash
   # Ubuntu/Debian
   sudo apt-get install ruby-full build-essential

   # Mac (using Homebrew)
   brew install ruby
   ```

2. **Install Bundler:**
   ```bash
   gem install bundler
   ```

3. **Install dependencies:**
   ```bash
   cd ~/Support-for-your-code
   bundle install
   ```

4. **Run the site:**
   ```bash
   bundle exec jekyll serve
   ```

5. **Open in browser:**
   ```
   http://localhost:4000
   ```

---

### Option 2: Using Docker (Alternative)

If you don't want to install Ruby, use Docker:

1. **Install Docker Desktop:**
   - Windows: https://www.docker.com/products/docker-desktop/
   - Mac/Linux: Follow official Docker installation

2. **Run the site with Docker:**
   ```bash
   docker run --rm -v "%cd%":/srv/jekyll -p 4000:4000 jekyll/jekyll jekyll serve
   ```

3. **Open in browser:**
   ```
   http://localhost:4000
   ```

---

## Making Changes

1. **Edit files:**
   - Edit `.md` files in the repository
   - Changes to most files will auto-reload
   - Changes to `_config.yml` require restart

2. **See changes:**
   - The site will automatically rebuild when you save files
   - Refresh your browser to see changes
   - Check terminal for any build errors

3. **Stop the server:**
   - Press `Ctrl+C` in the terminal

---

## File Structure

```
Support-for-your-code/
├── _config.yml           # Site configuration
├── index.md              # Homepage
├── Gemfile               # Ruby dependencies
├── docs/
│   ├── index.md          # Documentation index
│   ├── FAQ.md            # FAQ page
│   └── common-issues/
│       ├── connection-problems.md
│       └── trading-errors.md
├── CONTRIBUTING.md       # Contributing guide
└── README.md            # Repository README
```

---

## Customization

### Change Theme

Edit `_config.yml`:
```yaml
theme: jekyll-theme-cayman

# Try other themes:
# theme: jekyll-theme-slate
# theme: jekyll-theme-minimal
# theme: jekyll-theme-architect
```

### Change Colors

Create `assets/css/style.scss`:
```scss
---
---

@import "{{ site.theme }}";

/* Custom styles */
.page-header {
  background: linear-gradient(120deg, #667eea 0%, #764ba2 100%);
}
```

### Add Custom Pages

Create new `.md` files in the root or `docs/` folder:
```markdown
---
layout: default
title: My Custom Page
---

# Content here
```

---

## Troubleshooting

### "bundle: command not found"
- Make sure Ruby is installed
- Run: `gem install bundler`

### "Could not find gem 'jekyll'"
- Run: `bundle install`

### Port 4000 already in use
- Use a different port: `bundle exec jekyll serve --port 4001`
- Or kill the process using port 4000

### Changes not showing
- Hard refresh: `Ctrl+Shift+R` (Windows) or `Cmd+Shift+R` (Mac)
- Restart Jekyll server
- Clear browser cache

---

## Deploying to GitHub Pages

Once you're happy with the site:

1. **Push to GitHub:**
   ```bash
   git add .
   git commit -m "Add documentation website"
   git push
   ```

2. **Enable GitHub Pages:**
   - Go to repository Settings
   - Scroll to "Pages"
   - Source: "Deploy from branch"
   - Branch: "main" and "/root"
   - Click "Save"

3. **Access your site:**
   ```
   https://yourusername.github.io/Support-for-your-code/
   ```

GitHub will automatically build and deploy your site!

---

## Next Steps

- Customize the theme and colors
- Add more documentation pages
- Test all links work correctly
- Deploy to GitHub Pages

For more Jekyll help: https://jekyllrb.com/docs/
