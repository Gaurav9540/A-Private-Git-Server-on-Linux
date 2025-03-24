# A-Private-Git-Server-on-Linux

The objective of this project is to set up a private Git server on an AWS EC2 instance running Amazon Linux. This allows a team to securely manage code, enabling SSH-based authentication, repository hosting, and controlled access for collaborative development without relying on services like GitHub or GitLab.

Step 1: Install Git on Server

```ssh
yum update -y
```

```ssh
yum install git -y
```

Step 2: Create a Git User

```ssh
adduser <username>
```

```ssh
passwd <username>
```

add git to wheel group:
```ssh
usermod -aG wheel git
```

```ssh
su - git
```

Step 4: Set Up SSH Authentication   <br>
On Client Machine (Developer Laptop)  <br>
Generate an SSH key (if not already created):  <br>
```ssh
ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
```

Copy the public key:
```ssh
cat ~/.ssh/id_rsa.pub
```

On Git Server
Switch to the git user:
```ssh
sudo su - git
```

Create the .ssh directory and authorized_keys file:
```ssh
mkdir -p ~/.ssh
vim ~/.ssh/authorized_keys
```

Set correct permissions:
```ssh
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

Step 5: Create a Git Repository  <br>
On Git Server  <br>
Create a new directory for Git repositories:  <br>
```ssh
sudo mkdir -p /home/git/repos
sudo chown git:git /home/git/repos
cd /home/git/repos
```

Initialize a bare repository:
```ssh
git init --bare myproject.git
```


Step 6: Clone and Use the Repository  <br>
On Client Machine   <br>
Install git:  <br>
```ssh
yum install git -y
```

Clone the repository:  <br>
```ssh
git clone ssh://git@your-ec2-public-ip:/home/git/repos/myproject.git
```

Navigate to the project:
```ssh
cd myproject
```

Create a new file:
```ssh
echo "Hello Git Server" > README.md
```

Add and commit the file:
```ssh
git add README.md
git commit -m "Initial commit"
```

Push to the server:
```ssh
git push origin main
```

Check logs on server machine
```ssh
git log
```


