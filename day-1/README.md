# Continuous Integration / Continuous Delivery/Deployment (CI/CD)
Set of DevOps practices **automating the software delivery process**
- From code changes to deployment
- Allows for **faster, more frequent, more reliable software releases** via...
- **Automated builds, tests, deployments**

**CI focuses on merging code often**   
**CD handles releasing that tested code...**
- **Manually (Delivery)**
- Or, **automatically (Deployment)**

CI/CD key advantages:
- Faster releases
- More frequent testing (so typically less bugs)
- Better collaboration and fast feedback loops
- Reduced risk due to smaller, more frequent changes (as opposed to large, infrequent changes)


## CI/CD Pipeline
![CI/CD Pipeline diagram](../day-0/cicd/diagrams/CICD-Pipeline.webp)


### Continuous Integration (CI)
**Automation of push -> test -> merge** to main branch of source code/repo
- CI is completely isolated from CD (you can have an independent CI pipeline)


### Continuous Delivery/Deployment (CD)
**Automate the running of the new code** (that has passed CI) **to the end user**
- **Delivery** is the automation of the entire process, but with a **manual approval** right before Deployment to end user
- **Deployment** is when the **entire process** is automated, all the way to the end user



## Jenkins
**Open-source automation server/software** with a **very broad use case** (beyond just CI/CD) and a lot of **customizability (via plugins)** and **scalability**
- Also used in Data and Machine Learning
- Jenkins runs on a Control Server
- It then has Agent Nodes run tasks for it

Jenkins can also run on all OS's
- But this broadness also means it is **more complex than alternatives**
- Becomes **more difficult to maintain at scale**

**Code** from: **source code management (SCM)** (1) / version control   
**Jenkins**: CI/CD
- **Build** (2)
- **Test** (3)
- **Package** (4)
- **Deploy/Deliver** (5)
- **Monitor** (6)


