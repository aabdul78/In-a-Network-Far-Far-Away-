# In-a-Network-Far-Far-Away-
Homework 9

You are a Network Jedi working for the Resistance.

The Sith Empire recently carried out a DoS attack, taking out the Resistance's core network infrastructure, including its DNS servers.

This attack destroyed the Resistance's ability to communicate via email and retrieve other crucial information about one another's operations. The Empire has taken advantage of this compromised availability by ambushing numerous Resistance outposts, all vulnerable because the Resistance can no longer call for help.

Your task is a crucial one: restore the Resistance's core DNS infrastructure and verify that traffic is routing as intended.

Objectives:

Topics Covered in This Assignment
DNS
nslookup
DNS record types
A, PTR, MX, NS, SOA, SRV, TXT
Wireless
WEP, WPA
Aircrack-ng
Wireshark Wireless analysis and decryption

Mission 1:

Issue: With the DoS attack, the Empire took down the Resistance's DNS and primary email servers.

The Resistance's network team was able to build and deploy a new DNS server and mail server.

The new primary mail server is asltx.1.google.com, and the secondary mail server should be asltx.2.google.com.

The Resistance (starwars.com) is able to send emails but unable to receive any.

Your Mission

Determine and document the mail servers for starwars.com using NSLOOKUP.

Answer
command: - nslookup type=mx starwars.com

Explain why the Resistance isn't receiving any emails.

Answer

The Resistance is unable to receive emails because the new primary mail server, asltx.1.google.com, and the secondary server, asltx.2.google.com, are not configured as part of the mail exchanger (MX) records. The new mail servers are not listed in the Resistance's DNS email server settings.

Document what a corrected DNS record should be.

Answer

The corrected DNS should be like this.

starwars.com mail exchanger = 1 asltx.l.google.com

starswars.com mail exchanger = 2 asltx.2.google.com

![image](https://github.com/user-attachments/assets/b1a03ae8-9297-4b72-ab6f-07dfd4353bbd)


Mission 2:

Issue: Now that you've addressed the mail servers, all emails are coming through. However, users are still reporting that they haven't received mail from the theforce.net alert bulletins.

Many of the alert bulletins are being blocked or going into spam folders.

This is probably because theforce.net changed its mail server's IP address to 45.23.176.21 while your network was down.

These alerts are critical for identifying pending attacks from the Empire.

Your Mission:

Determine and document the SPF for theforce.net using nslookup.

Answer

nslookup -type=TXT theforce.net

Explain why the Force's emails are going to spam.

Answer
The IP address 45.23.176.21 for their mail server is not included in the DNS records for theforce.net.

Document your suggested DNS corrections.

![image](https://github.com/user-attachments/assets/3e507a3b-599c-4a4d-a662-2cd38c47fd30)

Mission 3

Issue: You have successfully resolved all email issues and the resistance can now receive alert bulletins. However, the Resistance is unable to easily read the details of alert bulletins online. They are supposed to be automatically redirected from their sub page of resistance.theforce.net to theforce.net.

Your mission:
Document how a CNAME should look by viewing the CNAME of www.theforce.net using NSLOOKUP.

Answer

nslookup -type=CNAME www.theforce.net

Explain why the sub page of resistance.theforce.net isn't redirecting to

Answer

The Alliance server is displaying an incorrect entry for theforce.net, including an inaccurate canonical name.

Document what a corrected DNS record should be.

Answer

Resistance.theforce.net canonical name = theforce.net.

![image](https://github.com/user-attachments/assets/e05f8884-d6a4-439a-8337-f219342b82e7)


Mission 4

Issue: During the attack, it was determined that the Empire also took down the primary DNS server of princessleia.site.

Fortunately, the DNS server for princessleia.site is backed up and functioning.

However, the Resistance was unable to access this important site during the attacks, and they need you to prevent this from happening again.

The Resistance's networking team provided you with a backup DNS server of: ns2.galaxybackup.com.

Your Mission:

Confirm the DNS Records for princessleia.site

![image](https://github.com/user-attachments/assets/675be60d-35af-4dcf-a4c6-7b535951bf78)

Document how you would fix the DNS record to prevent this issue from happening again.

Answer
princessleia.site nameserver = ns25.domaincontrol.com.
princessleia.site nameserver = ns26.domaincontrol.com.


Mission 5

Issue: The network traffic from the planet of Batuu to the planet of Jedha is very slow. You have been provided a network map with a list of planets connected between Batuu and Jedha. It has been determined that the slowness is due to the Empire attacking Planet N.

Your Mission:
View the Galaxy Network Map and determine the OSPF shortest path from Batuu to Jedha. Confirm your path doesn't include Planet N in its route. Document this shortest path so it can be used by the Resistance to develop a static route to improve the traffic.

Answer

The shortest bath between the Batuu and Jedha is as following Batuu > D > C > E > F > J > I > L > Q > T > V > Jedha.

![image](https://github.com/user-attachments/assets/37b86897-fb93-4056-8647-c54e46a9a4c7)


Mission 6

Issue: Due to all these attacks, the Resistance is determined to seek revenge for the damage the Empire has caused. You are tasked with gathering secret information from the Dark Side network servers that can be used to launch network attacks against the Empire. You have captured some of the Dark Side's encrypted wireless internet traffic in the following pcap: Darkside.pcap.

Your Mission:

Figure out the Dark Side's secret wireless key by using Aircrack-ng. Hint: This is a more challenging encrypted wireless traffic using WPA. In order to decrypt, you will need to use a wordlist (-w) such as rockyou.txt. Use the Dark Side's key to decrypt the wireless traffic in Wireshark. Hint: The format for they key to decrypt wireless is <Wireless_key>:.


Answer

aircrack-ng -w /usr/share/wordlists/rockyou.txt Darkside.pcap

aircrack-ng -w /usr/share/wordlists/rockyou.txt Darkside.pcap

![image](https://github.com/user-attachments/assets/6c2afd0c-8825-4c03-964e-553650f82b39)

Once you have decrypted the traffic, figure out the following Dark Side information: Host IP Addresses and MAC Addresses by looking at the decrypted ARP traffic.

![image](https://github.com/user-attachments/assets/dff2f7c9-0322-4169-a7ae-e634cce81251)

Document these IP and MAC addresses, as the Resistance will use them to launch a retaliatory attack.

Answer

MAC: address: Cisco-Li_e3:e4:01 (00:0f:66:e3:e4:01) IP address: 172.16.0.1 MAC address : IntelCor_55:98:ef (00:13:ce:55:98:ef) IP address : 172.16.0.101

Mission 7

As a thank you for saving the galaxy, the Resistance wants to send you a secret message!

Your Mission:

View the DNS record from Mission #4. The Resistance provided you with a hidden message in the TXT record, with several steps to follow. Follow the steps from the TXT record. Note: A backup option is provided in the TXT record (as a website) in case the main telnet site is unavailable Take a screen shot of the results.

![image](https://github.com/user-attachments/assets/0f1e4e41-c644-4e90-95b7-db41f7b06896)




