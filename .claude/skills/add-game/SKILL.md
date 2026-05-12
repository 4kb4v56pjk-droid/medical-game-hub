---
name: add-game
description: "Add a new interactive game to your Learning Games Hub website. Use this skill whenever you want to add a new game to your site—whether it's a medical quiz, interactive tool, learning module, or any educational game. The skill will guide you through: (1) creating the game HTML file, (2) registering it in games.json, (3) deploying it to GitHub Pages. The process takes ~5-10 minutes from idea to live game."
---

# Add Game to Learning Games Hub

Your Learning Games Hub uses a simple data-driven architecture: all games are registered in `games.json`, which automatically displays them on your site. Adding a new game requires three steps:

1. **Create the game HTML file** in the `games/` folder
2. **Add an entry to `games.json`** with game metadata
3. **Push to GitHub** to trigger auto-deployment

## Step 1: Create the Game HTML File

Create a new file in the `games/` folder with a descriptive name (use lowercase, hyphens instead of spaces).

**File location:** `games/your-game-name.html`

**Example:** `games/pharmacology-quiz.html`

### HTML Template

Use this self-contained template as your starting point:

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
            height: 100%;
            background: #FAFAF8;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            color: #3D3A36;
            line-height: 1.6;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            padding: 2rem;
        }

        header {
            margin-bottom: 2rem;
            border-bottom: 1px solid #E8E4DC;
            padding-bottom: 1rem;
        }

        header h1 {
            font-size: 2rem;
            margin-bottom: 0.5rem;
            color: #3D3A36;
        }

        .game-content {
            background: white;
            padding: 2rem;
            border-radius: 12px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.08);
        }

        .back-link {
            display: inline-block;
            margin-top: 2rem;
            color: #7C6B5D;
            text-decoration: none;
            font-weight: 500;
            transition: color 0.2s;
        }

        .back-link:hover {
            color: #3D3A36;
        }

        button {
            background: #7C6B5D;
            color: white;
            padding: 0.75rem 1.5rem;
            border: none;
            border-radius: 6px;
            font-size: 1rem;
            cursor: pointer;
            transition: background 0.2s;
        }

        button:hover {
            background: #6B5B4D;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Your Game Title</h1>
            <p>Brief description of what players will learn</p>
        </header>

        <div class="game-content">
            <h2>Instructions</h2>
            <p>Explain how to play your game here.</p>

            <!-- Your game content goes here -->
            <div id="game">
                <!-- Add your interactive content here -->
                <p>Game placeholder</p>
            </div>

            <a href="../index.html" class="back-link">← Back to Games Hub</a>
        </div>
    </div>

    <script>
        // Your game logic goes here
        console.log('Game loaded');
    </script>
</body>
</html>
```

### Key Requirements

- **Self-contained:** All CSS and JavaScript must be inline (no external files except the back-link)
- **Responsive:** Must work on mobile and desktop (use `max-width` and flexible layouts)
- **Back link:** Always include `<a href="../index.html">← Back to Games Hub</a>` so players can return
- **Color scheme:** Use the site colors: cream (#FAFAF8), beige (#F5EFE7), grey (#A89F96), dark grey (#3D3A36), accent (#7C6B5D)

## Step 2: Add Entry to games.json

Open `games.json` in your editor and add an entry to the `"games"` array:

```json
{
  "id": "your-game-id",
  "title": "Your Game Title",
  "category": "Category Name",
  "description": "A brief description of what players will learn (1-2 sentences)",
  "link": "games/your-game-name.html"
}
```

### Field Guide

- **id:** Unique identifier, lowercase with hyphens (must match your filename without `.html`)
- **title:** Display name shown on the card
- **category:** Type of game (e.g., "Biochemistry", "Clinical", "Vocabulary", "Biology")
- **description:** 1-2 sentence summary of what the game teaches
- **link:** Path to the HTML file relative to index.html (always `games/filename.html`)

### Example

```json
{
  "id": "pharmacology-quiz",
  "title": "Pharmacology Quiz",
  "category": "Pharmacology",
  "description": "Test your knowledge of drug interactions, dosing, and side effects with interactive scenarios.",
  "link": "games/pharmacology-quiz.html"
}
```

### Optional: Change the Featured Game

After adding your game, you can feature it on the homepage by changing the `"featured"` ID at the top of `games.json`:

```json
{
  "featured": "your-game-id",
  "games": [...]
}
```

This is useful for testing your new game before deciding which one to highlight.

## Step 3: Push to GitHub

Git commands to deploy your game:

```bash
# Stage your changes
git add games/your-game-name.html games.json

# Commit with a descriptive message
git commit -m "Add: Your Game Title"

# Push to deploy
git push origin main
```

Your game will be live on your site in **~30 seconds** after pushing!

## Optional: Add a Custom Logo

The site displays SVG logos for each game. You can add a custom logo in `index.html`'s `createGameLogo()` function:

```javascript
function createGameLogo(gameId) {
    const logos = {
        'your-game-id': `
            <svg width="80" height="80" viewBox="0 0 100 100" style="stroke: #7C6B5D; stroke-width: 2; fill: none; stroke-linecap: round;">
                <!-- Your SVG code here -->
            </svg>
        `
    };
}
```

Current logos in the site: metabolic-game, anatomy-quiz, medical-terms, patient-cases. Ask me to design a custom logo for your game, or leave it blank to use the default `?`.

## Verification Checklist

Before pushing, verify:

- [ ] HTML file is in `games/` folder with correct filename (matches `id` in games.json)
- [ ] games.json entry has all 5 fields (id, title, category, description, link)
- [ ] Back link in HTML points to `../index.html`
- [ ] Game works locally in your browser
- [ ] CSS and JavaScript are inline (no external dependencies except back-link)
- [ ] File is responsive (test at mobile size)

## Troubleshooting

**Game won't display?**
- Check file path in `link` field matches your filename exactly
- Verify `id` and filename use the same name (without `.html`)
- Clear your browser cache and hard-refresh (Cmd+Shift+R or Ctrl+Shift+R)

**Git push failed?**
- Make sure you're on the `main` branch: `git branch`
- Verify you've committed changes: `git status`
- Check your GitHub credentials are set up

**Site won't update after push?**
- GitHub Pages takes ~30 seconds to deploy; refresh after waiting
- Check GitHub Actions tab in your repo for deployment errors
- Verify your repo is set to deploy from `main` branch (Settings → Pages)

---

**Next steps:** Create your game HTML file, update games.json, test locally, then push to GitHub. Your game goes live automatically!
