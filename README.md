# Jira + Jenkins + Kubernetes Demo Project

A hands-on beginner project demonstrating core DevOps and Agile practices: managing work with **Jira (Scrum & Kanban)**, automating builds with **Jenkins**, and deploying a containerized app using **Kubernetes (Minikube)**.

This repository serves as proof-of-work for learning and practicing an end-to-end Agile + CI/CD + Container Orchestration workflow.

---

## 📌 Project Overview

| | |
|---|---|
| **Goal** | Learn and demonstrate Agile project tracking + CI/CD + container orchestration fundamentals |
| **Tools used** | Jira, Jenkins, Docker, Kubernetes (Minikube), Git/GitHub |
| **Skill level** | Beginner |
| **Status** | ✅ Completed |

---

## 🗂️ What's Inside This Project

This project covers four connected pieces of a real-world software delivery workflow:

1. **Agile Project Management (Jira)** — Task planning and tracking using both Scrum (sprints) and Kanban (continuous flow) boards.
2. **Continuous Integration (Jenkins)** — An automated build job that runs whenever triggered, simulating a real CI pipeline.
3. **Container Orchestration (Kubernetes)** — A sample application deployed and exposed using a local Kubernetes cluster.
4. **Version Control (GitHub)** — This repository, hosting documentation and proof-of-work screenshots.

---

## 📁 Directory Structure

```
jira-jenkins-kubernetes-demo/
│
├── README.md                          # This file — project overview & documentation
│
├── docs/                              # Supporting documentation
│   ├── Jira-Jenkins-Kubernetes-Beginner-Guide.md   # Full step-by-step setup guide
│   └── Jira-Jenkins-Kubernetes-Revision-Notes.md   # Quick-reference notes/cheat sheet
│
└── screenshots/                       # Proof-of-work images
    ├── jira-scrum-board.png           # Screenshot of active Scrum sprint board
    ├── jira-kanban-board.png          # Screenshot of Kanban board
    ├── jira-backlog.png               # Screenshot of backlog with epics/stories
    ├── jenkins-successful-build.png   # Screenshot of green/successful Jenkins build
    └── kubernetes-running-app.png     # Screenshot of app running via Minikube
```

> This project was done primarily through the Jira, Jenkins, and Kubernetes UIs/CLIs directly on a local machine — no pipeline or manifest files were checked into version control. The repo mainly serves as a documented record of the work via screenshots.

---

## 🧩 Part 1: Jira — Agile Project Tracking

- Created a Scrum project (`MSDP`) with:
  - 1 Epic: *Set up CI/CD and Container Pipeline*
  - Multiple Stories/Tasks under the epic
  - A Sprint with tasks moved across **To Do → In Progress → Done**
- Created a separate Kanban project to practice continuous-flow task tracking

📸 See: `screenshots/jira-scrum-board.png`, `screenshots/jira-kanban-board.png`, `screenshots/jira-backlog.png`

---

## ⚙️ Part 2: Jenkins — Continuous Integration

- Installed Jenkins locally (`localhost:8080`)
- Created a Freestyle job (`sample-pipeline`) connected to this GitHub repo
- Ran a build that executes a simple shell command as a proof-of-concept CI step

📸 See: `screenshots/jenkins-successful-build.png`

---

## ☸️ Part 3: Kubernetes — Container Deployment

- Set up a local Kubernetes cluster using **Minikube**
- Deployed a sample containerized app (`hello-node`)
- Exposed it as a Service and accessed it via browser

📸 See: `screenshots/kubernetes-running-app.png`

The app was deployed directly via `kubectl create deployment` and `kubectl expose` commands (see the beginner guide in `docs/` for exact commands used).


---

## 🎯 Skills Demonstrated

- Agile Project Management (Scrum & Kanban) using Jira
- CI/CD fundamentals with Jenkins
- Containerization with Docker
- Container orchestration with Kubernetes (Minikube, kubectl)
- Version control with Git & GitHub
- Technical documentation

---

## 📄 License

This is a personal learning project and is free to use/reference for educational purposes.

---


**Your Name**
📧 anuska.dasguptaa@example.com
🔗 [LinkedIn](https://www.linkedin.com/in/anuska-dasgupta-232a30293/) | [GitHub](https://github.com/anu31d)
