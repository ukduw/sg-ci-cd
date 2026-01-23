# Installing, running Jenkins server on AWS
1. **Launch an EC2 instance**
2. **Install Jenkins on that instance**
3. **Configure Jenkins** to **automatically spin up Jenkins agents** to run Jenkins jobs.
    - Then make **AMI/user data script** to automate the above


### Step-by-step
- **Launch EC2 instance**
    - **Key pair**
    - **Security group: ports 80, 22, 8080 open**
        - Allow inbound HTTP access from anywhere
        - Allow inbound SSH traffic from anywhere (preferably only from specific PC's public IP)
        - Jenkins runs on port 8080
    - **Ubuntu Server 24 AMI**
- **SSH into instance**
    - `sudo apt update`
    - `sudo wget -O /etc/yum.repos.d/jenkins.repo \ https://pkg.jenkins.io/rpm-stable/jenkins.repo`
    - `sudo rpm --import https://pkg.jenkins.io/rpm-stable/jenkins.io-2026.key`
    - `sudo apt upgrade -y`
    - `sudo apt install java-21-amazon-corretto -y` OpenJDK distro (Java is prerequisite for Jenkins)
    - `sudo apt install jenkins -y`
    - `sudo systemctl enable jenkins` enable Jenkins service to start at boot
    - `sudo systemctl start jenkins` start Jenkins as a service
        - `sudo systemctl status jenkins` to check state of Jenkins service
- 
- 
- 




