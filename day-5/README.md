# Installing, running Jenkins server on AWS
1. **Launch an EC2 instance**
2. **Install Jenkins on that instance**
3. **Configure Jenkins** to **automatically spin up Jenkins agents** to run Jenkins jobs.
    - Then make **AMI/user data script** to automate the above


### 1. Launch EC2 instance
- **Key pair**
- **Default VPC, subnet**
- **Security group: ports 80, 22, 8080 open**
    - Allow inbound HTTP access from anywhere
    - Allow inbound SSH traffic from anywhere (preferably only from specific PC's public IP)
    - Jenkins runs on port 8080
- **t3micro/small**
- **Ubuntu Server 24 AMI**

### 2. SSH into instance
- `sudo apt update`
- `sudo wget -O /etc/yum.repos.d/jenkins.repo \ https://pkg.jenkins.io/rpm-stable/jenkins.repo`
- `sudo rpm --import https://pkg.jenkins.io/rpm-stable/jenkins.io-2026.key`
- `sudo apt upgrade -y`
- `sudo apt install java-21-amazon-corretto -y` OpenJDK distro (Java is prerequisite for Jenkins)
- `sudo apt install jenkins -y`
- `sudo systemctl enable jenkins` enable Jenkins service to start at boot
- `sudo systemctl start jenkins` start Jenkins as a service
    - `sudo systemctl status jenkins` to check state of Jenkins service
- `sudo cat /var/lib/jenkins/secrets/initialAdminPassword` initial admin password to unlock Jenkins in next step

### 3.1 Connect to `http://SERVER_PUBLIC_IP:8080`
- **Input the initial admin password**
- Installation script will redirect to **Customize Jenkins page**
- **Click install suggested plugins**
- Redirect to **Create First Admin User page**
    - Enter admin user info... (username, password, name, email)
- On left, select **Manage Jenkins**, **Manage Plugins**
    - Select the **Available tab**, enter **Amazon EC2 plugin** at top right
    - Select the **checkbox next to Amazon EC2 plugin**
    - Select **Install without restart**
- After installation, select **Back to Dashboard**

### 3.2 Select **Configure a cloud** (if there are no existing nodes/clouds)
- ( **If nodes/clouds have already been set up**, select **Manage Jenkins** on the left -> **Manage Nodes and Clouds** -> **Clouds** )
- Select **Add a new cloud**, **Amazon EC2**
    - Click **Add** under **Amazon EC2 Credentials**
        - Kind: **AWS Credentials**
        - Fill in **Access Key ID** and **Secret Access Key**
    - Region: e.g. **eu-west-1**
    - Click **Add** under **EC2 Key Pair's Private Key**
        - Kind: **SSH Username with private key**
        - Username: **ec2-user**
        - Select **Enter Directly** under **Private Key**, cat and copy-paste (including the `-----BEGIN RSA PRIVATE KEY-----` and `-----END RSA PRIVATE KEY-----`) the key, then **Add**
    - Click **Test Connection**
    - If `Success`, select **Save**




