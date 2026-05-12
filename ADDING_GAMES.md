# How to Add New Games - Quick Guide for Beam

## The Workflow (Every Time You Add a Game)

### Step 1: Create Your Game
Ask Claude to create an interactive game. Ask for:
- Self-contained HTML file (all CSS/JS inside)
- Back button linking to `../index.html`
- Responsive design

Save as: `games/your-game-name.html`

### Step 2: Edit games.json
Open `games.json` and add your game to the `games` array:

```json
{
  "id": "your-game-id",
  "title": "Your Game Title",
  "category": "Category (e.g., Biology, Chemistry)",
  "description": "1-2 sentence description of the game",
  "link": "games/your-game-name.html"
}
```

### Step 3: Test Locally (Optional)
1. Open `index.html` in your browser
2. Click on your game to test it
3. Make sure the back button works

### Step 4: Push to GitHub
```bash
# Add the changes
git add games.json games/your-game-name.html

# Create a commit with a description
git commit -m "Add: Your Game Title"

# Push to GitHub
git push origin main
```

**That's it!** Your game is live in ~30 seconds.

---

## Testing Featured Games

Want to test a new game as featured before making it permanent?

```json
{
  "featured": "your-new-game",  // ← Test this game
  "games": [...]
}
```

Then push and test. When ready:
- Keep it as featured, OR
- Change back to previous game

---

## File Naming Convention

**Keep it simple:**
- Use lowercase with hyphens: `cardiac-pathways.html`
- In `games.json` ID: use same name without `.html`: `"id": "cardiac-pathways"`
- Match the HTML filename to the ID

Example:
```
games/cardiac-pathways.html  →  "id": "cardiac-pathways"
games/drug-interactions.html  →  "id": "drug-interactions"
```

---

## Common Tasks

### Change Featured Game
```json
"featured": "new-game-id"
```
Push → Done!

### Remove a Game
1. Delete the HTML file from `games/` folder
2. Remove the object from `games` array in `games.json`
3. Push

### Edit Game Description
Open `games.json`, edit the `"description"` field for that game, push.

---

## Questions to Ask Claude

**When creating a game, ask:**

"Create a [game type] game for me. It should:
- Be self-contained (all CSS and JavaScript in one HTML file)
- Have a back button linking to ../index.html
- Be mobile responsive
- [Any other specifics]

Save it as games/[your-game-name].html"

**Example:**
"Create a chemistry quiz game about chemical reactions. It should have 10 questions, show score, and have a back button. The file should be games/chemistry-quiz.html"

---

## File Paths Quick Reference

| File | Purpose |
|------|---------|
| `index.html` | Main page (DO NOT EDIT for adding games) |
| `games.json` | Game list (EDIT THIS) |
| `games/*.html` | Your game files (CREATE THESE) |
| `.github/workflows/deploy.yml` | Auto-deploy (DO NOT EDIT) |
| `README.md` | Documentation |

---

## Deployment Automatic!

No need to manually deploy. Just push to `main` and GitHub automatically:
1. Detects the push
2. Runs the deployment workflow
3. Publishes to GitHub Pages

Check deployment status:
- GitHub → Actions tab
- Look for the latest workflow run
- Should show ✅ if successful

---

## Error Checklist

If your game doesn't appear on the site:

- [ ] `games.json` is valid JSON (no trailing commas)
- [ ] Game ID matches the filename (without .html)
- [ ] HTML file is in the `games/` folder
- [ ] Back button link is `../index.html`
- [ ] You pushed to `main` branch
- [ ] Check GitHub Actions for errors

---

## Your Games So Far

**Current games in games.json:**
1. Metabolic Pathways (featured)
2. Anatomy Quiz
3. Medical Terms
4. Patient Cases

Next game? Just follow the 4 steps above! 🚀
