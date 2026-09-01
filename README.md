# Jenkins Learning Demo

A tiny Python project used to learn Jenkins pipelines from scratch.

## What's in here
- `calculator.py` — a small app with a few functions
- `test_calculator.py` — tests for it (uses `pytest`)
- `Jenkinsfile` — defines the Jenkins pipeline (Checkout → Setup → Test → Run App)

## Step 1: Push to GitHub
```bash
cd jenkins-learn-demo
git init
git add .
git commit -m "Initial commit: calculator app + Jenkinsfile"
git branch -M main
git remote add origin https://github.com/<your-username>/jenkins-learn-demo.git
git push -u origin main
```

## Step 2: Install Jenkins (if you haven't)
Easiest way locally, using Docker:
```bash
docker run -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```
Then open `http://localhost:8080` and follow the setup wizard
(it will show you a password to paste in, found in the container logs).

## Step 3: Create a Pipeline job
1. In Jenkins, click **New Item**
2. Name it `calculator-demo`, choose **Pipeline**, click OK
3. Scroll to **Pipeline** section → Definition: **Pipeline script from SCM**
4. SCM: **Git** → paste your GitHub repo URL
5. Branch: `*/main`
6. Script Path: `Jenkinsfile` (default, already correct)
7. Save, then click **Build Now**

## Step 4: Watch it run
Click the build number → **Console Output** to see each stage
(Checkout, Setup, Test, Run App) execute live. If a test fails,
you'll see exactly why in the log — try breaking a test on purpose
to see how a failed build looks.

## Where to go next
- Add a `Lint` stage (e.g. `flake8`)
- Trigger builds automatically on every GitHub push (needs a webhook
  or "Poll SCM")
- Add parameters, environment variables, or parallel stages
- Try a `Dockerfile` + build/push stage once comfortable
