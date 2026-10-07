# Installing your IDE

How to install and configure the tools you need to write and run robot code.

## Outline
- [ ] **What you need** (an IDE plus the FRC tooling; they are separate installs)
  - [ ] Install the **WPILib installer** (bundles its own JDK, Gradle support, a separate copy of VS Code, and tools like AdvantageScope, Glass, Elastic, SysId, PathWeaver and more; it is large, ~2-3 GB, and installs into a year-specific folder)
  - [ ] Choose your IDE: **WPILib VS Code** (the officially supported one, comes with the installer; launch *WPILib VS Code*, not a system VS Code) or **IntelliJ IDEA** (unofficial, works because the project is Gradle; what the sim page uses)
  - [ ] Supported systems for 2026: Windows 10/11 64-bit, macOS 13.3 or later (Intel and Arm)
- [ ] Install steps (Mac)
- [ ] Install steps (Windows)
- [ ] Open the robot repo for the first time
  - [ ] Let Gradle import/sync
  - [ ] Make sure the project is using the WPILib JDK
- [ ] Check it works (build the project)

## Links
- WPILib installation guide: https://docs.wpilib.org/en/stable/docs/zero-to-robot/step-2/wpilib-setup.html
- WPILib releases (installer downloads): https://github.com/wpilibsuite/allwpilib/releases/latest
- IntelliJ IDEA (Community): https://www.jetbrains.com/idea/download/
- Git (needed to clone the repo): [[Installing Git]]

> [!todo] Check
> Fact-checked: WPILib VS Code is the supported IDE per the WPILib docs; IntelliJ isn't documented by WPILib. Latest release when checked: WPILib 2026.2.1. I didn't confirm the exact JDK number the installer ships, so don't state one without checking. Confirm which IDE the team officially uses.
