# 🚀 Docker Installation on Ubuntu EC2 (Production-Ready Approach)

## 🎯 Objective:

Install the latest **Docker CE (Community Edition)** on an **Ubuntu EC2 instance** using the official Docker repository and best practices.

---

## ✅ Step 1: System Preparation

Update the system and install prerequisite packages:

```bash
sudo apt-get update -y
sudo apt-get install -y ca-certificates curl gnupg lsb-release
```

---

## ✅ Step 2: Add Docker’s GPG Key

Create the keyring directory and import Docker’s GPG key:

```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
  sudo tee /etc/apt/keyrings/docker.asc > /dev/null
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

---

## ✅ Step 3: Add the Docker Repository

Configure APT to use Docker’s official stable repository:

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] \
  https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

---

## ✅ Step 4: Update APT Index

Refresh your package database with the Docker repo included:

```bash
sudo apt-get update
```

---

## ✅ Step 5: Install Docker Engine and Tools

Install Docker Engine along with essential plugins:

```bash
sudo apt-get install -y docker-ce docker-ce-cli containerd.io \
  docker-buildx-plugin docker-compose-plugin
```

---

## ✅ Step 6: Verify Installation

Test Docker by running a sample container:

```bash
sudo docker run hello-world
```

---

## ✅ (Optional) Configure Non-root Access

Add your user to the `docker` group to avoid using `sudo`:

```bash
sudo usermod -aG docker $USER
newgrp docker
```

---

## 🔄 Bonus: Remove Old Docker Installation (If Any)

If Docker was previously installed via `apt install docker.io`, clean it up:

```bash
sudo apt remove -y docker.io
sudo rm -rf /var/lib/docker
```

---

## 📝 Summary

| Task                       | Command or Result                           |
| -------------------------- | ------------------------------------------- |
| Update & prerequisites     | `apt-get update && install ca-certificates` |
| Add GPG key & repository   | `/etc/apt/keyrings/docker.asc`              |
| Install Docker CE          | Includes `buildx` & `compose` plugins       |
| Verify Docker installation | `docker run hello-world`                    |
| Optional: Enable non-root  | `usermod -aG docker $USER`                  |
