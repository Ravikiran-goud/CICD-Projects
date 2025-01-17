# Setting Up Jenkins on AWS EC2 Instance

## **Launch an EC2 Instance**
1. Go to the **AWS Console**.
2. Navigate to **Instances (Running)**.
3. Click on **Launch Instances**.

---

## **Install Jenkins**
### **Pre-Requisites:**
- Install Java (JDK).

#### **Steps to Install Java**
1. Update the package list:
   ```bash
   sudo apt update
   ```
2. Install OpenJDK 17:
   ```bash
   sudo apt install openjdk-17-jre
   ```
3. Verify Java installation:
   ```bash
   java -version
   ```

---

### **Steps to Install Jenkins**
1. Add Jenkins repository key:
   ```bash
   curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
   /usr/share/keyrings/jenkins-keyring.asc > /dev/null
   ```
2. Add Jenkins repository:
   ```bash
   echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
   https://pkg.jenkins.io/debian binary/ | sudo tee \
   /etc/apt/sources.list.d/jenkins.list > /dev/null
   ```
3. Update package lists:
   ```bash
   sudo apt-get update
   ```
4. Install Jenkins:
   ```bash
   sudo apt-get install jenkins
   ```

---

### **Configure Security Group for Jenkins**
By default, Jenkins will not be accessible externally due to inbound traffic restrictions on AWS EC2. To allow traffic:

1. Go to **EC2 > Instances** and select your instance.
2. In the **Bottom Tabs**, click on **Security**.
3. Select **Security Groups**.
4. Edit inbound traffic rules to allow port `8080`:
   - Protocol: TCP
   - Port Range: 8080
   - Source: Anywhere (0.0.0.0/0) or your specific IP address.

---

### **Access Jenkins**
1. Get the public IP address of your EC2 instance from the AWS Console.
2. Access Jenkins at:
   ```
   http://<ec2-instance-public-ip>:8080
   ```
3. Copy the Jenkins Admin Password:
   ```bash
   sudo cat /var/lib/jenkins/secrets/initialAdminPassword
   ```
4. Paste the Administrator password to log in.

---

### **Post-Installation Setup**
1. Install Suggested Plugins:
   - Follow the prompts to install plugins.
2. Create the First Admin User:
   - It is recommended to create an admin user for future use.

---

## **Install Docker Pipeline Plugin in Jenkins**
1. Log in to Jenkins.
2. Navigate to **Manage Jenkins > Manage Plugins**.
3. Go to the **Available** tab and search for "Docker Pipeline".
4. Install the plugin.
5. Restart Jenkins after installation.

---

## **Docker Slave Configuration**
1. Install Docker:
   ```bash
   sudo apt update
   sudo apt install docker.io
   ```
2. Grant permissions to the Jenkins and Ubuntu users:
   ```bash
   sudo su -
   usermod -aG docker jenkins
   usermod -aG docker ubuntu
   systemctl restart docker
   ```
3. Restart Jenkins:
   ```bash
   http://<ec2-instance-public-ip>:8080/restart
   ```

The Docker agent configuration is now complete.

---

Your Jenkins setup is successful and ready to use!

