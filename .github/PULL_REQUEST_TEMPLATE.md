---
title: "fix: repair Vercel build & deployment for builder-app"
body: |
  This PR prepares the repo for reliable deployments on Vercel by:
  - Adding vercel.json to force Create React App to be built via @vercel/static-build and use `build` as the output directory.
  - Adding .vercelignore to exclude root-level built artifacts that can cause Vercel to serve stale files instead of running a build.
  - Adding .gitignore for node_modules, build output and local env files.
  - Pinning Node engine in package.json to >=16.0.0 to ensure compatibility with react-scripts v5.
  - Replacing root-level built artifacts (index.html, App.js, index.js, manifest.json, service-worker.js) with placeholders so the repository's source files under `src/` and `public/` are authoritative.

  How to test locally:
  1. git checkout fix/vercel-deploy
  2. npm install
  3. npm run build
  4. npx serve -s build
  5. Open http://localhost:5000 and confirm the app loads.

  Post-merge checklist:
  1. Merge this PR to the default branch (e.g., main).
  2. Ensure Vercel triggers a new deployment. If it doesn't, trigger a redeploy in the Vercel dashboard or run `vercel --prod` from the CLI.
  3. Ensure any required environment variables are set in the Vercel project settings.

  Notes:
  - I intentionally avoided changing source files under `src/` or `public/`.
  - If runtime errors occur after deployment, share the Vercel build/runtime logs and I will diagnose further.

labels: |-
  automated-fix
---
