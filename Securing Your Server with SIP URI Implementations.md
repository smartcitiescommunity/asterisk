Securing Your Server with SIP URI Implementations

There are two important security steps once you have enabled anonymous SIP URI calling to your server. The first line of defense is to harden the IPtables Firewall to only permit anonymous SIP access to the specific FQDN you plan to use for your SIP URI callers. The second is to harden Asterisk to disallow requests for domains not serviced by your server.

1. Edit the IPv4 rules for your operating system. On the CentOS-compatible platforms, it’s /etc/sysconfig/iptables. On the Debian/Ubuntu/Raspbian platforms, it’s /etc/iptables/rules.v4. Toward the end of the file and just above the final fail2ban entries, insert the following code using your actual FQDN in the first line:

-A INPUT -p udp --dport 5060 -m string --string "@k43X20.mycompany.com" --algo bm -j ACCEPT
-A INPUT -p udp --dport 5060 -m string --string "REGISTER sip:" --algo bm -j DROP
-A INPUT -p udp --dport 5060 -m string --string "OPTIONS sip:" --algo bm -j DROP
-A INPUT -p udp -m udp --dport 5060 -j DROP

2. Run the following commands substituting your actual FQDN in the first line to lock down Asterisk to only your FQDN for anonymous SIP connections:

sed -i '/\[general\]/a ;domain=k43X20.mycompany.com' /etc/asterisk/sip.conf
sed -i '0,/;domain/s/;domain/domain/' /etc/asterisk/sip.conf
sed -i '0,/;allowtransfer=no/s/;allowtransfer=no/allowtransfer=no/' /etc/asterisk/sip.conf
sed -i '0,/; allowexternaldomains=no/s/; allowexternaldomains=no/allowexternaldomains=no/' /etc/asterisk/sip.conf

3. Restart your firewall: iptables-restart

4. Restart Asterisk: asterisk-restart

5. Done!
