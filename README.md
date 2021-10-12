# 🕹 PhantomHand
  
[日本語](https://zenn.dev/noov/articles/d7d9f448941ec6)  
  
Control and automate Nintendo Switch from a browser. A tool developed with React and Arduino.  

## 🚀 Introduction
**PhantomHand** is a tool that allows you to control and automate your Nintendo Switch from your browser.
If you just want to know how to use it quickly, please see the **[Getting Started Guide](/GettingStartedGuide.md)**.

#### Repositories
- [PhantomHand-React](https://github.com/noov-smash/PhantomHand-React)
- [PhantomHand-Arduino](https://github.com/noov-smash/PhantomHand-Arduino)

    
#### DEMO
<https://phantom-hand.web.app/>

 <font color="Red">⚠️ The content of this repository does not contain any illegal activities such as uploading modified firmware, but it may fall under the Nintendo Switch Terms of Service. Please use at your own risk.</font>


## 💡 Overview
Briefly, this is a web application for the NintendoSwitch macro controller.
  
<img width="840" alt="spec" src="https://user-images.githubusercontent.com/83855713/136757401-a9f6d115-8f24-4d7f-aa9d-1b90bfdacdbb.gif">
  
Specifically, it will have the following functionality: with React and Arduino.  
- Operate the Switch in the browser GUI
- Save a series of operations as a command (macro function)
- Recall and reproduce saved commands (macro replay function)
- Share the command with your followers via Twitter
  
The differences from the macro tools created by the great pioneers are as follows.  
- Works with Google Chrome on Windows / Mac / Linux
- Macro commands can be created while watching the Switch screen
- Can be connected via Bluetooth
- Can be used for Smash Bros (most important!)
  
## ⚙️  Function Description
  
### Create Macro
<img width="840" alt="create" src="https://user-images.githubusercontent.com/83855713/136768549-5ab07e19-dd22-4ef6-9056-392a62ecc695.gif">
  
You can save commands entered in the browser GUI as macros.  
If you connect a pro-controller to your PC, you can also create macros by operating the pro-controller.  
  
### Play macro
<img width="840" alt="play" src="https://user-images.githubusercontent.com/83855713/136768796-ec36282c-b0d8-472d-a3e6-290486553a52.gif">
  
Recall saved macros with the browser GUI.
Unlimited number of macros can be saved, and the macro command to be called can be changed with a single click.
Repeating playback is also supported.
  
## 📦 Devices required
- Arduino Leonard (Atmega32u4)
- BLE Serial Device (CC2840R2F) or USB Serial Device (FT232)
- Jumper wire
  
Please see the **[Getting Started Guide](/GettingStartedGuide.md)** for installation instructions.  
  
## 🛠  Specifications
<img width="840" alt="spec" src="https://user-images.githubusercontent.com/83855713/136764272-de212543-ca13-430f-b33f-2b652e42f7a1.png">
  
### Arduino
**The Arduino Leonardo** microcontroller will allow you to control the Switch remotely.The Arduino Leonardo contains the ATmega 32U4 chip.  
The Arduino Leonardo is powered by the ATmega 32U4 chip, which has the unique feature of working as a USB device.  
This means that the Arduino Leonardo can be configured to behave as a controller when connected to the Switch.  
  
#### NintendoSwitchControlLibrary
The logic for acting as a controller has been made into a library by a great pioneer under the MIT license.  
  
<https://github.com/lefmarna/NintendoSwitchControlLibrary>
  
**PhantomHand** uses the NintendoSwitchControlLibrary to control the Switch from a web browser.   
  
### React
The GUI was developed in React with the possibility of making it a native application with Electron or ReactNative in the future.  
  
#### WebUSB / WebBluetooth
Serial communication was adopted to link the browser and Arduino Leonardo. controller operation signals are sent to the serial communication module connected to the Arduino via wireless (WebBluetooth) or wired (WebUsb).  
  
##### Uint8Array and JSON
The controller operation signals are sent to the Arduino as an 8-bit binary data array. The length of the array is 2, and its contents are the identifiers of the controller's buttons and sticks (0 - 21) and the state of the buttons and sticks (0 or 1, 0 - 255).  
  
<img width="840" alt="spec" src="https://user-images.githubusercontent.com/83855713/136764816-69109eae-ad6c-4323-a778-3f6e210e5254.png">
  
In order to realize the macro function, in addition to the binary sent to the Arduino, the time data of "how many seconds after the start will that command fire" is added and saved as JSON.

```ts
type command = {
  t: number, // Time
  s: Uint8Array[] // Signal => [buttonNumber, buttonState]
}[]
```

#### GamePad API
The browser GUI is not suitable for creating commands for games with complex operations such as Smash Bros.Therefore, a function to acquire the status of the pro-controller was added using the JavaScript GamePad API.  
  
When you connect the pro-controller to your PC via Bluetooth or USB, you can play the game as if it were directly connected to the Switch while still going through JavaScript and Arduino.  
  
<https://developer.mozilla.org/ja/docs/Web/API/Gamepad_API/Using_the_Gamepad_API>
<https://www.npmjs.com/package/react-gamepad>


#### Share command function
  
![share](https://user-images.githubusercontent.com/83855713/136824402-8b938aed-c7c8-49d0-9475-19879e537ec9.gif)
  
Use Rison to embed JSON in the query parameter of a URL. When that URL is shared, anyone who accesses it can emulate that command on Switch by simply pressing the play button. It will be interesting to see if this catches on.  
  
To avoid reaching Twitter's character limit with overly long URLs, a URL shortening service called Bitly was used.  (It's a free service, so you may reach the limit soon.  
  
<https://app.bitly.com/Bl9miVlf2zr/bitlinks/3AUZ7PB>
<https://www.npmjs.com/package/rison>

## 🎮  DEMO
Here's the React project deployed on Firebase.  
You can experience the demo by connecting to an Arduino with a program written on it.  
For more information on how to build an Arduino, please refer to the [Getting Started Guide](/GettingStartedGuide.md).  
  
<https://phantom-hand.web.app/>

## 🛌 Conclusion
I've been testing it myself for about a week, and I've made surprisingly good progress in practicing Smash Bros. I'm sure that Pokémon and RPG enthusiasts will be happy with it. If there seems to be a reasonable demand for it, I'm interested in commercializing it.  
  
However, I have almost no knowledge of hardware mass production, so it will take time.  
If you are a game peripheral manufacturer interested in mass production, please send [me](https://twitter.com/intent/user?user_id=1295277787293446145) a direct message.  
  
## 📚 Appendix
Here is a list of articles and other Switch automation ideas that I found useful. If you're interested in Switch automation after reading this article, I hope you'll explore the various ways to automate your Switch!

### Joycontrol
This method uses a Python library called Joycontrol, which sends the controller signal via Bluetooth, so there is no need to attach a device to the Switch. It's revolutionary.  
<https://github.com/mart1nro/joycontrol>

### ESP-32
ESP-32 is a microcontroller module with built-in WiFi and Bluetooth.  
<https://github.com/mizuyoukanao/UARTSwitchCon>

### Local Network, WebSocket, OSC, etc.
<img width="840" alt="esp8226" src="https://user-images.githubusercontent.com/83855713/136765979-b8932571-d4b6-4da0-91a1-9afd915ed501.png">
  
There are several Arduino microcontrollers (Atmega32u4) with the ESP8266 WiFi module, which can be used to turn itself into a server, or connected to WiFi to turn it into an IoT device.  
  
<https://ja.aliexpress.com/i/32839674193.html>

If you connect this to the Switch, you can control it from outside the house. .... It seems like it could be used for a lot of interesting things. I think this idea has the most potential for development.  
  