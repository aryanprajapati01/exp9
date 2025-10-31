🎯 Set Up CI/CD Pipeline using GitHub Actions (for a Node.js/React App)

🏗️ Folder Structure your-repo/ │ ├── .github/ │ └── workflows/ │ └── main.yml │ ├── package.json ├── src/ └── ...

⚙️ Step 1: Create GitHub Actions Workflow File 📄 .github/workflows/main.yml name: CI/CD Pipeline

🔹 Trigger workflow on push to main branch
on: push: branches: [ main ]

jobs: build-and-deploy: runs-on: ubuntu-latest

steps:
  # 🧩 Step 1: Checkout code
  - name: Checkout repository
    uses: actions/checkout@v4

  # 🟢 Step 2: Set up Node.js
  - name: Set up Node.js
    uses: actions/setup-node@v4
    with:
      node-version: 18

  # 📦 Step 3: Install dependencies
  - name: Install dependencies
    run: npm ci

  # 🧪 Step 4: Run tests
  - name: Run tests
    run: npm test --if-present

  # 🏗️ Step 5: Build the project
  - name: Build project
    run: npm run build --if-present

  # 🚀 Step 6 (Optional): Deploy to GitHub Pages
  # Enable this if you want automatic deployment
  - name: Deploy to GitHub Pages
    if: success()
    uses: peaceiris/actions-gh-pages@v4
    with:
      github_token: ${{ secrets.GITHUB_TOKEN }}
      publish_dir: ./build
🧩 Step 2: Modify package.json (for React app)

Make sure your package.json has scripts for testing and building:

{ "scripts": { "start": "react-scripts start", "test": "react-scripts test --watchAll=false", "build": "react-scripts build" } }

🧰 Step 3: Optional — Configure for Deployment

If you’re using GitHub Pages, go to:

Repository Settings → Pages → Build and Deployment → GitHub Actions

and select the workflow you created.

If you use Netlify or AWS S3, replace the last step with the relevant deploy action:

Netlify: uses: nwtgck/actions-netlify@v2

AWS S3: uses: jakejarvis/s3-sync-action@v0.5.1

🚀 Step 4: Commit and Push git add . git commit -m "Add GitHub Actions CI/CD pipeline" git push origin main

Then go to your repo → Actions Tab → You’ll see the workflow run automatically.

✅ Expected Output

On every push to the main branch:

GitHub automatically installs dependencies.

Runs your tests.

Builds the project.

(Optionally) Deploys your build output.

Workflow status visible in the Actions tab: ✅ Success (green) or ❌ Failure (red).
