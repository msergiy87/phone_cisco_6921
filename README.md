I have used configuration the same as in foloving sites:

https://github.com/amooma/GS3/wiki/Cisco-CP-69xx-VoIP-Telefone-mit-Asterisk-Gemeinschaft
https://zadarma.com/ru/support/instructions/cisco/cisco-6921/

But I need configure some custom settings. For example

1) I used g729a codec and I need callStats for correct end calls

\<preferredCodec>g729a\</preferredCodec>

\<callStats>false\</callStats> 

2) Set messageWaitingLampPolicy to 3

How the phone alerts the user to unread voicemail messages.

The messageWaitingLampPolicy values work like this:

 - Primary Line - Light and Prompt set to 1
 - Primary Line - Prompt Only set to 2
 - Primary Line - Light Only set to 3
 - Light and Prompt presumably set to 4
 - Prompt Only presumably set to 5
 - Light Only presumably set to 6
 - None set to 7

Light Lamp and Display Prompt if message is waiting - 3

'Light' is the bright red lamp on the headset

'Prompt' will show up a flashing voicemail envelope next to the Line on the RHS side of the display when there is voicemail

3) 
