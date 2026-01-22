# Continuous Delivery/Deployment (CD)
**Automate the running of the new code** (that has passed CI) **to the end user**
- **Delivery** is the automation of the entire process, but with a **manual approval right before Deployment** to end user
- **Deployment** is when the **entire process** is automated, **all the way to the end user**


### Jenkins CD
![GitHub-Jenkins full CI/CD pipeline diagram](diagrams/gh-jenkins-cicd-pipeline.png)
Developer pushes to `dev` branch and GitHub webhook triggers Jenkins job on agent node, running automated tests **(1)**. If tests pass and job completes successfully, second job runs and merges the `dev` branch to the `main` branch automatically **(2)**. On completion of the second job, the third job is triggered and this has an agent node deploy the updated code to an existing AWS EC2 instance **(3)** - this is via SSH into the target AWS instance, copying over the updated code **(delivery)**, then running it **(deployment)**.


### Jenkins SSH into target AWS EC2 instance, deploy changes
Refer to screenshots   
**Make new Jenkins job**
- Select **Copy from** and use the settings from job2
- Update the description
- **Retain all GitHub settings** - needs to clone down code from same repo
- **Update Build Triggers** to be on successful **job2 completion**
- Under **Post-build Actions**, **remove Git Publisher**
- **Build Environment, enable SSH Agent** (plugin)
    - **Add**
    - Kind: **SSH Username with private key**
    - Global scope
    - Fill in ID, Description and Username with descriptive name...
    - **Enter directly**: `cat aws-key-pair-name.pem` in terminal; **copy-paste this into field (include the dashes)**
    - **No passphrase**
- **Build Steps, Execute shell**:
```
rsync -avz -e "ssh -o StrictHostKeyChecking=no" nodejs20-se-test-app-2025/app ubuntu@{INSTANCE_PUBLIC_IP_HERE}:/home/ubuntu/

ssh -o "StrictHostKeyChecking=no" ubuntu@{INSTANCE_PUBLIC_IP_HERE} <<EOF
   ls
   cd app
   ls
   npm install
   pm2 kill
   pm2 start app.js
EOF
```


### Problems...
- If app instance runs with user data script...
    - `pm2` runs process, `port 3000` already being listened on - subsequent run will error out
- If not, there's no `npm install`, `pm2 start app.js`
    - No webpage displayed before first CI/CD run
- Jenkins cannot overwrite existing app data (does not have the permissions) - job3 will fail
- Jenkins using `sudo rsync ...` to get around permissions causes SSH disconnection
- Jenkins writing into new directory leads to first problem
    - Even with `pm2 kill`, the new process will still error out
    - `port 3000` already listened on, `--update-env` or other flags/reset commands don't fix this


