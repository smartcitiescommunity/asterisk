#! /sbin/iptables-restore
# Generated by iptables-save v1.4.21 on Wed Oct 22 16:06:25 2014
*filter
:INPUT DROP [0:0]
:FORWARD DROP [0:0]
:OUTPUT ACCEPT [1:104]
-A INPUT -i lo -j ACCEPT
-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
-A INPUT -p tcp -m tcp --dport 22 -j ACCEPT
-A INPUT -p icmp -m icmp --icmp-type 8 -j ACCEPT
-A INPUT -p icmp -m icmp --icmp-type 11 -j ACCEPT
-A INPUT -p udp -m udp --dport 5060 -j ACCEPT
-A INPUT -p udp -m udp --dport 5060 -m string --string "sundayddr" --algo bm --to 65535 -j DROP
-A INPUT -p udp -m udp --dport 5060 -m string --string "sipsak" --algo bm --to 65535 -j DROP
-A INPUT -p udp -m udp --dport 5060 -m string --string "sipvicious" --algo bm --to 65535 -j DROP
-A INPUT -p udp -m udp --dport 5060 -m string --string "sipcli" --algo bm --to 65535 -j DROP
-A INPUT -p udp -m udp --dport 5060 -m string --string "friendly-scanner" --algo bm --to 65535 -j DROP
-A INPUT -p udp -m udp --dport 5060 -m string --string "iWar" --algo bm --to 65535 -j DROP
-A INPUT -p udp -m udp --dport 5060 -m string --string "sip-scan" --algo bm --to 65535 -j DROP
-A INPUT -p udp -m udp --dport 10000:20000 -j ACCEPT
-A FORWARD -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
COMMIT
# Completed on Wed Oct 22 16:06:25 2014
