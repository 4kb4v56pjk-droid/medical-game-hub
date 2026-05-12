# Learning Games Hub

A simple, easy-to-maintain website for sharing interactive learning games with friends. Built with HTML, JSON, and auto-deploy via GitHub Pages.

## Quick Start

### 1. Set Up GitHub Pages

1. Go to your repository settings (Settings → Pages)
2. Under "Build and deployment":
   - **Source**: Deploy from a branch
   - **Branch**: Select `main` and `/root` folder
   - Click "Save"

Your site will be live at: `https://yourusername.github.io/learning-games`

GitHub Actions will automatically deploy whenever you push to `main`.

---

## Adding a New Game

### 3 Simple Steps:

#### Step 1: Create the Game File
Ask Claude to create an interactive game. Save it as `games/your-game-name.html`

Example:
```bash
games/my-new-game.html
```

#### Step 2: Update games.json
Add one entry to the `games` array in `games.json`:

```json
{
  "id": "my-new-game",
  "title": "My Awesome Game",
  "category": "Category Name",
  "description": "Brief description of the game",
  "link": "games/my-new-game.html"
}
```

#### Step 3: Push to GitHub
```bash
git add games.json games/my-new-game.html
git commit -m "Add: My Awesome Game"
git push origin main
```

✅ Done! Your game is live in ~30 seconds.

---

## Changing the Featured Game

Simply change the `featured` ID in `games.json`:

```json
{
  "featured": "my-new-game",  // ← Change this ID
  "games": [...]
}
```

Perfect for testing! Update featured, push, test live, then change again.

---

## Project Structure

```
learning-games/
├── index.html              # Main page (loads all games automatically)
├── games.json              # Game list + featured game ID
├── games/
│   ├── metabolic-game.html
│   ├── anatomy-quiz.html
│   ├── medical-terms.html
│   └── patient-cases.html
├── .github/workflows/
│   └── deploy.yml          # Auto-deploy on push (GitHub Actions)
└── README.md               # This file
```

---

## How It Works

1. **index.html** loads `games.json`
2. JavaScript automatically renders:
   - The featured game (from `"featured"` ID)
   - All games in the grid (from `"games"` array)
3. Each game is a standalone HTML file in the `games/` folder

**No manual HTML editing needed!** Just update `games.json` and push.

---

## Game File Template

Your game HTML should be self-contained. Here's a minimal template:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Your Game Title</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        html, body {
            background: #FAFAF8;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            color: #3D3A36;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            padding: 2rem;
        }

        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 2rem;
            border-bottom: 1px solid #E8E4DC;
            padding-bottom: 1rem;
        }

        header h1 {
            font-size: 2rem;
            color: #3D3A36;
        }

        .home-btn {
            background: #7C6B5D;
            color: white;
            padding: 0.75rem 1.5rem;
            border: none;
            border-radius: 6px;
            text-decoration: none;
            font-weight: 500;
            cursor: pointer;
            transition: background 0.2s;
        }

        .home-btn:hover {
            background: #6B5B4D;
        }

        /* Your CSS here */
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Your Game Title</h1>
            <a href="../index.html" class="home-btn">Home</a>
        </header>

        <div id="game">
            <!-- Game content here -->
        </div>
    </div>
    
    <script>
        // Your JavaScript here
    </script>
</body>
</html>
```

### Tips:
- Keep all styles and scripts inside the file
- Include a Home button in the header (links to `../index.html`)
- Use the color scheme: cream (#FAFAF8), dark grey (#3D3A36), accent (#7C6B5D)
- Make it responsive (mobile-friendly)
- Test locally before pushing

---

## Customizing

### Change Colors
Edit the CSS variables in `index.html`:
```css
:root {
    --cream: #FAFAF8;
    --accent: #7C6B5D;
    /* etc. */
}
```

### Change Site Title/Description
Edit in `index.html`:
```html
<h1>Your Game Hub</h1>
<p>Your description here</p>
```

### Add Navigation
Edit the `<nav>` section in `index.html`

---

## Adding Game Logos

Each game needs a logo in `games.json`. The site supports SVG logos. Add your logo ID to the `createGameLogo()` function in `index.html`:

```javascript
function createGameLogo(gameId) {
    const logos = {
        'your-game-id': `
            <svg><!-- Your SVG here --></svg>
        `
    };
}
```

Or ask Claude to generate a custom logo!

---

## Troubleshooting

**Games won't load?**
- Check file names are spelled correctly in `games.json`
- Make sure `.html` files are in the `games/` folder
- Clear browser cache and refresh

**Game links broken?**
- Verify the `"link"` path in `games.json` matches your file location
- File paths should start with `games/`

**Site won't deploy?**
- Check GitHub Actions workflow is enabled (Settings → Actions)
- Verify branch is set to `main` in GitHub Pages settings
- Check for errors in GitHub Actions tab

---

## Contact

Made by Beam and Claude.
Any mistakes, contact LINE ID : beamchalit

---

## License

Free to use and modify!
