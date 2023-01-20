# AutoDoor_TelegramBot
Using an ESP8266 relay board and Telegram bot, you can now get notification when someone ring at your door and open it from anywhere. You also can set and AutoOpen function for the door to automatically open after someone dial at the intercom.

### INPUT PIN
PIN IntercomInput is GPIO14 which is triggered whenever someone dial at the intercom

### OUTPUT
PIN KeyOutput GPIO5 will be triggered to activate the relay after Telegram command received. 

### LOOP FUNCTION
The loop function is the main loop of the program, which is executed repeatedly after setup. It uses the millis() function to keep track of the time since the last time the loop ran. It will only execute the code inside the if statement when the time elapsed since the last time it ran is greater than or equal to a specified interval time.

The code inside the if statement checks for new messages from the Telegram bot and calls the handleNewMessages function to handle them. It also checks if the intercom is activated, and if it is, it sends a message to the Telegram chat asking the user to open the door. If the AutoActivation variable is set to true, it will automatically activate the keys without waiting for user input.

### PROGRAM SETUP
First initializes the serial communication and sets the baud rate to 115200. Then it uses the WiFiManager library to connect to a WiFi network. The network's name is "MaxDoorBot" and the password is "123456789".

After connecting to WiFi, the code uses the configTime function to set the time using the NTP (Network Time Protocol) and set the time zone, then it sets the trust anchor for the Telegram API.

The code then sets the IntercomInput and KeyOutput pins as inputs and outputs, respectively. It also sets the initial state of the KeyOutput pin to LOW.

The code then enters a loop that repeatedly checks the status of the WiFi connection, and waits until it is connected. Once the ESP32 is connected to the WiFi, the code sets the IntercomInput pin as an interrupt, assigns the changeDoorStatus function as the interrupt handler, and sets the interrupt mode to RISING.

The code also sends a message to the Telegram chat to notify that the DoorDfrescoBot has started up, and then sets the commands that are available to the Telegram bot to open, cancel, auto and stop.

It is important to note that for this code to work, you will need to define the client, cert, bot, IntercomInput, KeyOutput, CHAT_ID and WiFiManager variables before the setup() function.

### INTERRUPT WHEN INTERCOM RING
The changeDoorStatus function is called whenever the state of the IntercomInput changes. It sets the IntercomActivated variable to true.

### HANDLE NEW MESSAGE FROM TELEGRAM
The handleNewMessages function handles the new messages received from the Telegram bot. It loops through all the new messages, and checks the text of each message. If the message text is "/open", it calls the ActivateKeys function, which presumably activates the door lock. If the message text is "/cancel", it cancels the pending

