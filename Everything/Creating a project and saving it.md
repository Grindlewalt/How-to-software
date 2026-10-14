So, you've (hopefully) opened Choreo now and are at a screen that looks something like this (it will of course vary from game field to game field):
![[Pasted image 20260612235150.png]]

## How to do it
1. **Open the file menu** — To set it up so that all of your autos save to our code, click the folder icon in the top left.
    ![[Pasted image 20260613000314.png]]
2. **Navigate to the deploy folder** — It should open your file explorer. Navigate to where the robot code is saved and go to `./src/main/deploy/choreo`. There, you will see any .traj files (already built paths) that have been made.

You now have the project configured to save in the correct location! Now when you create, delete or modify paths, since they are saved there, the changes will be made. (You still have to rebuild the program every time for the actual changes to take effect — unless you're Elliot and you edit decompiled code on the fly and then recompile it while the program is still running.)

---
← Previous: [[Installing Choreo]] | Next: [[Configuring the robot physics]] | Up: [[Choreo]]
