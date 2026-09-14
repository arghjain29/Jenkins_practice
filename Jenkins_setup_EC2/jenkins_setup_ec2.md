# Jenkins Setup on EC2

This guide shows how to install Jenkins on an EC2 Ubuntu instance using Java 21 and make it accessible through port 8080.

## Goal
Set up Jenkins on an AWS EC2 server so it runs successfully and can be opened in the browser at:

`http://<EC2_PUBLIC_IP>:8080`

## Prerequisites
- An Ubuntu EC2 instance
- SSH access to the instance
- Security group with port 22 enabled for SSH
- Java 21 installed

## Steps

### 1. Update the instance and install Java 21

```bash
sudo apt update
sudo apt install -y openjdk-21-jdk
java -version
```

If Java is installed correctly, you should see the OpenJDK 21 version in the output.

### 2. Install Jenkins LTS

#### Long Term Support release

A [LTS (Long-Term Support) release](https://www.jenkins.io/download/lts/) is chosen every 12 weeks from the stream of regular releases as the stable release for that time period. It can be installed from the [`debian-stable` apt repository](https://pkg.jenkins.io/debian-stable/).

```bash
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key

echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install jenkins
```

### 3. Start Jenkins

You can enable the Jenkins service to start at boot with the command:

```bash
sudo systemctl enable jenkins
```

You can start the Jenkins service with the command:

```bash
sudo systemctl start jenkins
```

You can check the status of the Jenkins service using the command:

```bash
sudo systemctl status jenkins
```

If everything has been set up correctly, you should see output similar to this:

```bash
Loaded: loaded (/lib/systemd/system/jenkins.service; enabled; vendor preset: enabled)
Active: active (running) since Tue 2018-11-13 16:19:01 +03; 4min 57s ago
```

To get the initial admin password, run:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Copy this password and paste it into the Jenkins setup page in the browser.

### 4. Add port 8080 in the EC2 security group

Go to the EC2 dashboard and follow these steps:

1. Open **Security Groups**.
2. Select the security group attached to your EC2 instance.
3. Click **Edit inbound rules**.
4. Add a new rule:
   - Type: **Custom TCP**
   - Port range: **8080**
   - Source: **0.0.0.0/0** or your own IP
5. Click **Save rules**.

This allows traffic to reach Jenkins on port 8080 from the browser.

## Final check

Open your browser and visit:

```text
http://<EC2_PUBLIC_IP>:8080
```

You should see the Jenkins unlock page. Once you enter the admin password, you can complete the Jenkins installation setup.

That’s it — Jenkins is now installed and running on your EC2 instance.
