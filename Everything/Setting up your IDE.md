# Setting up your IDE

How to install and set up the tools you need to write and run robot code. Almost every other lesson needs this done first. All the steps in these docs are written for IntelliJ, so use that unless you're already comfortable with something else.

## Outline
- [ ] **What you need** (an IDE plus the FRC tooling; they are separate installs)
  - [ ] Install the **WPILib installer** (bundles its own JDK, Gradle support, a separate copy of VS Code, and tools like AdvantageScope, Glass, Elastic, SysId, PathWeaver and more; it is large, ~2-3 GB, and installs into a year-specific folder)
  - [ ] **IntelliJ IDEA Ultimate**, free for students
    - [ ] Apply for GitHub Education (the Student Developer Pack)
    - [ ] Once approved, use it to get the free JetBrains student license and install IntelliJ
  - [ ] Other option: **WPILib VS Code** (the officially supported one, comes with the installer; launch *WPILib VS Code*, not a system VS Code). Fine if you already know it, but these docs use IntelliJ.
  - [ ] Supported systems for 2026: Windows 10/11 64-bit, macOS 13.3 or later (Intel and Arm)
- [ ] Install Git and clone the robot repo → [[Installing Git]]
- [ ] Install steps (Mac)
- [ ] Install steps (Windows)
- [ ] Open the robot repo for the first time
  - [ ] Let Gradle import/sync
  - [ ] Make sure the project is using the WPILib JDK
- [ ] Check it works (build the project)

## Links
- GitHub Education (Student Developer Pack): https://education.github.com/pack
- JetBrains free student license: https://www.jetbrains.com/community/education/#students
- WPILib installation guide: https://docs.wpilib.org/en/stable/docs/zero-to-robot/step-2/wpilib-setup.html
- WPILib releases (installer downloads): https://github.com/wpilibsuite/allwpilib/releases/latest
- IntelliJ IDEA: https://www.jetbrains.com/idea/download/
- Git (needed to clone the repo): [[Installing Git]]

> [!todo] Check
> Fact-checked: WPILib VS Code is the supported IDE per the WPILib docs; IntelliJ isn't documented by WPILib. Latest release when checked: WPILib 2026.2.1. I didn't confirm the exact JDK number the installer ships, so don't state one without checking.

---
Next: [[Installing Git]] | Up: [[How to software on the 4911 Cyberknights]]
