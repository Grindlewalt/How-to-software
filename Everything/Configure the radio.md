Configuring the radio is quite simple. I will most likely make a video and link the documentation so that it is always up to date, but for now I will go over our team-specific docs.

**Documentation:** https://frc-radio.vivid-hosting.net/overview/programming-your-radio-at-home
**The video:** I haven't made the video yet

## Plugging the radio in
- This can vary quite a bit from robot to robot depending on how we power the radio that year. In general we use direct 12V to the radio, then the Rio (or whatever the new onboard processor is from now on — Pi 5 compute module pls?) goes to the port labeled "Rio", and then AUX 1 and 2 are used for anything else like PhotonVision, QuestNav, etc.
- The port labeled "DS" (Driver Station) is where you plug in the laptop that you are using to configure/connect the radio.
- Most of the time we will power the access point radio (the one that plugs into your computer) over PoE (Power over Ethernet), and it will plug into the "Rio" port. You will know it powered on when the LEDs on the top turn on.
- To summarize: the computer plugs into "DS", the Rio plugs into "Rio", and power plugs into either the 12V direct or over PoE (which also plugs into the "Rio").

## Initial connection
- First connect the radio via Ethernet. This step applies for both the robot radio and the access point radio.
- After that, open your web browser and navigate to http://192.168.69.1, http://radio.local or http://10.49.11.1 if the radio has already been configured.
- It should take you to a config screen that looks like this:

![[Pasted image 20260611115836.png|316]]

Once you get to that screen, you can now configure the radio.

## For the radio that plugs into the robot (Robot Radio)
- At the top, set it to access point mode
- You can leave both 2.4GHz and the QoS BW Limit
- You don't have to enable the SystemCore mode (unless we specifically need it)
- Set team number to 4911
- SSID suffix can be whatever the name of the robot is (ex: Rossi for the 2026 robot)
- WPA key for the 6GHz connection can be something like ROSSI4911 (name in caps, followed by number)
- WPA key for 2.4GHz can be the same as the 6GHz one
- Once that has been typed in, click the big "Configure" button

## For the radio that plugs into the laptop (Access Point)
The process will be quite similar.

> [!todo] Get the actual GUI of the AP config
> The steps below are for the robot radio config, not the AP config, but they should be similar.

- At the top, set it to access point mode
- You can leave both 2.4GHz and the QoS BW Limit
- You don't have to enable the SystemCore mode (unless we specifically need it)
- Set team number to 4911
- SSID suffix can be whatever the name of the robot is (ex: Rossi for the 2026 robot)
- WPA key for the 6GHz connection can be something like ROSSI4911 (name in caps, followed by number)
- WPA key for 2.4GHz can be the same as the 6GHz one
- Once that has been typed in, click the big "Configure" button

## Troubleshooting
There is a *lot* to cover for troubleshooting, but the LED indicators can be very helpful. The full LED debug docs can be found here: https://frc-radio.vivid-hosting.net/overview/led-status-indications

Turning it on and off again can be surprisingly helpful. So can reconfiguring both radios, making sure everything matches up and that both radios are turned on. After competitions, you will have to reconfigure the robot radio.

---
Up: [[Robot Radio]]
