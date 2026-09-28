# Logistic Regression Visualizer (LR_2)

A single-page, single-file web app that teaches binary Logistic Regression step by step: click-to-add data points, train with real batch gradient descent, and watch the weight vector, decision boundary, and loss curve update live — nothing on the page is hard-coded, every number comes from the actual model.

This is a from-scratch rebuild against a detailed implementation spec (exact IDs, exact interaction modes, exact error messages, exact color roles), distinct from the [LR_1](../LR_1) visualizer.

## Files

- `index.html` — complete HTML, CSS, and JavaScript app (no build step, no dependencies)

## Run locally

Open `index.html` directly in a browser, or serve the folder with a simple local web server:

```bash
cd /Users/luchit/3rd-year/DA/LR_2
python3 -m http.server 8000
```

Then visit `http://localhost:8000/`.

## Deploying to GitHub Pages

```bash
cd /Users/luchit/3rd-year/DA/LR_2
git init
git add index.html README.md
git commit -m "Add logistic regression visualizer"
git branch -M main
git remote add origin <your-repo-url>
git push -u origin main
```

Then in the GitHub repo: **Settings → Pages → Source: `main` branch, `/ (root)`**. The page will be published at `https://<username>.github.io/<repo>/`.

## Layout

- **Header** — title, a beginner-friendly description, and a "How it works?" 6-step card.
- **Left column** (scrolls independently)
  - *Data Canvas* — normalized 0–1 coordinate space; classification regions and decision boundary drawn live.
  - *Controls* — dataset generator (Linearly Separable / Slightly Noisy), manual point modes (Add Class 0 / Add Class 1 / Delete Point), hyperparameter sliders (learning rate, max epochs, decision threshold), and Step / Play Until Convergence / Reset.
- **Right column** (scrolls independently)
  - *Model State* — live epoch, loss, learned parameters (w₁, w₂, b), a click-to-inspect "Current Prediction" breakdown (x₁, x₂, z, σ(z), predicted vs. true class), the sigmoid function with a reference table, and the classification rule.
  - *Loss Graph* — binary cross-entropy vs. epoch, auto-scaling, with hover tooltip.
- **Footer** — compact, group members and CEi KMITL.

## Interaction model

- **Add Class 0 / Add Class 1**: click empty canvas space to add a point of that class; clicking an existing point selects it as the "Current Prediction" point instead of stacking a duplicate.
- **Delete Point**: click an existing point to remove it.
- The decision boundary is hidden (`w₁ = w₂ = 0`) until the model has taken at least one training step.
- "Play Until Convergence" stops automatically when either max epochs is reached or the loss improvement stays under `0.00001` for 3 consecutive epochs, and can be stopped early.

## Features

- Manual point creation/deletion, two random dataset generators
- Adjustable learning rate, max epochs, and decision threshold — all live-labeled sliders
- Step-by-step training and automatic play-until-convergence with a real stop condition
- Real-time classification-region shading and decision-boundary line
- Live model-state panel: parameters, current-prediction math, sigmoid reference table, classification rule
- Auto-scaling loss graph with hover readout
- Input validation with clear error messages (no data, single-class data, max epochs reached)
- Dark theme, independent-scroll two-column layout, responsive, crisp canvases at any DPI
