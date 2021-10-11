# 🦾   Getting Started Guide
[日本語](https://zenn.dev/noov/articles/8afaf41678dfa7)
  
## 💻 System Requirements
- Google Chrome (Windows / macOS / Linux)
	- Smartphones and tablets are not supported (Android may work, but we have not tested it)
- Nintendo Switch (v13.0)

## 📦 Required devices
The following devices are required.

- Microcontroller with Atmega32u4
- Serial communication module (FT232 or CC2640R2F)
- Jumper wire (male-to-female)

## 💿 Writing a program to a microcontroller
Since no program has been written to the microcontroller in the industrial shipment state, you need to write a program using [Arduino IDE](https://www.arduino.cc/en/software).

First, install the [Arduino IDE](https://www.arduino.cc/en/software) from the official website.  
  
<https://www.arduino.cc/en/software>

### Install Arduino IDE

<img width="840" alt="selectOS" src="https://user-images.githubusercontent.com/83855713/136785006-201b767d-839e-42eb-9bb6-a2b8585f3da0.png">


Download the version that matches your OS.  

<img width="840" alt="download" src="https://user-images.githubusercontent.com/83855713/136785216-c86b6bfa-e578-4627-a0e5-0fc4adaff8b9.png">


For macOS, move it to the Applications folder.
  
<img width="840" alt="app" src="https://user-images.githubusercontent.com/83855713/136785552-27b190c5-0135-4574-a3c0-e9c6f9b3b3dd.png">
  

When you launch the application, you will see a screen like this.
  
<img width="840" alt="launch" src="https://user-images.githubusercontent.com/83855713/136786916-af9f1bf8-3c1a-423d-a8cb-b4c9a1c6da58.png">
  
### Download the program
Next, download the program to write to the Arduino Leonardo.  
Go to [Repository](https://github.com/noov-smash/PhantomHand-Arduino) and click on **Download Zip**.  
  
<img width="840" alt="code" src="https://user-images.githubusercontent.com/83855713/136786307-6c5aed14-8b9a-4964-bed0-21c5830d6ce4.png">
  

Open the configuration window of Arduino IDE.
  
<img width="840" alt="performance" src="https://user-images.githubusercontent.com/83855713/136787195-995daaa2-b428-4366-a9f1-c04341eaed36.png">
  

In this screen, you can see the location of your Arduino sketchbooks.
  
<img width="840" alt="path" src="https://user-images.githubusercontent.com/83855713/136789110-2ac0f533-28c7-41d1-962a-332f89ef7035.png">
  

Navigate to there in Finder or Explorer. In most cases, the path will be as follows.  
  
**macOS**: `/Users/Documents/{YourUserName}/Arduino`.  
**Windows**: `C:\Users\{YourUserName}\Documents\Arduino\`
  
<img width="840" alt="arduinofolder" src="https://user-images.githubusercontent.com/83855713/136807803-9e56d7d5-5bd9-42d3-b4bc-a932c3ddf15e.png">
  
Unzip the zip file you just downloaded and move it into the Arduino folder marked as **Sketchbook Location**.  
If you already have a Libraries folder, just move the contents into it.  
  
<img width="840" alt="move" src="https://user-images.githubusercontent.com/83855713/136807972-49eff8b5-faa9-4091-818b-6e60dbd339be.png">
  

When you are done here, close Arduino IDE.
  

### Write configuration
  
You are now ready to write the program to the Arduino. The next step is to configure the board settings for the Arduino.  
  
If you use the Arduino's ID as is, NintendoSwitch will not recognize the Arduino as a controller. If you rewrite the ID assigned to the Arduino to the same ID as **Pokken DX Pro Pad**, NintendoSwitch will recognize the Arduino as a controller.  
  
The procedure for rewriting the ID is as follows.
  
<font color="Yellow">⚠️ Please make sure that Arduino IDE is closed.</font>
  
#### macOS
  
Right-click on **Arduino** in the Applications folder and select **View Package Contents**.
  
<img width="840" alt="arduino" src="https://user-images.githubusercontent.com/83855713/136799964-08f0ff6f-932c-4e23-a6a8-fc96036a1a6e.png">
  
  
Open the file `boards.txt` in the following folder with a text editor.
`/Contents/Java/hardware/arduino/avr/`.
  
<img width="840" alt="boardspath" src="https://user-images.githubusercontent.com/83855713/136800444-34b2c479-00a5-44d2-b186-97559cfec030.png">
  
  
#### Windows
Open the file `boards.txt` in the following folder with a text editor.  
`C:\Users\<YourUserName>\AppData\Local\Arduino15\packages\arduino\hardware\avr\1.8.13`  
  
⚠️`1.8.13` part is the version of Arduino IDE you installed.  
  

#### Edit boards.txt (macOS / Windows)
Rewrite the following **4 values** and save the file.   
Be careful not to change the wrong part.    
  
| Row | Key | Before |  | After |
| ---- | ---- | ---- | ---- | ---- |
| 285 | leonardo.vid.1 | 0x2341 | => | 0x0f0d |
| 286 | leonardo.pid.1 | 0x8036 | => | 0x0092 |
| 311 | leonardo.build.vid | 0x2341 | => | 0x0f0d |
| 312 | leonardo.build.pid | 0x8036 | => | 0x0092 |
 
<img width="840" alt="boards.txt" src="https://user-images.githubusercontent.com/83855713/136802147-6bbcc43b-213d-4340-98bc-8ccc2ff950d0.png">

<font color="Yellow">⚠️ Don't forget to save the file after editing.</font>
  
  
### Write the program
  
Now that everything is ready, let's write a program to the Arduino.  
Connect the Arduino to the PC via USB. If the connection is successful, the LED will light up.  
  
<img width="840" alt="arduino" src="https://user-images.githubusercontent.com/83855713/136805988-19a57087-f53d-40f2-b334-a9fa1c63e5df.JPG">


Go back to the Arduino folder where you just moved the files.  
Open the contents of `FT232` if the serial communication module you got is **FT232 (wired module)**, or `CC2640R2F` if it is **CC2640R2F (wireless module)**.  

<img width="840" alt="folder" src="https://user-images.githubusercontent.com/83855713/136797225-2f8e75c8-399c-4247-a2e1-cd04cc7d7bab.png">
  
<img width="840" alt="file" src="https://user-images.githubusercontent.com/83855713/136797301-6e43172f-56ff-47b3-818b-6df07fa453af.png">
  

Open **Tools** -> **Boards** and select **Arduino Leonardo**.
  
<img width="840" alt="baord" src="https://user-images.githubusercontent.com/83855713/136805170-6e090bd2-5a4c-4fa2-beb1-78549b6761ca.png">
  

Open **Tools** -> **Serial Ports** and select the one that contains the string **usb**.  
In most cases, there will only be one port that contains usb, but if there are multiple ports, select them from the top and try until the following process is successful.  
  
<img width="840" alt="port" src="https://user-images.githubusercontent.com/83855713/136805492-4461fb69-94d3-40a0-b52a-945d1b783190.png">
  
  
Click the check button in the upper left corner to compile the program.  
It is OK when the message "Compilation completed" appears at the bottom of the screen.  
  
<img width="840" alt="compile" src="https://user-images.githubusercontent.com/83855713/136808765-2a58e5dc-2fc8-47c1-82d7-f843261619a7.png">
  

Finally, click on the arrow button to write the sketch.  
If you see "Writing to the board is complete" at the bottom of the screen, you are finally finished.   
Congratulations!  
  
<img width="840" alt="Screenshot 2021-10-11 23 32 54" src="https://user-images.githubusercontent.com/83855713/136808906-17a1c70c-20e5-4a73-8789-b8631dd6b58d.png">

## 🔌 Connecting the device

#### FT232 (wired module)
  
Use a jumper wire to connect the Arduino to the FT232.  
Stick the wire so that the RX and TX pins intersect.
  
| Arduino |  | FT232 |
| ---- | ---- | ---- |
| TX1 | <=> | RX |
| RX1 | <=> | TX |

It's small and hard to see, but the names are written near the pins.  
  
<img width="840" alt="ft232" src="https://user-images.githubusercontent.com/83855713/136813325-2a80c875-d4ad-4ef5-b467-3cdb38d1c658.png">
  
  
You can use any color of jumper wire you like.  
  
<img width="840" alt="rxtx" src="https://user-images.githubusercontent.com/83855713/136813872-b85745c4-7eb4-4e5e-9002-00aa688f365f.JPG">
  
Connect the Arduino to the Switch's dock.  
  
<img width="840" alt="arduino-switch" src="https://user-images.githubusercontent.com/83855713/136814178-dcd856ec-ae88-4e80-9d10-28fac8a64063.JPG">
  

Connect the FT232 to the PC.  
  
<img width="840" alt="ft232-pc" src="https://user-images.githubusercontent.com/83855713/136814245-53968203-b0d6-46ce-8987-228a09df7608.JPG">
  

Finally, make sure the whole thing is connected as shown below.  
  
<img width="840" alt="sketch" src="https://user-images.githubusercontent.com/83855713/136815603-8edf91b1-a2a6-4e05-8d2b-39224cf5f953.png">

#### CC2640R2F (wireless module)
  
| Arduino |  | CC2640R2F |
| ---- | ---- | ---- |
| TX1 | <=> | RX |
| RX1 | <=> | TX |
| 5V | <=> | VCC |
| GND | <=> | GND |

There is no need to connect anything to the PC side.  
  
  
## 🌎 Google Chrome Settings
  
In order for GoogleChrome to communicate with Arduino, you need to enable the settings.  
Type the following into the address bar one by one and set all of them to **Enabled**.  
  
`chrome://flags/#enable-javascript-harmony`  
`chrome://flags/#enable-experimental-web-platform-features`  
  
When using **CC2640R2F (wireless module)**, the following items should also be set to **Enabled**.  
`chrome://flags/#enable-web-bluetooth-new-permissions-backend`  
  
<img width="840" alt="chrome" src="https://user-images.githubusercontent.com/83855713/136818722-32544371-5d3c-48a3-a5bc-4838e72029b3.png">


## 🎉 You are now ready!
  
Here are the instructions for using **PhantomHand**.  
First, please visit the site.  
  
<https://phantom-hand.web.app/>
  

Click on the purple button.  
  
<img width="840" alt="home" src="https://user-images.githubusercontent.com/83855713/136819959-4662c147-6347-465c-84ba-d41ba267de73.png">

Select the game software that you want to control with **PhantomHand**.  
If you don't have one, just choose one.   
(If you have any additional requests for game software, please send [me](https://twitter.com/intent/user?user_id=1295277787293446145) a message.)
  
<img width="840" alt="projects" src="https://user-images.githubusercontent.com/83855713/136819967-03da59b4-0b84-4ee5-957b-10d0b4a94c5b.png">
  
    
When you see the controller screen, click the **USB icon** in the upper left corner and select **Search Device**.  
If you are using the CC2640R2F (wireless module), click the Bluetooth icon.  
  
<img width="840" alt="search" src="https://user-images.githubusercontent.com/83855713/136821220-19540209-364d-4f77-9d1d-83c6389ed5c3.png">
  
  
When the pop-up window appears, select the device and click **Connect**.  
  
<img width="840" alt="connect" src="https://user-images.githubusercontent.com/83855713/136820951-d6bbb358-1112-43ea-9e24-2972a3e6b0ec.png">
  

Once this is done, you should be able to control Switch from your browser.  
Operate the GUI controller and see if Switch screen responds!  
  
<img width="840" alt="demo" src="https://user-images.githubusercontent.com/83855713/136757401-a9f6d115-8f24-4d7f-aa9d-1b90bfdacdbb.gif">

  
If it doesn't work, try pressing the reset button on the Arduino.  
The LED will start blinking and it will reboot in 5~10 seconds.  
  
If it still doesn't work, there is most likely a problem with the connections.  
Check all the connections.  
(It is very common to misconnect the RX and TX pins)  
  

<img width="840" alt="reset" src="https://user-images.githubusercontent.com/83855713/136822068-55f8c283-65be-4b92-a7fc-b1023422d278.JPG">
  
# 📖 How to use
  
If you've made it this far, you probably don't need me to explain, but just in case, here's a brief explanation.
  
<img width="840" alt="gui" src="https://user-images.githubusercontent.com/83855713/136822667-8fb0fa45-dbd2-4536-a66b-92ddbdd88ebc.png">

### Side menu
Allows you to select preset commands. The most frequently used commands in the game are saved in the side menu.  
Currently, only the developer can edit the side menu. If you have a command you would like to save, you can share it on Twitter and it may be noticed by the developers.  
  
### Gamepad
The gamepad displayed in the center of the screen can be operated by clicking and dragging. If the device is connected, the operation will be reflected on the Switch.  
If you have a PC with a pro-controller connected, the buttons on this gamepad will light up when you move it.  
  
<img width="840" alt="create" src="https://user-images.githubusercontent.com/83855713/136768549-5ab07e19-dd22-4ef6-9056-392a62ecc695.gif">
    
### Macro
The control buttons in the upper right corner allow you to **Create**, **Play**, **Repeat**, and **Share** macro commands.  
  
### Share
The ability to save created commands is currently not available to the public, but you can share commands via URL instead.   
When you press the share button, a URL will be issued.  
By accessing the URL, everyone can replay your command with a single click at any time.  
  
<img width="840" alt="share" src="https://user-images.githubusercontent.com/83855713/136824402-8b938aed-c7c8-49d0-9475-19879e537ec9.gif">
  
  
# ✅ Conclusion
If you see any improvements, please send me a pull request!  🥺