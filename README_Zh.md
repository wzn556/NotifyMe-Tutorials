# NotifyMe-Tuorials
这是一份如何使用NotifyMe的指南。NotifyMe是一个安卓App，通过此App你可以向你的安卓设备发送通知。
## 功能
* 在安卓设备上接收消息，应用场景包括：  
  * 通知转发；  
  * 物联网设备或服务器的消息推送；  
  * 在电脑上向安卓设备推送文本，可复制，或在浏览器进行搜索。  
* 内置6种通知图标，也可使用用户自定义的通知图标，便于区分不同的通知来源。  
* 可设置大图标，提升通知辨识度。  
* 可自定义通知通道，便于管理通知的优先级、铃声及振动等。  
* 可接收加密消息，提升通知的安全性。  
## 如何使用
### 方法1：通过http请求POST发送JSON格式的消息数据  
网址：```https://asia-east2-notifyme-f7507.cloudfunctions.net/send```  
请求头：```Content-Type:application/json```  
JSON：  
```
{
    "data": {
        "to": "d-NnQPgQTYGF_JhRK6iFiB:APA91bET0S07sI1bOYBQ7FrWMBcQ53SyxnwO-ODXP19mDzku4ZijawFSQFT_LZ5cUqKPjDbd61-UBzzNiiiz_vkkYoK6jnu-zWU2qo1mDKYdy2wnjsZ99g_9j-vZ-5sm2QwNDWYAF_vh",
        "ttl": 60,
        "priority": "normal",
        "data": {
            "title": "NotifyMe！",
            "body": "This is a test message!",
            "iconType": 0,
            "smallIcon":"1322",
            "largeIcon":"345",
            "id":"-11",
            "encryption":false,
            "iv":"",
            "invisible":false,
            "browse":"https://www.baidu.com/s?wd=search_word",
            "channel":"quicker_channel"
        }
    }
}
```
#### JSON数据说明  
```to```：接收消息的设备token。  
```ttl```：如果设备离线，消息应在 FCM 存储中保留多长时间（以秒为单位）。支持的最长时间为```2419200```( 4 周)，如果不设置，则默认值为 4 周。如果要立即发送消息，不在服务器上进行保存，请将其设置为 ```0```。  
```priority```：消息优先级。可以取```normal```和```high```。```normal```：应用在前台运行时，消息会被立即传递。当应用在后台运行时，消息传递可能会延迟。```high```：即使设备处于低电耗模式，FCM 也会立即尝试传递消息。  
```title```：消息标题。  
```body```：消息内容。  
```iconType```：消息小图标。可取值为```0~6```。```0~5```为App内置图标，```6```为用户自定义图标，可在```smallIcon```中进一步设置。  
```smallIcon```：设置用户自定义的小图标，取值为用户创建图标时设定的名称。未设置或值不存在时为默认图标（```iconType```取值为```0```时的图标）。  
          需注意，对于原生系统或类原生系统的设备，使用的图标应为单色图标（背景为透明），否则图标有色部分会为纯白，这Google故意设置的。在部分高度定制化的系统上，彩色图标是可以正常显示，如ColorOS、MIUI等。  
```largeIcon```:设置用户自定义的大图标，取值为用户创建图标时设定的名称。未设置或值不存在时通知无大图标。  
```id```：通知的id，新通知会在状态栏覆盖相同的```id```的旧通知，取值为```[1,+∞)```。也可取值为```0```，表示App自动设置通知```id```，以确保通知不会覆盖。  
```encryption```：是否进行加密。加密方法为```AES/CBC/PKCS5Padding```，加密内容为```title```和```body```。加密时请使用```App/设置```中的```AesKey```，初始化向量```iv```可自行设置，填入```iv```项中即可。  
```iv```：AES加密的初始化向量，长度为```16```字节，用于App解密数据。  
```invisible```：通知是否可见，设置为true时，将不会显示通知的```title```和```body```（仅在app内可见）。  
```browse```：网址，设置此项时，点击通知会在浏览器中打开该网址，也可以以```body```的值进行搜索。不设置或设置值为非网址时，点击通知会打开App。  
要以body的值进行搜索，请将搜索引擎的搜索关键词设置为```search_word```。例如：```https://www.baidu.com/s?wd=search_word```  
```channel```：通知通道，取值为用户自定义的通道名称。未设置或取值不存在时，将使用默认通道。  
### 方法2：使用Quicker发送通知  
Quicker下载地址：https://getquicker.net/  
Quicker动作地址：https://getquicker.net/Sharedaction?code=a709b6bc-ca19-4a07-89ca-08dc547a3ff5  
