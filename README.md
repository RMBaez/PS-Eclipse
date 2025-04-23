<h1>PS-Eclipse</h1>


<h2>Description</h2>

You are a SOC Analyst for an MSSP (Managed Security Service Provider) company called TryNotHackMe .

A customer sent an email asking for an analyst to investigate the events that occurred on Keegan's machine on Monday, May 16th, 2022 . The client noted that the machine is operational, but some files have a weird file extension. The client is worried that there was a ransomware attempt on Keegan's device. 

Your manager has tasked you to check the events in Splunk to determine what occurred in Keegan's device. 




<h2>Questions</h2>

- <b>1. A suspicious binary was downloaded to the endpoint. What was the name of the binary?</b>
- <b>2. What is the address the binary was downloaded from? Add http:// to your answer & defang the URL.</b>
- <b>3. What Windows executable was used to download the suspicious binary? Enter full path.</b>
- <b>4. What command was executed to configure the suspicious binary to run with elevated privileges?</b>
- <b>5. What permissions will the suspicious binary run as? What was the command to run the binary with elevated privileges? (Format: User + ; + CommandLine)</b>
- <b>6. The suspicious binary connected to a remote server. What address did it connect to? Add http:// to your answer & defang the URL.</b>
- <b>7. A PowerShell script was downloaded to the same location as the suspicious binary. What was the name of the file?</b>
- <b>8. The malicious script was flagged as malicious. What do you think was the actual name of the malicious script?</b>
- <b>9.A ransomware note was saved to disk, which can serve as an IOC. What is the full path to which the ransom note was saved?</b>
- <b>10.The script saved an image file to disk to replace the user's desktop wallpaper, which can also serve as an IOC. What is the full path of the image?</b>


<h2>Languages and Utilities Used</h2>

- <b>Splunk</b> 


<h2>Environments Used </h2>

- <b>TryHackMe VM</b>






<h2>Program walk-through</h2>

<b>Answer the question below <br/>

1. A suspicious binary was downloaded to the endpoint. What was the name of the binary?

<p align="center">
  First, I adjusted the time to All Time and in Verbose mode. Then on the search bar I wrote down ' index=* '.
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/c4dbb25b-5290-4b47-b8a5-a47940d94961" />
  I then scrolled to the interestin field "Images" to look for any thing suspicious. I found one in the TEMP folder. I plugged that one in and it was the correct answer.
<img width="1440" alt="Screenshot 2025-04-22 at 9 34 12 PM" src="https://github.com/user-attachments/assets/1200151c-57de-4fba-8497-230bd8770972" />





<br />
<br />
Answer: OUTSTANDING_GUTTER.exe<br/>





<h2>Program walk-through</h2>

<b>Answer the question below <br/>
2. What is the address the binary was downloaded from? Add http:// to your answer & defang the URL.

<p align="center">
   I put into the search bar 'OUTSTANDING_GUTTER.exe'. Then I went to the field 'CommandLine". I saw a command that had the suspicious binary running on a schedule
<img width="1440" alt="Screenshot 2025-04-22 at 9 45 41 PM" src="https://github.com/user-attachments/assets/d88df8c9-e1af-498d-ba74-4ae51d17af53" />
    I looked a bit deeper into the events and saw this guy
<img width="1440" alt="Screenshot 2025-04-22 at 9 58 50 PM" src="https://github.com/user-attachments/assets/a14a9237-5f06-4805-a07b-55810d5bf305" />
    I copied and pasted the encoded command into cyberchief. I put in the following operations in the recipe field of cyberchief.. From Base64, Decode Text, and Defang. The Answer is highlighted in green
<img width="1440" alt="Screenshot 2025-04-22 at 10 02 35 PM" src="https://github.com/user-attachments/assets/d583c867-aa16-41de-9d55-cbd8cdd6a291" />







<br />
<br />
Answer: hxxp[://]886e-181-215-214-32[.]ngrok[.]io<br/>




<h2>Program walk-through</h2>

<b>Answer the question below <br/>
3. What Windows executable was used to download the suspicious binary? Enter full path.

<p align="center">
   I went back to 'OUTSTANDING_GUTTER.exe' in the search bar, pressed enter and looked foerexecutable commands on powershell and found this which contains the answer
<img width="1440" alt="Screenshot 2025-04-22 at 10 12 47 PM" src="https://github.com/user-attachments/assets/da8c4839-a708-4202-a59e-ce6ed9ebf6f5" />
  



<br />
<br />
Answer: C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe <br/>






<h2>Program walk-through</h2>

<b>Answer the question below <br/>
4. 

<p align="center">
    I filtered the binary 'IonicLarge.exe' into the search bar. I went to the field 'DestinationIp' and look for any connection(s) made twice to the same ip. Only one did. Defang the ip and that is the answer.
<img width="1440" alt="Screenshot 2025-04-21 at 10 09 58 AM" src="https://github.com/user-attachments/assets/c983acea-f9a5-430d-a2c1-225c11cdf949" />




<br />
<br />
Answer: 2[.]56[.]59[.]42 <br/>



<h2>Program walk-through</h2>

<b>Answer the question below <br/>

5. 

<p align="center">
    I filtered the binary 'IonicLarge.exe' into the search bar. I then went to the field 'EventType' and added 'CreateKey' filter into the search bar. The first event contained the answer
    <img width="1440" alt="Screenshot 2025-04-21 at 10 31 12 AM" src="https://github.com/user-attachments/assets/7fe1dc3a-d543-4284-af55-5a0633a28507" />





<br />
<br />
Answer:  HKLM\SOFTWARE\Policies\Microsoft\Windows Defender<br/>






<h2>Program walk-through</h2>

<b>Answer the question below <br/>

6. 

<p align="center">
    There was a hint to this question and it said Process were killed with 'taskkill /im'. I added it into the search bar. Received 5 events. I went to the field 'CommandLine' where the answer could be found.
<img width="1440" alt="Screenshot 2025-04-21 at 10 52 16 AM" src="https://github.com/user-attachments/assets/003c3e7d-b529-4f79-8671-d26cde9b80a0" />




<br />
<br />
Answer: WvmIOrcfsuILdX6SNwIRmGOJ.exe, phcIAmLJMAIMSa9j9MpgJo1m.exe <br/>





<h2>Program walk-through</h2>

<b>Answer the question below <br/>
7. 

<p align="center">
     I added powershell into the search since I was looking for a powershell command. I need to organize the data some more so I added the command “| Table _time CommandLine” to make a list and "| dedup CommandLine" to remove duplicates.
  <img width="1440" alt="Screenshot 2025-04-21 at 11 13 10 AM" src="https://github.com/user-attachments/assets/4a2cc1fa-e7a0-4abe-bc51-ff81befe9c7a" />





<br />
<br />
Answer: powershell WMIC /NAMESPACE:\\root\Microsoft\Windows\Defender PATH MSFT_MpPreference call Add ThreatIDDefaultAction_Ids=2147737394 ThreatIDDefaultAction_Actions=6 Force=True <br/>




<h2>Program walk-through</h2>

<b>Answer the question below <br/>
8.



<p align="center">
    The IDs are shown based on the previous search bar filter. Go one by one looking at the different exectuables.





<br />
<br />
Answer: 2147735503,2147737010,2147737007,2147737394 <br/>






<h2>Program walk-through</h2>

<b>Answer the question below <br/>
9. 

<p align="center">
   I knew I had to go to a new directory under the same user so I put into the search bar ' index=main C:\\Users\\Finance01\\AppData '.
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/2a897bd0-cf91-4dd0-a9a7-44acc094b758" />
    I went to the field Images and looked at the results. There were two with a high count. I did not know which binary was malicious or if either of them where. I did google searches on them and found that one of them was an adware.
<img width="1440" alt="Screenshot 2025-04-21 at 12 14 24 PM" src="https://github.com/user-attachments/assets/fd28f46d-9115-4392-8e1e-f56f7cfe759d" />






<br />
<br />
Answer: C:\Users\Finance01\AppData\Roaming\EasyCalc\EasyCalc.exe<br/>




<h2>Program walk-through</h2>

<b>Answer the question below <br/>
10.

<p align="center">
   I plugged in the search 'index=main C:\Users\Finance01\AppData\Roaming\EasyCalc\EasyCalc.exe'. To get the full picture of the path, I went to the field 'ImageLoaded'. There I was able the dll files.
<img width="1440" alt="image" src="https://github.com/user-attachments/assets/168384e1-d50c-47a7-91d7-1d6f04e54437" />







<br />
<br />
Answer: ffmpeg.dll,nw.dll,nw_elf.dll<br/>
