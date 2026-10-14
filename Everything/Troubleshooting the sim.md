# Troubleshooting the sim

What to check when the simulator won't build, launch, or respond. Back to [[Launching and configuration of the simulator]].

## Outline
- [ ] **How to read the build output** (find the *first* red error, that's usually the real one)
- [ ] **It won't build**
  - [ ] Red Java errors / code doesn't compile
  - [ ] Wrong branch or not up to date (`git pull`, see [[Installing Git]])
  - [ ] Wrong Java version (Spotless errors, `java -version`, point Gradle at the WPILib JDK)
  - [ ] `permission denied: ./gradlew` (Mac)
- [ ] **It builds but the window never appears**
  - [ ] Opened on another desktop/Space
  - [ ] Another sim is already running (port in use)
- [ ] **The window opens but the robot won't move**
  - [ ] Robot State is on Disconnected
  - [ ] Keyboard/controller not bound to Joystick 0
  - [ ] Sim window not focused
- [ ] **Errors that are safe to ignore** (PhotonVision/camera spam, controller-not-found warnings)
- [ ] **Resetting the Sim GUI config** (delete the `simgui*.json` files and start fresh)
- [ ] When to ask a lead

> [!todo] Still to write
> Fill in each item with the real fix. Verify every item against the repo as you go; this list is from problems I ran into earlier and hasn't been checked.

---
← Previous: [[Using elastic and selecting an autonomous routine]] | Up: [[Simulator]]
