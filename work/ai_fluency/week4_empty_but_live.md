# Week 4 — Empty but Live

## Stack
- **Frontend Core:** Static HTML5
- **Styling:** Vanilla CSS3 (Custom properties, Flexbox layout, Responsive Viewports)
- **Typography:** Inter (Google Fonts)
- **Hosting / Infra Target:** GitHub Pages (Free static site hosting served from repo root)

## Local run
To preview and test the portfolio locally on your machine:

1. Open your terminal in the repository root directory:
   ```bash
   cd c:\Users\Admin\OneDrive\Desktop\Projects\Machine-Learning
   ```
2. Start Python's built-in HTTP web server:
   ```bash
   python -m http.server 8000
   ```
3. Open your browser and navigate to:
   [http://localhost:8000](http://localhost:8000)

## Deployment
The portfolio is designed for zero-config free deployment via **GitHub Pages**:

1. **Commit and Push to GitHub:**
   ```bash
   git add index.html work/ai_fluency/week4_empty_but_live.md
   git commit -m "feat(ai_fluency): add Week 4 near-blank live portfolio landing page and deployment guide"
   git push origin main
   ```
2. **Enable GitHub Pages in Repository Settings:**
   - Go to your GitHub repository: `https://github.com/AryaVengurlekar03/Machine-Learning`
   - Click **Settings** > **Pages** (in the left sidebar).
   - Under **Build and deployment** > **Source**, select **Deploy from a branch**.
   - Under **Branch**, select `main` branch and `/ (root)` folder.
   - Click **Save**.

3. GitHub Pages will build and deploy the site automatically in ~1-2 minutes.

## Expected live URL
Based on your GitHub username (`AryaVengurlekar03`) and repository name (`Machine-Learning`), the expected live public URL will be:
`https://aryavengurlekar03.github.io/Machine-Learning/`

*(Note: Do not mark deployed until you enable Pages in settings and verify the URL loads publicly).*

## Mobile verification
Once deployed, open `https://aryavengurlekar03.github.io/Machine-Learning/` on your mobile phone (iOS Safari or Android Chrome) to verify:
- Typography scale and readability
- Whitespace and container margins
- Monogram and role badge alignment
- Absence of horizontal scrolling

Take a screenshot on your phone and save it as `work/screenshots/week4_mobile.png` (or attach to submission).

## Assignment checklist
- [x] Near-blank portfolio created
- [x] Identity kit applied
- [x] Responsive layout
- [x] Local test passed
- [ ] Deployed to a real URL
- [ ] URL opened on phone
- [ ] Phone screenshot captured
- [x] Identity kit added to Claude Project
- [x] Case studies added to Claude Project
- [x] Content map added to Claude Project
