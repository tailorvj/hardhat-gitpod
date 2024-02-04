# Devlog

## 2024-Feb-04 15:29

I started this new project under nodejs-projects/Web3/hardhat-gitpod.

I'm following the HardHat TypeScript setup guide on https://hardhat.org/hardhat-runner/docs/guides/typescript

### First step - Github and Gitpod

Before diving into the Hardhat setup instructions, which demand installing various npm modules (which I wouldn't like to do on my local system), I've set up a basic npm project with 

```bash
$ npm init -y
```

I created the following .gitpod.yml

```yaml
# List the start up tasks. Learn more https://www.gitpod.io/docs/config-start-tasks/
tasks:
  - name: Start development environment
    init: npm install
```

and created a basic .gitignore file to make sure node_modules and .env never get into source control

```
node_modules
.env
```

I'm documenting my work in this DEVLOG.md file and updating the [README.md](README.md) with setup and development instructions

#### Github

I created a new Github project on https://github.com/tailorvj/hardhat-gitpod

I used the following commands to push it to Github:

```bash
git init
git add .
git commit -m "default npm project setup for gitpod.io"
git branch -M main
git remote add origin git@github.com:tailorvj/hardhat-gitpod.git
git push -u origin main
```