# 🚀 ansibleRoboshop: My Ansible Automation Journey 🛠️✨

Welcome to **ansibleRoboshop**!  
This repository is a showcase of my hands-on journey automating the Roboshop microservices stack using **Ansible**.  
From provisioning databases to configuring Node.js and Python apps, every playbook here reflects my learning, troubleshooting, and growth as a DevOps enthusiast! 🌱

---

## 📚 How I Learned

- 📝 **Ansible Documentation:**  
  I relied heavily on the [official Ansible documentation](https://docs.ansible.com/) for module usage, syntax, and best practices.
- 🤖 **ChatGPT:**  
  Whenever I hit a roadblock or error, I turned to ChatGPT for quick explanations, YAML fixes, and debugging tips.
- 🔍 **Trial & Error:**  
  Especially when loading data into MongoDB and MySQL, I experimented with different modules, shell commands, and error handling until things worked!

---

## 🗂️ What’s Inside

## 📦 Playbooks for Each Component

### 🍃 `mongodb.yaml` – Install & configure MongoDB

---

### 🐬 `mysql.yaml` – Install & secure MySQL

---

### 🧊 `redis.yaml` – Setup Redis

---

### 🐇 `rabbitmq.yaml` – Setup RabbitMQ

---

### 📦 `catalogue.yaml` – Node.js app with MongoDB  
![Catalogue UI](images/Screenshot%202025-06-19%20010603.png)

---

### 👤 `user.yaml` – Node.js app with MongoDB & Redis  
![User Setup 1](images/Screenshot%202025-06-19%20010631.png)  
![User Setup 2](images/Screenshot%202025-06-19%20010653.png)

---

### 🛒 `cart.yaml` – Node.js app with Redis & Catalogue  
![Cart Setup 1](images/Screenshot%202025-06-19%20010513.png)  
![Cart Setup 2](images/Screenshot%202025-06-19%20010726.png)

---

### 🚚 `shipping.yaml` – Java app with MySQL  
![Shipping Setup 1](images/Screenshot%202025-06-19%20011439.png)  
![Shipping Setup 2](images/Screenshot%202025-06-19%20010726.png)

---

### 💳 `payment.yaml` – Python app with RabbitMQ  
![Payment Setup 1](images/Screenshot%202025-06-19%20011511.png)  
![Payment Setup 2](images/Screenshot%202025-06-19%20011531.png)  
![Payment Setup 3](images/Screenshot%202025-06-19%20011554.png)

---

### 🌐 `frontend.yaml` – Nginx static frontend  
![Frontend UI](images/Screenshot%202025-06-19%20010603.png)

---

## 🖥️ Instances Overview

![Instance Overview](images/Screenshot%202025-06-19%20005635.png)

---

- **Service Files:**  
  - Systemd service files for each app (e.g., [`user.service`](user.service), [`cart.service`](cart.service), etc.)

- **Configs & Repos:**  
  - [`nginx.conf`](nginx.conf) for frontend  
  - [`mongo.repo`](mongo.repo), [`rabbitmq.repo`](rabbitmq.repo) for YUM repos

- **Inventory:**  
  - [`inventory.ini`](inventory.ini) – All hostnames and groups

---

## 🐞 Troubleshooting & Key Learnings

- **Module Usage:**  
  - Used `ansible.builtin.*` modules for most tasks (install, copy, user, file, service).
  - Leveraged `community.general.npm` for Node.js dependencies and `community.mysql.mysql_db` for MySQL data import.

- **Loading Data Challenges:**  
  - **MongoDB:**  
    - Loading initial data required using the `shell` module and careful handling of command output and conditions.
    - Example:
      ```yaml
      - name: check products loaded or not
        ansible.builtin.command: mongosh --host mongodb.srivenkata.shop --eval 'db.getMongo().getDBNames().indexOf("catalogue")'
        register: catalogue_output

      - name: load products
        ansible.builtin.shell: mongosh --host mongodb.srivenkata.shop < /app/db/master-data.js
        when: catalogue_output.stdout | int < 0
      ```
    - Faced issues with string/integer conversion and learned to use Jinja2 filters (`| int`).

  - **MySQL:**  
    - Used `community.mysql.mysql_db` to import SQL files.
    - Had to ensure MySQL was running and credentials were correct.

- **Common Errors & Fixes:**  
  - **User Module:**  
    - Learned about `system: true` and `create_home` options for system users.
  - **File Paths:**  
    - Used `remote_src: yes` for unarchiving files already present on the remote host.
  - **Service Reloads:**  
    - Always reloaded systemd after copying new service files.

- **Debugging Approach:**  
  - Checked Ansible output for failed tasks.
  - Used `ansible.builtin.debug` to print variables and outputs.
  - Searched Ansible docs and asked ChatGPT for error explanations.

---

## 💡 Tips for Learners

- 📖 **Read the Docs:**  
  The [Ansible documentation](https://docs.ansible.com/) is your best friend for understanding modules and options.
- 🧑‍💻 **Experiment:**  
  Try different modules and parameters—don’t be afraid to break things!
- 🤔 **Ask for Help:**  
  Use ChatGPT or community forums when stuck.
- 📝 **Document Everything:**  
  Keep notes on errors and solutions for future reference.

---

## 🏁 How to Use This Repo

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/ansibleRoboshop.git
   cd ansibleRoboshop
   ```
2. **Edit inventory.ini with your hostnames.**

3. **Run a playbook:**
 ```bash
ansible-playbook -i inventory.ini ansible-user=xyz ansible-password=--- catalogue.yaml
Repeat for each component!
 ```

## 🌟 My Favorite Moments
🎉 The first time all services started without errors!
🐞 Debugging and finally loading data into MongoDB and MySQL.
🤩 Seeing the Roboshop app running end-to-end, fully automated!
🤝 Join Me!
Feel free to fork, explore, and contribute.
Let’s automate and learn together! 🚀



   
