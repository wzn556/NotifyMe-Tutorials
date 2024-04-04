# NotifyMe-Tuorials
This tuotials is for NotifyMe, which is a app that can recevied notifications based on FCM on your android devices.
* To receive messages on Android devices, the application scenarios include:  
  * Notification forwarding;  
  * Message push for iot devices or servers;  
  * Push text from your computer to your Android device for easy copying, or search in your browser.  
* 6 built-in notification ICONS, and user-defined notification ICONS can also be used to distinguish between different notification sources.  
* Large ICONS can be set to improve the recognition of notifications.  
* You can customize the notification channel to manage the priority, ringtone, and vibration of notifications.  
* Can receive encrypted messages to improve the security of notifications.  
## How to Use
### Method 1: Send message in JSON format through http request POST  
URL：```https://asia-east2-notifyme-f7507.cloudfunctions.net/send```  
Headers：```Content-Type:application/json```  
JSON：  
```JSON
{
    "data": {
        "to": "d-NnQPgQTYGF_JhRK6iFiB:APA91bET0S07sI1bOYBQ7FrWMBcQ53SyxnwO-ODXP19mDzku4ZijawFSQFT_LZ5cUqKPjDbd61-UBzzNiiiz_vkkYoK6jnu-zWU2qo1mDKYdy2wnjsZ99g_9j-vZ-5sm2QwNDWYAF_vh",
        "ttl": 60,
        "priority": "normal",
        "data": {
            "title": "NotifyMe！",
            "body": "This is a test message!",
            "iconType": 0,
            "smallIcon":"smallIcon_0",
            "largeIcon":"largeIcon_0",
            "id":"0",
            "encryption":false,
            "iv":"UkAjUPykxX1Eu4h7",
            "invisible":false,
            "browse":"https://www.baidu.com/s?wd=search_word",
            "channel":"quicker_channel"
        }
    }
}
```
#### JSON Interpretation  
```to```: The value is the token of device which used to receive the message.  
```ttl```: How long (in seconds) the message should be kept in FCM storage if the device is offline. The maximum time to live supported is ```2419200```( 4 weeks), and the default value is 4 weeks if not set. Set it to ```0``` if want to send the message immediately without keep.  
```priority```: Notifications priority. Can take ```normal``` and ```high```. ```normal```: Messages are delivered immediately when the app is in the foreground. For backgrounded apps, delivery may be delayed. ```high```: FCM attempts to deliver high priority messages immediately even if the device is in Doze mode.   
```title```: The notification's title.  
```body```: The notification's body.  
```iconType```: The notification's small icon. Can take ```0~6```. ```0~5``` for build-in icons，```6``` for user-defined icons, which can be further set in ```smallIcon```.  
```smallIcon```: The user-defined notification's small icon, The value is the name set when the icon is created. The icon is default (Take ```0``` for ```iconType```) if not set or value does not exist.   
It should be noted that for Pixel or devices with AOSP, the icon used should be a monochrome icon (the background is transparent), otherwise the colored part of the icon will be pure white, which is deliberately set by Google. On some highly customized systems, color ICONS can be displayed normally, such as ColorOS, MIUI, etc.  
```largeIcon```: The notification's small icon, The value is the name set when the icon is created. The icon won't exist in notification if not set or value does not exist.  
```id```: The notification's id, The new notification will overwrite the old notification with the same ```id``` in the status bar, Can take ```[1,+∞)``` . The value can also be ```0```, which means that the App automatically sets the notification id to ensure that the notification will not be overwrote.  
```encryption```: Encrypt or not. The encryption method is ```AES/CBC/PKCS5Padding``` , The encrypted content is ```title``` and ```body``` . Please use ```AesKey``` in ```App/set``` to encrypt, initialization vector ```iv``` should fill in the ```iv``` item which can be created by yourself.  
```iv```: Initialization vector for AES encrypt，It is ```16``` bytes long and is used for the App to decrypt data.  
```invisible```: Whether notifications are visible, when set to true, notifications' ```title``` and ```body``` will not be displayed (Visible only within the app).  
```browse```: URL. When it was set, clicking on the notification will open the URL in browser. You can also search the ```body```. When you do not set or set the value to non-URL, clicking the notification will open the App。  
To search with the ```body```, set the keyword for the search engine to ```search_word```. For example: ```https://www.baidu.com/s?wd=search_word```.  
```channel```: The notification's small icon, The value is the name of channel which is set by user. The channel is default if not set or value does not exist.  
### Method 2: Send message with Quicker  
Download Quicker: https://getquicker.net/  
Action for Quicker: https://getquicker.net/Sharedaction?code=a709b6bc-ca19-4a07-89ca-08dc547a3ff5  
