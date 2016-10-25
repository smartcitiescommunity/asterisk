Connect SIP PBX
Posted on August 24, 2014 by snlsnl — No Comments ↓	

You can connect SIP PBX to out service to make outgoing calls and incoming calls from mobile clients.

First of all you must create Sipmobile account,

change password to be able to edit your account.

Below is an example how to connect Asterisk PBX.
Outgoing calls

1. If you have compiled Asterisk from source please ensure you have enabled SRTP:

./configure
make menuselect (check res_srtp in “resource modules”)
make
make install

If you are using Asterisk distributions like FreePBX – consult corresponding documentation.

You can check that SRTP module is loaded by the following commands:

# asterisk -r

CLI> module show like srtp

If module is loaded you will see output like this:

Module Description Use Count
res_srtp.so Secure RTP (SRTP)

2. For outgoing calls edit this files:

/etc/asterisk/sip.conf

in [general] section:

register=991xxxxxxx:yyyyyyy@sipmobile.org, where 991xxxxxxx is your phone number, yyyyyyy – your SIP password.

Add section:

[Sipmobile]
host=sipmobile.org
username=991xxxxxxx
secret=yyyyyyy
type=peer
fromuser=991xxxxxxx
fromdomain=sipmobile.org
outboundproxy=sip.sipmobile.org
context=to-trunk-sip-Sipmobile
encryption=yes

Edit your extensions.conf to forward calls to Sipmobile trunk.

Example:

exten => tdial,n,Dial(SIP/Sipmobile/${OUTNUM},90,Tt)

3. Pay some money in Bulling and Payments and you are ready to make cheep international calls.
Incoming calls

Add the following section to your sip.conf:

[Sipmobile]
host=144.76.238.124
type=peer
canreinvite=no
context=from-trunk-sipmobile
encryption=yes
transport=udp,tcp,tls

In extensions.conf under the section [from-trunk-sipmobile] you can set your rooting logic.

If you have questions please contact support@sipmobile.org
