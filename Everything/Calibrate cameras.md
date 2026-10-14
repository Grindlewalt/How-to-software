*Part of [[PhotonVision]]*

---

Every camera lens is a little different, so PhotonVision has to measure yours (focal length, lens distortion, etc.) before it can turn pixels into accurate distances and angles. Calibration is per resolution, so you need to calibrate at the resolution you set on the Dashboard page in [[Connect and configure]].

## How to do it
1. Go to the **Camera** page in the left menu.
2. Below the **Camera Settings** panel you used in [[Connect and configure]] is the **Camera Calibration** panel.
3. Under **Configure New Calibration**, set **Resolution** to the one you picked on the Dashboard page. For me that's 1280x800.

> [!todo] Calibration board measurements, Sorry Andy if you are reading this and I haven't gotten the correct config values, I can help you tho
> Add the actual calibration board settings (Board Type, Tag Family, Pattern Spacing, Marker Size, Board Width and Board Height) and how to get the board in the future.

4. Once all the values are filled in, make sure no AprilTags are in view of the camera, then click the yellow **Start Calibration** button.

   ![[PV calibration settings.png|600]]

5. This puts PhotonVision into calibration mode. Hold the board in front of the camera, and boxes should appear around the small markers on the board (they look like mini AprilTags). Click **Take Snapshot**, which is where the **Start Calibration** button was.
6. You need **at least 12 snapshots**, each from a different angle, height, distance, etc. You can (and should) take more than 12.

   ![[PV calibration take snapshot.png|600]]

7. When you're done, click the **Finish** button. It takes a few moments to process, then shows a dialog saying the calibration was successful.
8. Repeat for each camera.

## Next step
Now that the cameras are set up and calibrated, it's time to tell the robot code about them: [[Add cameras and transforms into code]].

---
← Previous: [[Connect and configure]] | Next: [[Add cameras and transforms into code]] | Up: [[PhotonVision]]
