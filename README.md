# 🚀 ansibleRoboshop: My Ansible Automation Journey 🛠️✨

Welcome! This repository showcases my hands-on automation of the Roboshop microservices stack using **Ansible**.  
Each playbook reflects my growth, troubleshooting wins, and practical DevOps experience. 🌱

---

## 📚 How I Learned

- 📝 [Official Ansible Documentation](https://docs.ansible.com/) for best practices and syntax.
- 🤖 ChatGPT for debugging help and YAML tips.
- 🔍 Trial and error with MongoDB and MySQL data loading.

---

## 🗂️ What’s Inside

### 📦 Playbooks for Microservices & Components

- 🍃 **mongodb.yaml** – Install & configure MongoDB
- 🐬 **mysql.yaml** – Install & secure MySQL
- 🧊 **redis.yaml** – Setup Redis
- 🐇 **rabbitmq.yaml** – Setup RabbitMQ
- 📦 **catalogue.yaml** – Node.js app with MongoDB ![Screenshot](images/Screenshot%202025-06-19%20010603.png)
- 👤 **user.yaml** – Node.js with MongoDB & Redis ![Screenshot](images/Screenshot%202025-06-19%20010631.png)
- 🛒 **cart.yaml** – Node.js with Redis & Catalogue ![Screenshot](images/Screenshot%202025-06-19%20010513.png)
- 🚚 **shipping.yaml** – Java app with MySQL ![Screenshot](images/Screenshot%202025-06-19%20011439.png)
- 💳 **payment.yaml** – Python app with RabbitMQ ![Screenshot](images/Screenshot%202025-06-19%20011511.png)
- 🌐 **frontend.yaml** – Nginx static frontend ![Screenshot](images/Screenshot%202025-06-19%20010603.png)

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

3. **Run a playbook  a specific component:**
 ```bash
ansible-playbook -i inventory.ini -e "ansible_user=<user>" -e "ansible_password=<password>" <component-playbook>.yaml

 ```
Replace `<component-playbook>` with e.g., `catalogue.yaml`.
-Example  🌟
```
ansible-playbook -i inventory.ini -e "ansible_user=<user>" -e "ansible_password=<password>" catalogue.yaml
```

## 🌟 My Favorite Moments
🎉 The first time all services started without errors!
🐞 Debugging and finally loading data into MongoDB and MySQL.
🤩 Seeing the Roboshop app running end-to-end, fully automated!
🤝 Join Me!
Feel free to fork, explore, and contribute.
Let’s automate and learn together! 🚀



   
