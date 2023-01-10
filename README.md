# Vulnerabilities of Wireless Networks
<p>The content provided is for educational and informational purposes only.</p>

## Evil Twin Attack

<br/>
In this attack scenario, we use a tool called Fluxion. The purpose of the attack is to obtain the password by creating a twin access point. The attack is split into two parts. The first part is intended to capture the 4-way handshake. In the second part, we will create a fake twin access point, to recover the password. After opening the Fluxion tool, first the target must be selected and then a 4-way handshake must be recorded. The attack was done on a local network.
<br/>

<br/>
<details>
  
<summary>More information about Evil Twin Attack</summary>
<br/>
  
### Handshake Snooper

<p>In the screenshot 1.1 below is the interface of the Fluxion tool. To get the 4-way handshake, press 2, then enter (Handshake Snooper).</p>

<p align="center">
<img align="center" width="742" alt="image" src="https://user-images.githubusercontent.com/120057560/211566986-ab1271e9-f7ea-4f5a-809a-40dee3a523cc.png">
</p><p align="center">Screenshot 1.1</p>

<p>Select the third option in the screenshot 1.2. All channels (2.4Ghz & 5Ghz) for the
search for all available channels.</p>

<p align="center"><img width="735" alt="image" src="https://user-images.githubusercontent.com/120057560/211571102-55a827e0-814d-4705-9273-6d59ea29bfbf.png">
</p>
<p align="center">Screenshot 1.2</p>

<p>The screenshot 1.3 below shows the list of available access points with which we can start recording the handshake. So, we choose as a target the first option, which is called COSMOTE.</p>

  <p align="center"><img width="734" alt="image" src="https://user-images.githubusercontent.com/120057560/211571860-a82e36fa-829d-4470-9353-17953b3cf3eb.png">
</p>
<p align="center">Screenshot 1.3</p>

<p>In the screenshot 1.4 shows the attack types. The passive attack has the advantage of being undetectable, but you have to wait until a user connects. This is a disadvantage. In this case, we choose the third option for the attack, mdk4 deauthentication. The aggressive attack, forcing already logged-in users to log out by sending a deauthentication frame.</p>

<p align="center"><img width="734" alt="image" src="https://user-images.githubusercontent.com/120057560/211576619-cca5b919-17c2-492d-b128-20f4b0fa8e51.png">
</p>
<p align="center">Screenshot 1.4</p>

<p>In screenshot 1.5 shows the methods that will verify if the generated PMK of the user matches the 4-way handshake that was recorded. Thus, the hash that will be produced from the password that the user will submit to the Captive Portal is compared. Therefore, we choose the second option, cowpatty verification.</p>
<p align="center"><img width="734" alt="image" src="https://user-images.githubusercontent.com/120057560/211578866-2539177b-dc06-4966-a361-5e46f0b36d9c.png"></p>
<p align="center">Screenshot 1.5</p>

<p>And the Handshake Snooper attack completed, now we have the 4-way handshake, which contains the hash of the password from the access point. In the next section, we will create a fake access point to get the password from the user, after that, we will compare the hash with the password to get access to the original AP.</p>
<p align="center"><img width="652" alt="image" src="https://user-images.githubusercontent.com/120057560/211579343-386f0d74-f79d-4a6f-807f-62e2970685f3.png">
</p>
<p align="center">Screenshot 1.6</p>

### Creating Fake Access Point 

<p>After select the Captive Portal from the first interface, select the Rogue AP - hostpd(screenshot 1.7).</p>
<p align="center"><img width="733" alt="image" src="https://user-images.githubusercontent.com/120057560/211582181-54c1803f-7847-497e-a0ff-892cb2b5d30c.png">
</p>
<p align="center">Screenshot 1.7</p>

<p>The screenshot 1.8, we choose "use hash found". Then, select the cowpatty verification.</p>
<p align="center"><img width="736" alt="image" src="https://user-images.githubusercontent.com/120057560/211583071-9d85b176-7117-4044-a37d-67f2734492b5.png">
</p>
<p align="center">Screenshot 1.8</p>

<p>If we select "None (disable SSL)" this will cause warnings to users because the browser will have to send forms over an unencrypted connection. In this case, we choose to create an SSL certificate (image 1.9).</p>
<p align="center"><img width="733" alt="image" src="https://user-images.githubusercontent.com/120057560/211584420-4c21e3f3-9df7-4196-ab42-47660a3d8bf3.png">
</p>
<p align="center">Screenshot 1.9</p>

<p>The screenshot 1.10 below shows two options for the type of connection to the fake network. In the disconnected option, after connecting to the fake access point, a window appears (popup) to enter the password. On the other hand, the emulated option does not bring up any window for entering the code. When the victim attempts to enter a web page from the browser, they will be redirected to the Captive Portal we have created. However, we are going to select the disconnected connection type.</p>
<p align="center"><img width="727" alt="image" src="https://user-images.githubusercontent.com/120057560/211584765-b68a506c-d5dc-49a5-9d1d-8417ce4ad5b5.png">
</p>
<p align="center">Screenshot 1.10</p>

<p>So we proceed to the last step, before the attack, where we choose the appearance and language of the Captive Portal.(Image 1.11)</p>
<p align="center"><img width="706" alt="image" src="https://user-images.githubusercontent.com/120057560/211588499-072a3d45-0930-4cb3-a9c8-9c93d598cd2f.png">
</p>
<p align="center">Screenshot 1.11</p>

<p>After the user attempt to log in with the correct password, the attack finishes, and we get a text output which is contains the password as shown below.</p>
<p align="center"><img width="700" alt="image" src="https://user-images.githubusercontent.com/120057560/211591711-7648a348-9d8e-44d3-9103-926951e55ba5.png">
</p>
<p align="center">Screenshot 1.12</p>
</details>

## Dictionary Attack

<br/>
  <p>
    In the following attack, we will capture the 4-way handshake on a local network and then use Aircrack-ng to "crack" the key with a dictionary attack
  </p>
<br/>

<details>
  <summary>More information about Dictionary Attack</summary>
  
  <p>
    Before we start, we must manually put the network card in monitor mode. This is achieved by running the command <b>airmon-ng start wlan0</b> in the terminal. Then, to confirm that it is in monitor mode, we type in the terminal the command <b>iwconfig</b> and as shown in screenshot 2.1.
  </p>
  
  <p align="center"><img width="742" alt="image" src="https://user-images.githubusercontent.com/120057560/211658861-56048a00-2fe2-46dd-af6d-503954f84701.png">

</p>
<p align="center">Screenshot 2.1</p>
  
  <p>
    Screenshot below shows the target network with <b>ESSID CYTA-GKS67H</b>, which is the result of the command <b>airodump-ng wlan0mon</b>, which is used to monitor and record packets for networks that are in our range. In this particular case we use it to search and select the target. The screenshot below shows the information that will be needed to record the handshake, the <b>BSSID</b> and the <b>Channel</b>.
  </p>
  
<p align="center">
      <img width="742" alt="image" src="https://user-images.githubusercontent.com/120057560/211659311-eb084e75-a16b-4874-a476-4ebea56b55b7.png">
</p>
<p align="center">Screenshot 2.2</p><br/>

<p>
  Enter the command below. In this case, the airodump-ng command serves to record the 4-way handshake. The parameters used in the airodump-ng command are as follows:
  <br/>
 <b> airodump-ng -c 13 -w /root/attack/file.cap --bssid wlan0mon </b>
      <ul>
        <li> <b>-c</b> is for the channel that used from the target </li>
        <li> <b>--bssid</b>  the MAC address of the target </li>
        <li> <b>-w</b> the location of 4 way handshake </li>
        <li> <b>wlan0mon</b> the network card that is in monitor mode </li>
      </ul>
</p>

<p>
The screenshot below shows that one user is logged in. In this case, we can perform two attacks, the passive and the aggressive. The passive attack is already running, we just have to wait for some user to connect to the access point. Aggressive attack refers to forcing the logout of a user who is already logged in by sending deauthentication packets.
<br/>
We run the command at the terminal:</p> 
<br/>
    <b>aireplay-ng -0 1 -a 72:68:C8:F2:A3:15 -c 44:18:FD:70:AA:04 wlan0mon<b/>
  <ul>
        <li> <b>-0</b> the number of deauthentication packets </li>
        <li> <b>-a</b> the MAC address of target AP</li>
        <li> <b>-c</b> the MAC address of target user</li>
        <li> <b>wlan0mon</b> the network card that is in monitor mode </li>
      </ul>

  
<p align="center">
    <img width="739" alt="image" src="https://user-images.githubusercontent.com/120057560/211664611-96ac7fe3-f23b-4933-9249-5e8f07050564.png">

</p>
  
<p align="center">Screenshot 2.3</p><br/>



<p>
  As a result of the aireplay-ng command, we get the 4-way handshake in the upper right corner in the screenshot 2.4. Now we are ready to dictionary attack. 
<p/>

<p align="center">
 <img width="742" alt="image" src="https://user-images.githubusercontent.com/120057560/211666828-912e24e5-027d-425f-8096-0c43a4ed4c15.png">

 
</p>
  
<p align="center">Screenshot 2.4</p><br/>



<p>
  And we are at the last step, in the dictionary attack. That is a kind of brute force attack. The text file that we use, rockyou.txt, is widely known and contains all the possible vulnerable words that are used for passwords. The command that we are going to use are below
<p/><br/>
      <b>aircrack-ng -w rockyou.txt -b /root/attack/file.cap<b/>
      <ul>
        <li> <b>-w</b> the number of deauthentication packets </li>
        <li> <b>-b</b> the MAC address of target AP</li>
        <li> <b>/root/attack/file.cap</b> the location of 4 way handshake</li>
      </ul>
<p>
  The screenshot 2.5 shows the found password. It took about 8 minutes to find out. In this particular attack, the password was easily found because it was short and existed in the rockyou.txt file. However, finding the password is not always an easy and quick process. It depends on its length and mainly how complicated it is. In this case, the password consisted of a phrase which is quite popular as a password.
<p/>
<p align="center">
    <img width="741" alt="image" src="https://user-images.githubusercontent.com/120057560/211671074-42995dff-feb4-4681-ad11-3885836ae036.png"> 
</p>

<p align="center">Screenshot 2.5</p><br/>


</details>
