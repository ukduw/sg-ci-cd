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
placeholder
- placeholder

