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
- Jenkins runs on a Control Node on the server
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


### Pipeline
Typical pipeline is made up of **3 Jenkins jobs**:
1. **Source Code Management (SCM) + Build (CI)**
    - Getting Jenkins to go to the right (private) repo, build that code...
    - Webhook + Jenkins listener
2. **Test + Merge if tests pass (CI)**
3. **Deploy to AWS (CD)** (or CDE - Deploy to Environment)
    - No manual approval


### Use
Refer to `jenkins-job-screens` screenshots for job-making/chaining


### SSH key pairs for GitHub -> Jenkins and webhook
**SSH key pair local generation**:   
`ssh-keygen -t rsa -b 4096 -C "name@email.com`
- **RSA encryption** (-t to specify type)
- **4096 bits** (-b to specify key length)
- -C ("comment") flag to **add email**

**Adding public key to GitHub repo**:
- Enter filename and passphrase (**empty** for Jenkins, since it cannot input passwords)   
- Go to **Settings > Deploy keys** tab in relevant **repo**   
- **Add deploy key**
- Run `cat name-of-key.pub` and copy-paste the contents into the Key field on GitHub (careful with whitespace)
- **Allow write access**

**Webhook**:
- **Webhook tab** on left
- Add webhook
- Fill in Jenkins payload URL (can be sent to multiple servers) with `github-webhook/` on the end
    - i.e. `http://server-ip-address:8080/github-webhook/`
- Content type: `application/x-www-form-urlencoded`
- Secret: [**blank**]
- SSL verification ideally enabled, but disable for basic testing
- **Just the push event** should **trigger** this webhook
- Active
- Add webhook


Adding private key to Jenkins:
Refer to screenshots
- Make new job and put in GitHub repo under GitHub project URL
    - NOTE: put `/` after the URL - i.e. `https://github.com/username/repo-name/`
- Check Git under Source Code Management
- Input the repo's SSH URL
- Select SSH Username with private key, global scope, input ID/Description/Username
- Private key, enter directly:
- `cat name-of-key-no-pub` again and copy-paste the contents, including the ----- START ----- and ----- END -----
- Remember to change `*/master` branch to `*/dev`
- Under Build Environment, check Provide Node & npm bin/ folder to PATH (plugin)
- Change NodeJS Installation to version 20
- Build triggers: GitHub hook trigger for GITScm polling
- Add cd, npm install and npm test commands to Execute Shell


