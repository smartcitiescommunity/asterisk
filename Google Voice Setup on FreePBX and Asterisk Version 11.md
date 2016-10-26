Google Voice Setup on FreePBX and Asterisk Version 11

This past weekend I installed a fresh new FreePBX (FreePBX 2.11.0) distribution with Asterisk 11.3. The install of FreePBX and Asterisk is made simple and once installed you have a fully functioning PBX waiting for your phones and trunks to connect.

I don’t have a trunk provider at this time so I decided to use Google Voice as my solution. The process of setting this up via the FreePBX WebUI was simplified and simply works. Best of all you have this all configured and running in under 10 min’s (5 min’s if you have done this more than once).

Here are the steps I took to get this up and running.

Requirements:

    Computer (I am using a VMware Virtual Machine, 1GB of RAM, 2 vCPU, 16GB HDD)
    Latest FreePBX Distribution CD/ISO (ISO works best for me to mount in VMware ESX)
    Google Voice Account
    Hardware or Softphone (I have tested with XLite and CSipSimple for Android)

After you have installed FreePBX and are up and running you will need to enter the webUI (http:// pbx address). From here you do the following:

Under Connectivity

    Select Google Voice (Motif)
    Under Typical Settings Enter your 
    Google Voice Username 
    Google Voice Password
    Google Voice Phone Number (10 digit number, no spaces or dashes)
    Check the option to Add Trunk
    Check the option to Add Outbound Routes
    Check the option to Send Unanswered ‘calls’ to Google Voicemail (optional)
    Under Advanced Setting > Google Voice Status Message (keep it short)
    In the XMPP Priority – Leave this as it is. No need to change this
    Click Submit, followed by applying the settings (you’ll notice it in red up at the top navigation area)

Under Applications

    Select Extensions
    Device: Generic SIP Device and Submit
    Configure an extension id (example: 101)
    Fill in the Display Name (example: jermsmit)
    Find your way down to ‘device options’
    In the ‘secret’ a default passphrase is give, replace this what a value of your choosing 
    Scroll down to the bottom and Click Submit

Under Connectivity

    Inbound Routes
    Create a description (example: GV_GoogleVoiceNumber)
    In DID place your 10 digit Google Voice Number
    Scroll down to ‘Set Destination’
    Change the value to Extension and choose the extension you created above
    Click Submit

Lastly you want to edit your sip settings

Under Settings

    Choose Asterisk SIP Settings
    Change the value of NAT to ‘yes’
    Change the IP Configuration to ‘Dynamic IP’ (in my case)
    Under Dynamic Host, enter your hostname (keep default refresh rate)
    Under Local Networks fill out the info pertaining to your network. You can also attempt to use the Auto Configure if so desired.
    Under Codecs you can leave the defaults (I enabled all of them)
    Scroll to the bottom and Click Submit Changes

At this point you should be all set to test with your SIP Client. Simple log in using the extension and secret (password). Once registered attempt to place a phone call. Open port 5060 on your firewall and you can use this to connect to your server remotely.
