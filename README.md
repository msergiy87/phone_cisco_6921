#### SEP.cnf.xml for Cisco CP-6921

The main configuration file for the phone. The actual name of the file is based on the MAC address of the phone, eg: SEP58971ECC97C1.cnf.xml (SEP\<MAC\>.cnf.xml).

I used configuration the same as in following sites:

(https://github.com/amooma/GS3/wiki/Cisco-CP-69xx-VoIP-Telefone-mit-Asterisk-Gemeinschaft) 

(https://zadarma.com/ru/support/instructions/cisco/cisco-6921/)

And get parameters explanations from this pages:

(http://docs.acsdata.co.nz/asterisk-cisco/sepmac-cnf-xml.shtml)

(http://www.voip-info.org/wiki/view/Asterisk+phone+cisco+79x1+xml+configuration+files+for+SIP) 

(http://www.voip-info.org/wiki/view/Asterisk+phone+cisco+7970+SIP)

But I need configure some custom settings. For example:

##### 1) I used g729a codec and I need callStats for correct end calls.
```
<preferredCodec>g729a</preferredCodec>
<callStats>true</callStats>
```
 - CallStats refer to if the phone feeds back call quality statistics to the SIP server when the call is terminated.

##### 2) How the phone alerts the user to unread voicemail messages. Set only 'Light' and 'Prompt' signal when you have unread messages. Without stutter.
```
<messageWaitingLampPolicy>3</messageWaitingLampPolicy>
```
 - messageWaitingLampPolicy - 3 - Light Lamp and Display Prompt if message is waiting.

'Light' is the bright red lamp on the headset.

'Prompt' will show up a flashing voicemail envelope next to the Line on the RHS side of the display when there is voicemail.

##### 3) I need set amount of calls that phone can recive simultaneously. Otherwise it set response busy when have more then one calls.
```
<maxNumCalls>4</maxNumCalls>
<busyTrigger>2</busyTrigger>
```
 - maxNumCalls - defines the maximum number of calls allowed per line.
 - busyTrigger - defines the number of calls that triggers Call Forward Busy per line on the SIP phone.

##### 4) Configure 2-nd line with auto answer for conference.
```
<autoAnswerTimer>1</autoAnswerTimer>

<line button="2">
<featureID>9</featureID>

<autoAnswerEnabled>3</autoAnswerEnabled>
<autoAnswerMode>Auto Answer with Speakerphone</autoAnswerMode>
```
 - autoAnswerTimer - seconds to wait before automatically answering the call for lines. Set to 10 sec - 3 calls.
 - featureID - Number determining which feature is assigned to this line key. More here (http://docs.acsdata.co.nz/asterisk-cisco/line-keys-xml.shtml)
 - autoAnswerEnabled - 3 - enable auto answer.

##### 5) Configure number to dial when the messages key is pressed.
```
<messagesNumber>VOICEMAIL_NUMBER</messagesNumber>
```
You can use another number for each line. And can use it for speed dial.

##### 6) Configure access.
```
<settingsAccess>2</settingsAccess>

<sshAccess>1</sshAccess>
<sshPort>22</sshPort>
<webAccess>1</webAccess>
```
 - sshAccess - 1 - disabled. For enable set 0. Restricts access to the phone's ssh-server.
 - webAccess - 1 - disabled. For enable set 0. Restricts access to the phone's web-server.
 - settingsAccess - enables and disables the Settings button on an IP phone. Useful to lock the phone config down.

   0 = Disabled.

   1 = Enabled (default). The phone user can modify features by using the Settings menu.
   
   2 = Restricted. The phone user is allowed to access User Preferences and volume settings only. 

##### 7) Set minimal ring volume. Maximum is 15.
```
<minimumRingVolume>10</minimumRingVolume>
```
 - minimumRingVolume - minimum volume of the phone's ringer. A number between 0 (off) to 15 (full).

##### 8) Configure userLocale fnd networkLocale settings. You will have native language message on the phone display. The Network locales allows the phone to play tones (ringing, busy etc.) native to the phone's country. More here (http://docs.acsdata.co.nz/asterisk-cisco/user-locale.shtml), (http://docs.acsdata.co.nz/asterisk-cisco/network-locale.shtml)
```
<userLocale>
<networkLocale>
```

##### 9) URL to use when the directories or contacts key is pressed. If necessary, set folder, where you store phonebook xml file.
```
<directoryURL>http://ASTERISK_SERVER_IP/phonebook.xml</directoryURL>
```

##### 10) Set transport protocol. As I'm using not reliable network infrastructure, so I use TCP for transport. As you can, use UDP, it faster.
```
<transportLayerProtocol>4</transportLayerProtocol>
```
 - transportLayerProtocol - what protocol the phone will use to connect to Asterisk (UDP, TCP). Only use 4 (TCP), as the phone causes SIP retransmit errors when using UDP.

   1 =	Use device default	

   2 =	UDP	

   4 =	TCP
   
##### 11) Disable DND.
```
<dndCallAlert>0</dndCallAlert>
<dndReminderTimer>5</dndReminderTimer>
```
 - dndCallAlert - how the phone displays an incoming call when DND is enabled and dndbusy is set to no in sip.conf.

   0 =	Disable
   
   1 =	Beep Only
   
   5 =	Flash Only

 - dndReminderTimer - how often in minutes to play a beep tone through the speaker when DND is enabled.

![6921](https://github.com/msergiy87/phone_cisco_6921/blob/master/6921.jpg)
