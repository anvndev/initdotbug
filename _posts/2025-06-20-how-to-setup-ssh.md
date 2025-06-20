---
title: "How to Set Up SSH for GitHub on macOS/Linux"
date: 2025-06-20
categories: ["Dev Setup & Tools"]
tags: ["ssh", "git", "github", "security", "cheatsheet"]
reading_time: 5
image: "https://raw.githubusercontent.com/andev0x/description-image-archive/45c20a891cfc1a934ad645bc11288c652aa93736/initdotbug/p2.png"
excerpt: "A step-by-step guide to setting up SSH authentication for GitHub on macOS and Linux. Secure your Git workflow and say goodbye to typing passwords."
---

# How to Set Up SSH for GitHub on macOS/Linux 🔐

Using SSH keys with GitHub enhances your security and streamlines your Git workflow by eliminating the need to enter your username and password every time. In this guide, I’ll walk you through setting up SSH authentication for GitHub on **macOS** and **Linux**.

Whether you’re setting this up for the first time or need a refresher, this post has got you covered.

---

## 🔧 Why Use SSH Instead of HTTPS?

While GitHub supports both HTTPS and SSH, using SSH has some key advantages:

- ✅ Secure authentication using cryptographic keys
- ✅ No need to enter your GitHub credentials every push or pull
- ✅ Works seamlessly with automation and scripting

---

## 🛠️ Step-by-Step Guide

### 1. **Check for Existing SSH Keys**

Open your terminal and run:

```bash
ls -al ~/.ssh
```

Look for files like:

- `id_rsa` and `id_rsa.pub`
- or `id_ed25519` and `id_ed25519.pub`

> If you already have a key, you can skip to [Step 3](#3-add-your-ssh-key-to-the-ssh-agent)

---

### 2. **Generate a New SSH Key**

If you don’t have one, generate a new SSH key:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

> `-C` adds a label for your key (your GitHub email).

If you're on an older system that doesn't support `ed25519`, use:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Press `Enter` to accept the default file path, and set a **passphrase** (optional but recommended).

---

### 3. **Add Your SSH Key to the SSH Agent**

Start the agent and add your key:

```bash
# Start the SSH agent
eval "$(ssh-agent -s)"

# Add the key
ssh-add ~/.ssh/id_ed25519
```

> Replace with `id_rsa` if you used RSA.

---

### 4. **Copy Your Public Key**

Run this command to copy the key to your clipboard:

```bash
pbcopy < ~/.ssh/id_ed25519.pub     # macOS
xclip -sel clip < ~/.ssh/id_ed25519.pub  # Linux (with xclip installed)
```

Alternatively, just open and copy it manually:

```bash
cat ~/.ssh/id_ed25519.pub
```

---

### 5. **Add the Key to GitHub**

1. Go to [GitHub SSH Keys](https://github.com/settings/keys)
2. Click **"New SSH key"**
3. Paste the key
4. Give it a meaningful **title**
5. Click **"Add SSH key"**

---

### 6. **Test Your Connection**

Verify that everything works:

```bash
ssh -T git@github.com
```

If successful, you’ll see a message like:

```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

---

### 7. **Configure Git to Use SSH by Default (Optional)**

If your Git remotes use HTTPS, you can switch to SSH:

```bash
git remote set-url origin git@github.com:username/repo.git
```

You can check your current remote with:

```bash
git remote -v
```

---

## 🧠 Tip: Multiple GitHub Accounts?

If you're using multiple GitHub accounts (e.g., personal & work), you can configure SSH config:

```bash
# ~/.ssh/config
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519

# For work account
Host github-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_work_ed25519
```

Then in your Git remote:

```bash
git remote set-url origin git@github-work:username/repo.git
```

---

## ✅ Final Thoughts

SSH keys are a secure and convenient way to manage GitHub authentication. Once set up, they save you time and improve your workflow. This setup works well with Git clients, CI/CD tools, and automation scripts.

For a smoother dev experience, I recommend:

- Backing up your SSH keys securely
- Using a passphrase-protected key
- Exploring `~/.ssh/config` for advanced use

---

*No more typing passwords. Just code, commit, and push!* 🚀

---

**Related posts:**

- [Essential Git Commands Cheatsheet](../cheatsheets/git-commands)
- [Neovim + Git Integration Tips](../dev-setup/neovim-git)
- [Dotfiles for Terminal Productivity](../tools/dotfiles-setup)

---

Happy coding,  
**[anvndev](https://github.com/anvndev)** ☕  
