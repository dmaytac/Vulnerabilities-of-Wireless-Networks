# Vulnerabilities of Wireless Networks
<p>The content provided is for educational and informational purposes only.</p>

## Evil Twin Attack

<br/>
In this attack scenario, we use a tool called Fluxion. The purpose of the attack is to obtain the password by creating a twin access point. The attack is split into two parts. The first part is intended to capture the 4-way handshake. In the second part, we will create a fake twin access point, to recover the password. After opening the Fluxion tool, first the target must be selected and then a 4-way handshake must be recorded. The attack was done on a local network.
<br/>

<details><summary>More information about Evil Twin Attack</summary>
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
  <summary>More information about Evil Twin Attack</summary>
  
  <p>
    Before we start, we must manually put the network card in monitor mode. This is achieved by running the command ** airmon-ng start wlan0 ** in the terminal. Then, to confirm that it is in monitor mode, we type in the terminal the command ** iwconfig ** and as shown in screenshot 2.1.
  </p>
  
  <p align="center">
</p>
<p align="center">Screenshot 2.1</p>

  

</details>
