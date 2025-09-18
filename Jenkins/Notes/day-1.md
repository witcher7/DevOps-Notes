## ✅ Practice Q\&A Answers

### **Q1: What's the difference between Controller and Agent in Jenkins?**

| Controller (aka Master)                   | Agent (aka Node)                             |
| ----------------------------------------- | -------------------------------------------- |
| Brain of Jenkins – reads Jenkinsfile      | Executes the actual steps in the pipeline    |
| Manages UI, plugins, credentials, configs | Can run on Docker, VM, K8s Pod, etc.         |
| Decides what needs to run and where       | Does the dirty work – like building, testing |
| Can also run jobs (not recommended)       | Better for scalability and performance       |

---

### **Q2: Why Jenkins is better for self-hosted Kubernetes pipelines?**

* 🔌 1700+ Plugins to integrate with K8s, Helm, Terraform, Docker, Trivy, etc.
* 💥 Full control over agents: you can launch builds inside K8s pods with custom images
* 🔐 Secure secrets and infrastructure (can use Vault, SealedSecrets)
* 📦 Supports GitOps, Infra-as-Code, Canary/Blue-Green
* 💯 Ideal for complex multi-stage pipelines (unlike GitHub Actions which gets messy)

---

# 🔧 Step 4: Jenkins Installation (Start Lab)

Let’s install Jenkins in **Docker** first. It’s the easiest and cleanest for practice 💪

---

## 🚀 Install Jenkins on Docker (Step-by-Step)

### ✅ Requirements:

* Docker installed (`docker -v`)
* Port 8080 free

---

### 🧱 Step 1: Create Jenkins Home Volume

```bash
docker volume create jenkins_home
```

---

### ⚙️ Step 2: Run Jenkins Container

```bash
docker run -d \
  --name jenkins \
  -p 8080:8080 -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home \
  jenkins/jenkins:lts
```

* `8080`: Jenkins web UI
* `50000`: Agent to controller communication
* `jenkins_home`: Persistent config, plugins, jobs

---

### 🔐 Step 3: Get Initial Admin Password

```bash
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

🔑 Copy that password — you'll need it to log in

---

### 🌐 Step 4: Open Jenkins UI

Go to: [http://localhost:8080](http://localhost:8080)

* Paste the password
* Install **Suggested Plugins**
* Create admin user

---

### ✅ You’re Done When:

You can see the Jenkins dashboard like this:

```
| Jenkins |
+---------+
| Create New Job |
| Manage Jenkins |
| My Views       |
```
