# Continuous Delivery/Deployment (CD)
**Automate the running of the new code** (that has passed CI) **to the end user**
- **Delivery** is the automation of the entire process, but with a **manual approval right before Deployment** to end user
- **Deployment** is when the **entire process** is automated, **all the way to the end user**


### Jenkins CD
![GitHub-Jenkins full CI/CD pipeline diagram](diagrams/gh-jenkins-cicd-pipeline.png)
Developer pushes to `dev` branch and GitHub webhook triggers Jenkins job on agent node, running automated tests **(1)**. If tests pass and job completes successfully, second job runs and merges the `dev` branch to the `main` branch automatically **(2)**. On completion of the second job, the third job is triggered and this has an agent node deploy the updated code to an existing AWS EC2 instance **(3)** - this is via SSH into the target AWS instance, copying over the updated code **(delivery)**, then running it **(deployment)**.


### Jenkins SSH into target AWS EC2 instance
**step 1**
- placeholder

**step 2**
- placeholder

**step 3**
- placeholder

