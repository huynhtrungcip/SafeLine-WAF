# 🔐 SafeLine WAF - Web Application Firewall

![Version](https://img.shields.io/badge/Version-1.0-blue)  
![Author](https://img.shields.io/badge/Author-Trung_Huynh-green)  
![Docker](https://img.shields.io/badge/Docker-Latest-blue)  
![License](https://img.shields.io/badge/License-MIT-green)  
![Contributions](https://img.shields.io/badge/Contributions-Welcome-orange)  

---

## 📖 **Description**

**SafeLine WAF** is a robust web application firewall designed to secure web services from threats like **SQL Injection**, **XSS**, and **Command Injection**. With its easy setup and management, SafeLine provides reliable protection for developers and system administrators.

---

## 🚀 **Installation Guide**

### 1️⃣ Install Docker and Docker Compose

#### Step 1: Update Your System
```bash
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
```

#### Step 2: Add the Docker Repository
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

#### Step 3: Install Docker
```bash
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io -y
```

#### Step 4: Start and Enable Docker
```bash
sudo systemctl start docker
sudo systemctl enable docker
```

#### Step 5: Install Docker Compose
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r .tag_name)/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

#### Step 6: Verify Docker and Docker Compose Installation
```bash
docker --version
docker-compose --version
```

---

### 2️⃣ Install SafeLine WAF

#### Step 1: Install SafeLine
Run the following command:
```bash
sudo bash -c "$(curl -fsSLk https://waf.chaitin.com/release/latest/setup.sh)"
```

#### Step 2: Access SafeLine
SafeLine runs on port **9443**. Access it via your browser:
- **URL**: `https://<Server-IP>:9443/`
The password will appear in the CLI section, please note
- **Username**: `admin`
- **Password**: `Example_password`

---

## 📋 **Configuration Guide**

### 🛠 Configure SafeLine to Protect DVWA

#### Step 1: Update Hosts File
Edit your system's `hosts` file to redirect domain traffic:

1. Open the `hosts` file for editing:
   - Path: `C:\Windows\System32\drivers\etc\hosts` (Windows)
2. Add the following line at the end of the file:
   ```
   Here I have an example
   192.168.100.100 192.168.100.101
   ```
   - `192.168.100.100`: SafeLine WAF IP
   - `192.168.100.101`: Domain or IP of OWASP BWA.
3. Save the file and close it.

#### Step 2: Add DVWA to SafeLine

1. Open SafeLine UI and navigate to **Web Services**.
2. Click **Add** and provide the following details:
For example, the IP address of DVWA 192.168.100.101
   - **Domain**: `192.168.100.101`
   - **Port**: `80`
   - **SSL Cert**: `None` (DVWA doesn't use HTTPS).
   - **Upstream**: `http://192.168.100.101:80`
4. Click **Save** to apply the configuration.

---

### 📊 Verify SafeLine Logs

#### Step 1: Access DVWA Through SafeLine
```bash
http://<IP-SafeLine>:80/
```
Replace `<IP-SafeLine>` with SafeLine's IP (e.g., `192.168.100.100`).

#### Step 2: Open SafeLine Logs
Navigate to the **Logs** tab in the SafeLine UI to check for incoming requests.

---

## 🔍 Testing WAF Protection

### Step 1: Login to DVWA
```bash
http://<IP-SafeLine>/
```
Use the default credentials:
- **Username**: `admin`
- **Password**: `password`

### Step 2: Enable Protection Rules
1. Open the **Rules** tab in SafeLine.
2. Activate critical rules, such as:
   - **SQL Injection**
   - **XSS**
   - **Command Injection**
3. Set **Run Mode** to `Security` or `Defense`.

### Step 3: Test with Malicious Requests
Example SQL Injection payload:
```sql
1' UNION SELECT user, password FROM users--+&Submit=Submit#
```
Check if SafeLine blocks the request and logs it.

---

## 👤 Author

Developed with ❤️ by [Trung Huynh](https://www.linkedin.com/in/trung-huynh-chi-pc01/)  

---

## 📜 License

This project is licensed under the MIT License. See the LICENSE file for details.

