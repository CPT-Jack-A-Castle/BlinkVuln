# Blink Sync Module Vulnerability 

Recently, I discovered a glaring vulnerability within the Blink Camera System Sync Module. I have not had a good experience with their team, and I will go over this later in this page.
CVE ID: CVE-2018-20161

# Requirements

 1. A computer running linux (Kali Linux preferably) 
 2. Nmap, and python-nmap
 3. Scapy
 4. termcolor
 5. Python 3

# Analysis
The following is a both Technical and Layman's Analysis of the vulnerability 
## Layman's Analysis
Below is a simplified explanation of the vulnerability and its implications. A more detailed report is below.
### The vulnerability

If the sync module kicked off the wifi network, live video is no longer accessible from the blink app<sup>1</sup>. Clips triggered by the motion sensor are also **not** saved. This is a bigger deal than the live video, and is the most compromising for the system.

### Implications

If a threat actor was able to deauth a Sync Module, he would be able to gain entry to a facility or home undetected and a video of him breaking in would not be recorded. 

## Technical Analysis
The following is a technical analysis of the vulnerability, including the CVSS score, and proof of concept source code that will discover sync modules on the wifi network and deauth them.
### The vulnerability
Like I said above, this is a Denial Of Service vulnerability within the Blink Sync Module. It is very simple, all you have to do is use any assortment of ways to deauth or kick the Sync Module off of the wifi network. You could also deauth the entire network without having to get the wifi password and join to get the same effect.
The unfortunate thing is, Blink cannot just patch the vulnerability through a software patch. The only way I could see this being fixed would be requiring that the Sync Module is connected to the router or modem over ethernet and not wifi.
![Image](https://i.imgur.com/M8tHhd8.png)
## CVSS Score
Through preliminary estimates, I found this vulnerability to have a medium criticality and a score a 7.0 out of 10. The link to the report can be found [here](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator?vector=AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H/E:F/RL:X/RC:R/CR:L/IR:L/AR:M/MAV:N/MAC:L/MPR:N/MUI:N/MS:U/MC:N/MI:N/MA:H).

# My experience with Blink
My experience with Blink has been less than satisfactory. When I first discovered the vulnerability, it was more difficult than it should be to find their [responsible disclosure webpage](https://blinkforhome.com/pages/responsible-disclosure-policy). On that site, they list the email info@blinkforhome.com as who to contact if a vulnerability is discovered. I did this, and emailed the listed email. They responded by telling me that they were *Sorry I was having this issue with my Sync Module*.<sup>2</sup> I was only truly able to report the vulnerability after two different hour long phone calls with tech support, in which I had to explain what I was trying to do each time. Even then, I did not receive any updates until today, when Blink tech support said that they were referring the ticket to engineering *today* almost three weeks after the initial report. 
Blinks responsible disclosure policy is a joke, and I can only hope that Amazon can at least make it a little better. For the sake of their customers who bought a product looking for peace of mind.
### Credit
Thank you to @chrizator writing netattack, which was used for the deauth portions of this simple script!

### Footnotes
<sup>1</sup>A screenshot of the app when the Sync Module is being deauthed can be found [here](https://i.imgur.com/8aiAtfH.png).

<sup>2</sup>A screenshot of the email exchange can be found [here](https://imgur.com/xYiFiDu).
