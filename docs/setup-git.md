# Setup `git`

1. Install `git` in your system.

```bash
apt-get install git
```

2. Define default branch when initing a new project.

```bash
git config --global init.defaultBranch main
```

3. Store `git` credentails permanently.

> See https://stackoverflow.com/a/12240995

```bash
git config credential.helper store
```

4. Define who you are.

```bash
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

## Credentials on GitHub

1. Click on "Settings".
2. Click on "Developer settings".
3. Click on "Personal access tokens".
4. Generate a token and use it as password when authenticating in `git`.
