# 🔐 GitHub Actions SSH Deployment Test

This project is a simple GitHub Actions workflow that demonstrates how to SSH into a remote server (e.g., AWS EC2, DigitalOcean Droplet) and run commands after a successful push to the `main` branch.



## 🚀 Workflow Summary

When you push code to the `main` branch:

1. GitHub Actions is triggered.
2. The workflow establishes an SSH connection to your remote server using a `.pem` key stored in GitHub Secrets.
3. It runs a command on the server to write a file at `/home/your-username/github-test/hello.txt`.

After the action runs, you can manually SSH into your instance and verify it worked by running:

```bash
cat /home/your-username/github-test/hello.txt
````

You should see:

```
Hello from GitHub Actions!
```


## 📁 Workflow File Structure

```
.github/
└── workflows/
    └── deploy.yml  <-- contains the GitHub Actions SSH workflow
```


## 🔐 GitHub Secrets Used
Secret Name and Description    
| `HOST`            | Public IP address of your server
| `USERNAME`        | SSH username (e.g., `ubuntu`)
| `SSH_PRIVATE_KEY` | Your PEM file contents (as tet)  

 
To set them up:

1. Go to your GitHub repo.
2. Click **Settings** > **Secrets and variables** > **Actions**.
3. Add each secret as shown above.

> Don't forget to remove `-----BEGIN PRIVATE KEY-----` and `\r\n` formatting issues when copying your PEM key.


## 🛠 Example SSH Command in Workflow

Here’s a simplified version of the SSH step:

```yaml
- name: Execute remote command
  uses: appleboy/ssh-action@v1.0.0
  with:
    host: ${{ secrets.HOST }}
    username: ${{ secrets.USERNAME }}
    key: ${{ secrets.SSH_PRIVATE_KEY }}
    script: |
      mkdir -p /home/${{ secrets.USERNAME }}/github-test
      echo "Hello from GitHub Actions!" > /home/${{ secrets.USERNAME }}/github-test/hello.txt
```


## ✅ Outcome

* ✅ Verified GitHub Actions workflow runs on push
* ✅ Successfully connects to server over SSH
* ✅ Creates a file remotely with a custom message


## 📌 Use Case

This is a foundation for:

* Zero-downtime deployments
* CI/CD pipelines using SSH
* Managing remote infrastructure automatically


## 💡 Author Notes

This project was built for DevOps learning and automation practice. Feel free to fork or adapt it for your own deployment workflows!

```
