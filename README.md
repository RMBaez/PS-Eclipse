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
  First, I adjusted the time to All TIme and in Verbose mode. Then on the search bar I wrote down ' index=main password viewer '.
<img width="1440" alt="Screenshot 2025-04-21 at 9 06 15 AM" src="https://github.com/user-attachments/assets/838a279e-be52-4ecf-8a65-b86ab590429d" />
  I went to the CommandLine field which only had one result. I clicked it and saw two commands but only one was an executable.
<img width="1440" alt="Screenshot 2025-04-21 at 9 07 53 AM" src="https://github.com/user-attachments/assets/6c552bae-9d11-4a7c-bff9-a2a06887465f" />




<br />
<br />
Answer: C:\Users\FINANC~1\AppData\Local\Temp\11111.exe  <br/>





<h2>Program walk-through</h2>

<b>Answer the question below <br/>
2. 

<p align="center">
   I added the command line from question 1 into the search bar. I looked at the field Company and there was the answer.
<img width="1440" alt="Screenshot 2025-04-21 at 9 12 34 AM" src="https://github.com/user-attachments/assets/30e436b2-efd9-4bc0-87f8-df7ca36790e8" />






<br />
<br />
Answer: NirSoft<br/>




<h2>Program walk-through</h2>

<b>Answer the question below <br/>
3. 

<p align="center">
    I removed the previous search filters except for 'index=main'. I added 'EventCode=1' since it is for process creation. I went to the field CurrentDirectory and selceted 'C:\Users\Finance01\AppData\Local\Temp\'.
<img width="1440" alt="Screenshot 2025-04-21 at 9 52 47 AM" src="https://github.com/user-attachments/assets/86c55c55-cbdb-4610-8036-f93309667154" />
    I went down to the field 'Images" which contained the answer to the first question. I selected and clicked on the result 'C:\Users\Finance01\AppData\Local\Temp\IonicLarge.exe'.
<img width="1440" alt="Screenshot 2025-04-21 at 10 00 11 AM" src="https://github.com/user-attachments/assets/56f81ac3-a934-4cd0-bb6c-9c66c5953ce8" />
    I went dow to the field 'OriginalFileName which one had one result. That was the answer to the second question.
<img width="1440" alt="Screenshot 2025-04-21 at 10 02 51 AM" src="https://github.com/user-attachments/assets/3e3a6333-2351-4587-96da-85ae43962afe" />




<br />
<br />
Answer: IonicLarge.exe,PalitExplorer.exe <br/>






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
