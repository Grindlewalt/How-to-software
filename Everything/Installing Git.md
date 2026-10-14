# Installing Git

How to install Git and clone the robot repo. Needed before your IDE can open the project, see [[Setting up your IDE]].

## What you should be able to do
- [ ] Install Git on Mac
- [ ] Install Git on Windows
- [ ] Check it works
- [ ] Clone the robot repo
- [ ] Pull the latest changes and switch branches

## Mac
Easiest option, in Terminal:
```
xcode-select --install
```
(Installs Apple's command line tools, which include Git. Running `git` for the first time on a Mac without them also prompts you to install. If you already have Homebrew, `brew install git` also works.)

Other install options (Homebrew, MacPorts, Xcode tools; there is no standalone installer anymore): https://git-scm.com/install/mac

## Windows
Download and run the installer: https://git-scm.com/install/windows. The default options are fine.

## Check it works
```
git --version
```

## Cloning the robot repo
```
git clone https://github.com/frc4911/2026-Rebuilt.git
```
Repo used in these docs: https://github.com/frc4911/2026-Rebuilt (public, so cloning doesn't need a login)

## Everyday commands
```
git pull
git checkout <branch name>
git status
```

> [!todo] Still to write
> GitHub login/access for pushing (ask a lead to add you), where cloned repos should live, committing and pushing, branches.

---
Up: [[Setting up your IDE]]
