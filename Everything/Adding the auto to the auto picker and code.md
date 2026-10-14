This section will also rely on the fact that you have set up and configured your document and the save location
So, you've created your auto and built it, but you still cant run it! In this section I will show you how you can make it so that your auto appears in your auto picker in network tables.

### How autos work now
We only keep a few Choreo paths (`Fifty`, `Sweep` and `Middle`), all drawn on the **blue** half of the field. The code turns each path into several entries in the auto picker (Red/Blue, Left/Right) by flipping it for red and mirroring it for the other side, so you only draw it once. The picker is a plain WPILib dropdown (`LoggedDashboardChooser`) at `SmartDashboard/Auto Chooser`, which Elastic shows as a ComboBox Chooser and AdvantageKit logs. (Choreo's own `AutoChooser` didn't show up as a dropdown in Elastic, so we don't use it.)

Shooting is driven by **split** waypoints. In Choreo, mark a waypoint as split and the robot will stop there and shoot. If the last waypoint is split it shoots there too; if it isn't, the path just ends.

### In the code
1. First you will need to open the actual robot code. In WPIlib/InteliJ it is just going to the top and clicking file > open folder > navigate to the spot where you have the code > src > open
2. Go to main > java > com > ck4911 > auto > then open ChoreoAutoCommandHandler.java
3. Scroll down to the `addAutos()` method, it should look something like this:
   ```java
private void addAutos() {
  addLeftAndRight("Fifty");
  addLeftAndRight("Sweep");
  addAuto("Red Middle", () -> routineFor(Alliance.Red, "Middle", false).cmd());
  addAuto("Blue Middle", () -> routineFor(Alliance.Blue, "Middle", false).cmd());

  // Test / tuning entries.
  ...
}
   ```
4. To add your own path, put the `.traj` file in `src/main/deploy/choreo` (Choreo does this for you if your project is saved there, see [[Creating a project and saving it]]) and add a line in `addAutos()`. For a path drawn on the blue half that you want in all four versions (Red/Blue, Left/Right):
   ```java
addLeftAndRight("GrantsAuto");
   ```
   Or, for a single alliance with no mirroring:
   ```java
addAuto("Blue GrantsAuto", () -> routineFor(Alliance.Blue, "GrantsAuto", false).cmd());
   ```

That's it, you don't write a method per auto anymore. `buildRoutine()` does the rest for every path.

Let's break down what you just added, this will be for someone who is new to java or coding in general.

```java
addLeftAndRight("GrantsAuto");
```
This looks up the path named `"GrantsAuto"` (it **must** match your Choreo path name exactly, or the auto will fail when you select it), works out which side of the field it was drawn on from where it starts, and adds four entries to the picker: "Red GrantsAuto Right", "Red GrantsAuto Left", "Blue GrantsAuto Right" and "Blue GrantsAuto Left" (the side names are from the driver's perspective). The "other side" entries are the same path mirrored across the middle of the field.

```java
addAuto("Blue GrantsAuto", () -> routineFor(Alliance.Blue, "GrantsAuto", false).cmd());
```
`addAuto` adds one entry to the picker. `"Blue GrantsAuto"` is the label you'll see. The `() -> ...` is a lambda, which hands over a bit of code so the command is only built *if* someone selects that option. `routineFor` builds the routine for that alliance and path, and `false` means don't mirror it. `.cmd()` turns the routine into a command the scheduler can run.

What `buildRoutine()` does with your path, split by split:
1. Resets odometry to the path's start, then follows the first piece of the path.
2. Spins up the flywheel early so it's at speed when the robot gets to the shooting spot.
3. At each split, the robot stops, aims at the hub, waits until heading, flywheel and hood are all on target, then feeds for `Auto/FeedSeconds` (5 s by default). The collector jitters while it feeds.
4. Stows the collector and drives to the next piece, until the last shot is done.

Event markers (see [[Markers]]) handle the collector while driving.

> [!note]
> The picked auto is rebuilt whenever the pick or the alliance changes while the robot is disabled, and a routine only runs once, so a fresh one is built after each run. If the Driver Station alliance doesn't match the auto's color, you'll get a "wrong alliance" warning, and the auto will run on the DS alliance's side.

---
← Previous: [[Building and naming paths]] | Next: [[Waypoints]] | Up: [[Choreo]]
