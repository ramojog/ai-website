Jose Ramos
Demonstration of deploying website to github pages.
# AI Website
## Purpose
This project is for my DevOps 320 class.  
It is a simple website I made using AI.  
I learned how to upload files to GitHub and publish a live website.
## Steps I Took
1. I installed Git on my computer.  
2. I opened PowerShell and went to my website folder.  
3. I typed `git init` to start Git.  
4. I added my files using `git add .`  
5. I saved my changes with `git commit -m "Initial commit"`  
6. I made a new public repo on GitHub called **ai-website**.  
7. I connected it with  
   `git remote add origin https://github.com/ramojog/ai-website.git`  
8. I pushed my files using  
   `git branch -M main`  
   `git push -u origin main`  
9. I turned on GitHub Pages in Settings → Pages to make my site live.  
## Challenges
- I got an error message about "main" not matching any branch.  
  I fixed it by renaming my branch with `git branch -M main`.  
- My website first showed a 404 page.  
  I fixed this by waiting a few minutes for GitHub Pages to build and deploy.  

---

## GitHub Actions Workflow Setup

### Overview
I set up a GitHub Actions workflow to automatically deploy my website to GitHub Pages whenever I push changes to the main branch. This automates the deployment process and ensures the live site is always up-to-date.

### Steps to Set Up the Workflow

1. **Created the Workflow Directory**
   - Created a `.github/workflows` directory in the root of my repository
   - This is where GitHub Actions looks for workflow configuration files

2. **Created the Workflow File**
   - Created a new file named `deploy.yml` in `.github/workflows/`
   - This YAML file defines the deployment workflow

3. **Configured the Workflow**
   - Set the workflow to trigger on pushes to the `main` branch
   - Used the `actions/checkout@v4` action to check out the repository code
   - Configured the workflow to use `actions/upload-pages-artifact@v3` to package the website files
   - Used `actions/deploy-pages@v4` to deploy the artifact to GitHub Pages
   - Set proper permissions for the workflow (contents: read, pages: write, id-token: write)

4. **Enabled GitHub Pages**
   - Went to repository Settings → Pages
   - Selected "GitHub Actions" as the source for deployment
   - This allows GitHub Actions to deploy directly to GitHub Pages

5. **Committed and Pushed the Workflow**
   - Added the workflow file using `git add .github/workflows/deploy.yml`
   - Committed with `git commit -m "Add GitHub Actions deployment workflow"`
   - Pushed to GitHub with `git push origin main`

### Challenges and Solutions

**Challenge 1: Understanding Workflow Syntax**
- **Problem**: I was initially unfamiliar with YAML syntax and GitHub Actions structure
- **Solution**: I reviewed the GitHub Actions documentation and used example workflows as templates. I learned that proper indentation is critical in YAML files.

**Challenge 2: Permissions Configuration**
- **Problem**: The workflow initially failed with a permissions error when trying to deploy to GitHub Pages
- **Solution**: I added the correct permissions block to the workflow file:
  ```yaml
  permissions:
    contents: read
    pages: write
    id-token: write
  ```

**Challenge 3: Pages Source Configuration**
- **Problem**: GitHub Pages wasn't set up to accept deployments from GitHub Actions
- **Solution**: I changed the deployment source in Settings → Pages from "Deploy from a branch" to "GitHub Actions"

**Challenge 4: Artifact Upload Path**
- **Problem**: I needed to specify which files to deploy
- **Solution**: I configured the upload-pages-artifact action to use the root directory (`.`) which includes all website files (HTML, CSS, JavaScript)

**Challenge 5: Workflow Testing**
- **Problem**: I needed to verify the workflow was working correctly
- **Solution**: I made a small change to the website and pushed it. I then monitored the Actions tab to watch the workflow run and verified the deployment was successful.

### How to Trigger the Deployment

The deployment workflow runs automatically, but here are the different ways to trigger it:

#### Automatic Trigger (Recommended)
1. Make changes to your website files (HTML, CSS, JavaScript, etc.)
2. Stage your changes: `git add .`
3. Commit your changes: `git commit -m "Your commit message"`
4. Push to the main branch: `git push origin main`
5. The workflow will automatically run and deploy your changes
6. Visit the Actions tab to monitor the deployment progress
7. Once complete, your changes will be live at: https://ramojog.github.io/ai-website/

#### Manual Trigger
1. Navigate to the "Actions" tab in your GitHub repository
2. Select the "Deploy to GitHub Pages" workflow
3. Click "Run workflow" button
4. Select the branch (main)
5. Click "Run workflow" to start the deployment

#### Monitoring the Deployment
1. Go to the "Actions" tab in your repository
2. Click on the most recent workflow run
3. Watch the progress of each job (build, deploy)
4. Check for any errors in the logs if the deployment fails
5. Once the workflow shows a green checkmark, your site is deployed

### Workflow File Location
The workflow configuration file is located at: `.github/workflows/deploy.yml`

### Benefits of Using GitHub Actions
- **Automation**: No need to manually deploy after every change
- **Consistency**: Same deployment process every time
- **Version Control**: Deployment configuration is version controlled
- **Visibility**: Easy to see deployment history and status
- **Fast**: Deployments happen within minutes of pushing changes

### Live Website
The website is automatically deployed to: https://ramojog.github.io/ai-website/
