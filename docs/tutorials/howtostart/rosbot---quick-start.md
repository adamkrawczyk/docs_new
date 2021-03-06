---
title: ROSbot - quick start
sidebar_label: 2. ROSbot - quick start
id: rosbot---quick-start
---

ROSbot 2.0 and ROSbot 2.0 PRO are autonomous, open source robot platforms running on CORE2-ROS controller. They can be used as learning platforms for Robot Operating System (ROS) as well as a base for a variety of robotic applications like inspection robots, custom service robots etc.

If you don't have one, you can get it [here](https://store.husarion.com/).

## Unboxing

What's in the box:

- carrying case
- ROSbot 2.0 (with optional 3D camera and LiDAR already assembled)
- Wi-Fi 2.4GHz antenna
- 3x 18650 Li-Ion rechargeable batteries
- universal charger with power adapter
- charging cable
- microSD card with the software for ROSbot
- USB to Ethernet adapter

![](/docs/assets/img/howToStart/ROSbot_unboxing.jpg)

## Assembly

Your ROSbot is assembled, but to get it ready to work, you need to provide a power supply and attach the antenna.

To mount batteries:

- turn ROSbot upside down
- unscrew battery cover mounted with two screws
- remove the battery cover
- place batteries accordingly to the symbols, keeping the black strip under the batteries
- place battery cover and mount it with screws

To charge the batteries, follow this [guide](https://files.husarion.com/docs2/Charging%20manual%20for%20ROSbot.pdf).

To attach the antenna, screw it to the antenna connector on the ROSbot rear panel.

## Connect ROSbot to your Wi-Fi network

At first ROSbot need to be connected to your Wi-Fi network.

### Option 1: Using display, mouse and keyboard

ROSbot is basically a computer running Ubuntu, so let's open it like a standard PC computer.

1. Plug in a display with HDMI, mouse and keyboard into USB port in the rear panel of ROSbot.
2. Turn on the robot and wait until it boots.
3. Connect to a Wi-Fi network using Ubuntu GUI.
4. Open Linux terminal and type `ifconfig` to find your IP address. Save it for later.

### Option 2: Using Ethernet adapter

In the ROSbot 2.0 set there is one USB-Ethernet card.

1. Turn on the robot and wait until it boots.
2. Plug in Ethernet adapter (included in set) to USB port in the rear panel.
3. Plug in one end of the Ethernet cable into your computer and other one to the adapter.
4. To connect with ROSbot via ssh, type in your terminal application: `ssh husarion@192.168.0.1` and password `husarion`.
5. Connect to a Wi-Fi network.

- In the terminal, type `nmtui` and press Enter. You should see:

![](/docs/assets/img/howToStart/nmtui_1.png)

- Go to `Active a connection` and tap `Enter`

![](/docs/assets/img/howToStart/nmtui_2.png)

- Chose you Wi-Fi network and tap `Enter` one more time. Enter your password, confirm it and tap `Esc` to get back to main menu.


![](/docs/assets/img/howToStart/nmtui_3.png)

- Use `Quit` to close `nmtui`.

6. Type `ifconfig` to find your IP address. Save it for later.

## Access ROSbot terminal using wireless connection

### Connecting over LAN network

The most convenient way to work with ROSbot on daily basis is to do that over Wi-Fi. Connect your laptop to the same Wi-Fi network as ROSbot and type in the terminal:

`ssh husarion@<ROSBOT_IP>` where <ROSBOT_IP> is the IP address obtained in the previous steps.

**FOR WINDOWS USERS:**

If you are Windows user you might like to connect to your ROSbot by using the Remote Desktop Connection:

Press `WinKey` + `r` then type `mstsc`.

You will see a window appear:

![Windows RDP](/docs/assets/img/aws-tutorials/quick-start/win_rdp.png)

Type in your device IP address and click connect.

You will see the ROSbot desktop, from the top menu, choose the `Applications` -> `Terminal`.

### Connecting over the internet (optional)

Not always your laptop and ROSbot can be in the same LAN network. To overcome that obstacle use VPN. [Husarnet](https://husarnet.com/) is a recommended VPN for ROSbots. It's preinstalled on ROSbot so you need to install that on your laptop.

To connect your laptop and ROSbot over VPN:

- **In the Linux terminal on your laptop** (Ubuntu OS is recommended) to install Husarnet type: `curl https://install.husarnet.com/install.sh | sudo bash` to install Husarnet. If the process is done type `sudo systemctl restart husarnet`
- **In the Linux terminal of your laptop and in the Linux terminal of your ROSbot** to configure network type:
  `sudo husarnet websetup` and open the link that will appear in a web browser. The link should look like that: `https://app.husarnet.com/husarnet/fc94xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx` and add your devices to the same network. You will need to do that step both for ROSbot and for your laptop.

At this point your laptop and ROSbot should be in the same VPN network. To access your ROSbot from a level of your laptop over the internet just type in the terminal:

`ssh husarion@<HOSTNAME_OF_YOUR_ROSBOT>`

To get more information about using Husarnet visit this [tutorial](https://docs.husarnet.com/getting-started/)

## Low level firmware installation

In the heart of each ROSbot there is a CORE2 board equipped with STM32F4 family microcontroller. The board is responsible for real time tasks like controlling motors, calculating PID regulator output or talking to distance sensors. High level computation is handled by SBC (single board computer) - ASUS Tinker Board (in ROSbot 2.0) or UP Board (in ROSbot 2.0 PRO).

### Mbed firmware

This firmware version is based on ARM's Mbed OS system. If you're interested in learning more about using Mbed OS check our tutorial [Using CORE2 with Mbed OS](https://husarion.com/tutorials/mbed-tutorials/using-core2-with-mbed-os/). We recommend you also to look at the [ROSbot's Mbed firmware GitHub page](https://github.com/husarion/rosbot-firmware-new).

All needed information about flashing ROSbot firmware and using stm32loader you can find in [ROSbot manual](https://husarion.com/manuals/rosbot/#i-mbed-firmware). 

#### Required ROS packages - `rosbot_ekf`

In order to use Mbed firmware the `rosbot_ekf` package have to be installed on your ROSbot. The package incorporates a ready to use Extended Kalman Filter that combines both the IMU and encoders measurements to better approximate the ROSbot position and orientation. The package also contains custom messages that are required by the new firmware. The package is already installed on your ROSbot.

## Usage

Programming procedure needs to be done only once, on further uses, you can start from this point:

- Turn on your ROSbot.
- Open a terminal and run ssh using that command: `ssh husarion@x.x.x.x` (instead of "x.x.x.x" type hostname of device if you using Husarnet or your local IP address - your laptop should be in the same Wi-Fi network as you robot in this case)
- In terminal paste following command:

_If you use ROSbot 2.0:_

```bash
roslaunch route_admin_panel demo_rosbot_mbed_fw.launch
```

_If you use ROSbot 2.0 PRO:_

```bash
roslaunch route_admin_panel demo_rosbot_pro_mbed_fw.launch
```

Launch web browser and type IPv6 if you using husarnet:
```
[fc92:a348:c2e8:cbcb:480f:bd93:6a21:f3c7]:8000
```
or the local IP of your ROSbot if both device are in the same network:
```
192.0.2.26:8000
```
*Please note that IP address may vary depending on your network configuration!*

- You should see interface as below, use it to test and control your ROSbot.

Also, you can check how it works in gazebo simulation:
    
```bash
roslaunch route_admin_panel demo_gazebo.launch
```

![panel accessed through husarnet](/docs/assets/img/software/panel_at_husarnet.png)

You can find detailed description of Route Admin Panel in [software section](https://husarion.com/software/route-admin-panel/).

> Note: if you experience any issues, make sure batteries are fully charged ([LED L1 is blinking](https://husarion.com/manuals/rosbot-manual/#rear-panel-description) if battery level is low). Charging manual is [here](https://husarion.com/manuals/rosbot-manual/#charging-rosbot).
