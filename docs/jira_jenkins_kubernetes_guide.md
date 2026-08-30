# Beginner's Guide: Jira Project + Jenkins + Kubernetes (Scrum & Kanban)

This guide walks you through everything, step by step, assuming you have never done any of this before. By the end you will have hands-on experience with:

- Creating a sample Jira project (with both Scrum and Kanban boards)
- Installing and running Jenkins on your laptop
- Installing and running Kubernetes (via Minikube) on your laptop

Take your time. Do one part at a time, and don't rush to the next section until the current one works.

---

## Before You Start: What You Need

- A laptop (Windows, Mac, or Linux) with at least 8GB RAM (Kubernetes/Minikube needs some resources)
- Internet connection
- An email address (for signing up to Jira/Atlassian)
- About 3 to 4 hours total, can be split across days

---

# PART 1: Create a Sample Jira Project

Jira is a project management tool made by Atlassian, used for tracking tasks using Scrum or Kanban methods.

## Step 1.1: Sign Up for Jira (Free)

1. Go to **https://www.atlassian.com/software/jira**
2. Click **"Get it free"**
3. Sign up using your email (or Google account). This creates your Atlassian account.
4. You will be asked to create a **"site name"**. This becomes your workspace URL, e.g. `yourname.atlassian.net`. Pick anything available.
5. Atlassian will ask "What team are you on?" Choose **Software** or **Engineering** (this gives you the dev-focused templates).

## Step 1.2: Create Your First Project

1. Once logged in, click **"Create project"** (usually a button on the left sidebar or homepage).
2. You will see templates. Choose **"Scrum"** first (we will add a Kanban board too, later).
3. Give your project a name, e.g. `My Sample DevOps Project`.
4. Jira auto-generates a **Project Key** (like `MSDP`). This prefixes all your task IDs (e.g. `MSDP-1`).
5. Click **Create**.

You now have an empty Scrum project.

## Step 1.3: Create Epics, Stories, and Tasks

Think of it like a tree:
- **Epic** = a big goal (e.g. "Set up CI/CD Pipeline")
- **Story** = a user-facing feature under that epic (e.g. "As a developer, I want automated builds")
- **Task/Sub-task** = the actual small to-do item (e.g. "Install Jenkins")

Steps:
1. In the left sidebar, click **Backlog**.
2. Click **"Create Epic"**. Name it: `Set up CI/CD and Container Pipeline`.
3. Click **"Create"** (the + button) to add issues under it:
   - Issue type: **Story**: "Install and configure Jenkins"
   - Issue type: **Story**: "Deploy sample app using Kubernetes"
   - Issue type: **Task**: "Write documentation"
4. Link each Story/Task to the Epic (there is an "Epic" field when creating/editing the issue).

Create at least 5 or 6 issues so your project has a realistic amount of content to practice with.

## Step 1.4: Set Up a Sprint (Scrum)

1. Go to **Backlog**.
2. Click **"Create Sprint"**.
3. Drag 3 or 4 of your issues from the backlog into the sprint.
4. Click **"Start Sprint"**. Set a duration (e.g. 1 week) and click **Start**.
5. Go to the **Active Sprint / Board** view. You will now see columns: **To Do, In Progress, Done**.
6. Drag a task from "To Do" to "In Progress", then to "Done". This simulates real sprint work.

## Step 1.5: Add a Kanban Board Too

Since this guide covers both Scrum and Kanban experience:

1. On the left sidebar, click **Project settings** (gear icon), then **Features**.
2. Enable **Kanban** (some Jira plans let you add a second board directly).
   - Alternative simpler method: Create a **second project** using the **Kanban template** (repeat Steps 1.1 to 1.2 but pick "Kanban" as the template). Name it `My Sample Kanban Project`.
3. In the Kanban project, create a few issues directly (no sprints needed in Kanban, it is a continuous flow board).
4. Move cards across columns: **Backlog, To Do, In Progress, Done**.

**Key difference to remember (good for interviews too):**
- **Scrum**: work is planned in fixed-length sprints with a sprint goal.
- **Kanban**: continuous flow, no fixed sprints, focus on limiting work-in-progress.

---

# PART 2: Install Jenkins on Your Laptop

Jenkins is an automation server used for CI/CD (Continuous Integration/Continuous Deployment). It automatically builds, tests, and deploys your code.

## Step 2.1: Install Java (Jenkins requires it)

Jenkins needs Java 11 or 17.

**On Windows:**
1. Go to **https://adoptium.net/**
2. Download the **Temurin JDK 17 (LTS)** installer for Windows.
3. Run the installer, click Next through the setup, and make sure **"Set JAVA_HOME variable"** is checked.
4. Verify: open Command Prompt and type:
   ```
   java -version
   ```
   You should see a version number like `17.x.x`.

**On Mac:**
1. Install Homebrew first if you don't have it. Open Terminal and run:
   ```
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```
2. Then install Java:
   ```
   brew install openjdk@17
   ```
3. Verify:
   ```
   java -version
   ```

## Step 2.2: Download and Install Jenkins

**On Windows:**
1. Go to **https://www.jenkins.io/download/**
2. Under "Windows", download the `.msi` installer.
3. Run it, keep default options, and note the **install directory** (usually `C:\Program Files\Jenkins`).
4. It will automatically open your browser to `http://localhost:8080`.

**On Mac:**
1. Easiest way, using Homebrew:
   ```
   brew install jenkins-lts
   brew services start jenkins-lts
   ```
2. Open your browser and go to `http://localhost:8080`.

**On Linux (Ubuntu/Debian):**
```
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list
sudo apt-get update
sudo apt-get install jenkins
sudo systemctl start jenkins
```

## Step 2.3: Unlock Jenkins

1. When you open `http://localhost:8080`, it asks for an **"Administrator password"**.
2. Find it:
   - **Windows**: `C:\Program Files\Jenkins\secrets\initialAdminPassword`
   - **Mac/Linux**: run `sudo cat /var/lib/jenkins/secrets/initialAdminPassword` (Linux) or check `/usr/local/var/lib/jenkins/secrets/initialAdminPassword` (Mac Homebrew path)
3. Open that file, copy the long password string, and paste it into the browser.
4. Click **"Install suggested plugins"** and wait for it to finish.
5. Create your admin username and password when prompted.
6. Click **"Save and Finish"**, then **"Start using Jenkins"**.

## Step 2.4: Create Your First Jenkins Job

1. Click **"New Item"** (top left).
2. Name it: `sample-pipeline`.
3. Choose **"Freestyle project"** (simplest for beginners), then click OK.
4. Under **"Build Steps"**, click **"Add build step"**, then **"Execute shell"** (Mac/Linux) or **"Execute Windows batch command"** (Windows), and type:
   ```
   echo "Hello from Jenkins! Build successful."
   ```
5. Click **Save**.
6. Click **"Build Now"** on the left.
7. Click the build number (e.g. `#1`), then **"Console Output"** to see it run.

If it works, you have just run your first automated build job.

---

# PART 3: Install Kubernetes on Your Laptop (via Minikube)

Kubernetes (K8s) manages containerized applications. Installing full Kubernetes on a laptop is not practical, so we use **Minikube**, which runs a small single-node Kubernetes cluster locally. This is the standard way beginners learn K8s.

## Step 3.1: Install a Container Tool (Docker Desktop)

Minikube needs a container runtime.

1. Go to **https://www.docker.com/products/docker-desktop/**
2. Download Docker Desktop for your OS (Windows/Mac).
3. Install it, then open Docker Desktop and let it finish starting up (icon in taskbar/menu bar should say "running").
4. Verify in terminal/command prompt:
   ```
   docker --version
   ```

## Step 3.2: Install kubectl (Kubernetes command-line tool)

**Windows** (using PowerShell):
```
curl.exe -LO "https://dl.k8s.io/release/v1.30.0/bin/windows/amd64/kubectl.exe"
```
Then move `kubectl.exe` to a folder that is in your PATH, or just run it from that folder.

**Mac:**
```
brew install kubectl
```

**Linux:**
```
curl -LO "https://dl.k8s.io/release/v1.30.0/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

Verify:
```
kubectl version --client
```

## Step 3.3: Install Minikube

**Windows** (PowerShell as Administrator):
```
winget install Kubernetes.minikube
```
(If `winget` is not available, download the installer directly from **https://minikube.sigs.k8s.io/docs/start/**)

**Mac:**
```
brew install minikube
```

**Linux:**
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

## Step 3.4: Start Your Cluster

```
minikube start
```

This downloads a small VM/container image and starts a single-node Kubernetes cluster. The first time may take a few minutes.

Verify it is running:
```
kubectl get nodes
```
You should see one node listed with status `Ready`.

## Step 3.5: Deploy a Sample App

1. Deploy a simple pre-built demo app:
   ```
   kubectl create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.39 -- /agnhost netexec --http-port=8080
   ```
2. Expose it as a service:
   ```
   kubectl expose deployment hello-node --type=LoadBalancer --port=8080
   ```
3. Check it is running:
   ```
   kubectl get pods
   kubectl get services
   ```
4. Open it in your browser:
   ```
   minikube service hello-node
   ```
   This opens your browser showing the running app.

---

## Troubleshooting Tips

- **Jenkins won't open on localhost:8080**: Make sure nothing else is using port 8080, and check if the Jenkins service is actually running.
- **`minikube start` fails**: Make sure Docker Desktop is running first. Try `minikube delete`, then `minikube start` again.
- **`kubectl` command not found**: Double check it is installed and added to your system PATH. Restart your terminal after installing.
- **Jira project template missing "Kanban"**: Just create a second project and pick Kanban as its template type.

Work through this guide once, and you will have hands-on, not just theoretical, experience with tools that show up in almost every DevOps/SWE job posting.
