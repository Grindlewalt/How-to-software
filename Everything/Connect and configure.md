*Part of [[PhotonVision]]*

---

How to flash the co-processor, connect the cameras, and configure them in PhotonVision.

## Flashing the co-processor
There is only one prerequisite, so it doesn't get its own page: install **balenaEtcher** from https://etcher.balena.io/#download-etcher. It's the tool that writes the PhotonVision image onto the microSD card.

1. **Find out which co-processor you have.** Most of the time it will be an Orange Pi, and there is almost always a label on it somewhere saying the model. In this guide I'm using an Orange Pi 5 Plus (8 GB). The amount of memory doesn't matter, but I'm specifying it anyway.
2. **Download the image.** Go to https://github.com/PhotonVision/photonvision/releases/latest and find the image for your co-processor. For the Orange Pi 5 Plus it's `photonvision-{version}-linuxarm64_orangepi5plus.img.xz`.
   This list is huge and confusing, so read the names carefully. If you flash the wrong image (for example, the Orange Pi 5 Pro image onto an Orange Pi 5 Plus), PhotonVision will not work.

> [!danger] Unplug every other drive first
> balenaEtcher **erases everything** on the drive you flash. Before going any further, unplug every other SD card, thumb drive and external drive so the only one connected is the microSD card you're flashing. That way you can't wipe the wrong one by accident.

3. Plug the microSD card into your computer and open balenaEtcher. You will be greeted by this window:

   ![[Pasted image 20261007221043.png|422]]

4. Click **Flash from file**, then find the image you just downloaded. Mine is at `~/Downloads/photonvision-v2026.3.4-linuxarm64_orangepi5plus.img.xz`. You don't need to unzip the `.xz` file first, balenaEtcher handles that.
5. Click **Select target** and pick the microSD card. **Again: this wipes everything on whatever drive you pick**, so make sure it's the right one.
6. Once you've selected it, the **Flash!** button turns blue and should look like this:

   ![[Pasted image 20261007221921.png|433]]

7. Double check that it's the correct microSD card one more time, then click **Flash!**

   ![[Pasted image 20261007222130.png|441]]

8. This takes a few minutes. When it's done you will get a success screen:

   ![[Pasted image 20261007222449.png|448]]

## Booting up the co-processor for the first time
Now that the microSD card is flashed, it's time to see if everything worked.

1. Put the microSD card into the co-processor.
2. Plug in power. The Orange Pi 5 Plus has 2 USB-C ports, but only one of them can power it: the USB-C port on the same edge as the 2 USB 2.0 ports, 3 HDMI ports and 2 Ethernet ports.
3. Depending on the state of the robot, there may already be a power supply for the co-processor. If not, an extension cord and a USB-C charger will work, as long as the charger is strong enough (the Orange Pi 5 Plus wants 5V at 4A). **Don't drive the robot around like this:** loose wires and co-processors get caught and shredded in swerve modules.
4. Run an Ethernet cable from the co-processor to an AUX port on the radio (see [[Configure the radio]] if you have questions about the radio ports).
5. Plug in at least one camera. This will almost certainly be over USB, so plug it into a USB 3.0 port (the blue ones).
6. Power on the robot and check that:
   - the radio has power,
   - the co-processor has power,
   - the Ethernet cable between the radio and the co-processor is plugged in properly,
   - and your laptop is connected to the radio.

A good way to tell if the co-processor is talking to the network is to look at the yellow and green lights on its Ethernet port. If they're blinking, data is flowing in and out.

## Connecting to the web dashboard
PhotonVision is set up through a web page that the co-processor hosts. Its **left menu** has a few pages (**Dashboard**, **Settings**, **Camera**, **Camera Matching** and **Documentation**), and that's what "page" means for the rest of this lesson.

1. On the same laptop that's connected to the radio, go to http://photonvision.local:5800. You should see a screen like this:

   ![[PV dashboard first boot.png|600]]

2. Click the **camera matching tab** link in the pop-up. If it isn't there, click **Camera Matching** in the left menu (or go straight to http://photonvision.local:5800/#/cameraConfigs, but this link may break in future versions).

   > [!tip] If the left menu is just icons
   > The menu has been collapsed. In the bottom left there are 4 icons:
   > - **Arrow:** expands or collapses the menu. Click this one to get the full menu back.
   > - **Moon/sun:** switches between the light and dark theme.
   > - **Robot head** (red with an X through it right now): whether PhotonVision is connected to NetworkTables on the roboRIO. It's red because we haven't set that up yet, we'll fix it in [[#Networking]].
   > - **Green server:** "Backend connected", meaning this web page is talking to PhotonVision on the co-processor.

3. The **Camera Matching** page shows every camera that's plugged in right now, along with how it's connected (USB), its brand and model (Arducam OV9281), and its status (**Unassigned** means we haven't activated or configured it yet). Click **Activate**.

   ![[PV camera matching activate.png|600]]

4. Next, click **Camera** in the left menu, right above Camera Matching (or go to http://photonvision.local:5800/#/cameras, but again this link may break).
5. You should now see the **Camera Settings** panel with the camera feed next to it. If the model drop down (**Arducam Model** for our cameras) is set to **None**, change it to match the camera's name. Here my camera is `Arducam_OV9281_USB_Camera`, so I picked **OV9281**. Click **Save Changes**.
   If you have multiple cameras, pick the next one from the **Camera** drop down and repeat this step.

   ![[PV camera settings model.png|600]]

6. Go back to **Dashboard**, the top option in the left menu. The panel under the camera feed has options like **Auto Exposure**, **Brightness** and **Camera Gain**. Turn on **Auto Exposure** and adjust **Brightness** to get as much contrast between the light and dark spots as possible.
7. Further down that panel are a few drop downs: **Orientation**, **Resolution** and **Stream Resolution**. Set **Resolution** as high as it will go without lowering the FPS (if it has any impact). I'm using 1280x800 at 120 FPS. **Stream Resolution** only changes the preview you see in the browser, not what PhotonVision processes.
8. In the panel to the right of the camera feed are **Camera**, **Pipeline** and **Type**. Click the pencil icon next to **Camera** and rename the camera based on where it is on the robot. I usually use FL, FR, BL and BR (front left, front right, back left and back right). Click the save icon when you're done.

   ![[PV dashboard exposure resolution name.png|600]]

## Networking
PhotonVision publishes everything over NetworkTables, so it needs to know the address of the NetworkTables server (the roboRIO) to connect to it.

1. Click **Settings** in the left menu. This page has the device info, metrics, global settings and various object detection add-ons. We only care about 2 settings, both in the **Global Settings** panel.
2. At the top of **Global Settings** is **Networking**, and right under that is **Team Number/NetworkTables Server Address**. Type in `10.49.11.2`, our roboRIO's address (4911 can also work, I just have had it not connect with only 4911, but it works fine with 10.49.11.2).
3. A few options down is **Hostname**. Changing it changes the web address: if I change the hostname to `GrantsRobot`, http://photonvision.local:5800 stops working and only http://GrantsRobot.local:5800 works. You need to do this if you have more than one co-processor so the names don't overlap, and it makes them easier to manage.
4. Click **Save** at the bottom.

   ![[PV settings networking.png|600]]

With the robot on, the robot head icon in the bottom left should turn green and say **NetworkTables Server Connected!** If it doesn't, double check the address you typed in.

## Next step
Before the cameras can give accurate results, each one has to be calibrated: [[Calibrate cameras]].

---
← Previous: [[What is PhotonVision]] | Next: [[Calibrate cameras]] | Up: [[PhotonVision]]
