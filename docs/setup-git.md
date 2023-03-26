# Setup `git`

1. Install `git` in your system.

```bash
apt-get install git
```

2. Define default branch when initing a new project.

```bash
git config --global init.defaultBranch main
```

3. Define who you are.

```bash
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

## Credentials on GitHub

1. Click on your profile pic menu.
2. Click on "Settings".
3. Click on "Developer settings".
4. Click on "Personal access tokens".
5. Generate a token and use it as password when authenticating in `git`.
