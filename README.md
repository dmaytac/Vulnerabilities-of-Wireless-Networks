# Vulnerabilities of Wireless Networks
<p>The content provided is for educational and informational purposes only</p>

<h2>Evil Twin Attach</h2>
<br/>
<p>In the first attack scenario, we use a tool called Fluxion. The purpose of the attack is to obtain the password by creating a twin access point. The attack is split into two parts. The first part is intended to capture the 4-way handshake. In the second part, we will create a fake twin access point, to recover the password. After opening the Fluxion tool, first the target must be selected and then a 4-way handshake must be recorded. The attack was done on a local network.</p>

<p>In picture 1.1 is the interface of the Fluxion tool. To get the 4 -way handshake, press 2, then enter (Handshake Snooper).</p>

<p align="center">
<img align="center" width="742" alt="image" src="https://user-images.githubusercontent.com/120057560/211566986-ab1271e9-f7ea-4f5a-809a-40dee3a523cc.png">
</p><p align="center">Image 1.1</p>

<p>In picture 1.2 select the third option. All channels (2.4 Ghz & 5Ghz) for the
search for all available channels.</p>

<p align="center"><img width="735" alt="image" src="https://user-images.githubusercontent.com/120057560/211571102-55a827e0-814d-4705-9273-6d59ea29bfbf.png">
</p>
<p align="center">Image 1.2</p>

<p>The picture 1.3 shows the list of available access points with which we can start recording the handshake. So, we choose as a target the first option, which is called COSMOTE.</p>

  <p align="center"><img width="734" alt="image" src="https://user-images.githubusercontent.com/120057560/211571860-a82e36fa-829d-4470-9353-17953b3cf3eb.png">
</p>
<p align="center">Image 1.3</p>

<p>In picture 1.4 shows the attack types. The passive attack has the advantage of being undetectable, but you have to wait until a user connects. This is a disadvantage. In this case, we choose the third option for the attack, mdk4 deauthentication. The aggressive attack forcing already logged-in users to log out by sending a deauthentication frame.</p>

<p align="center"><img width="734" alt="image" src="https://user-images.githubusercontent.com/120057560/211576619-cca5b919-17c2-492d-b128-20f4b0fa8e51.png">
</p>
<p align="center">Image 1.4</p>

<p>In pictures 1.5 shows the methods that will verify if the generated PMK of the user matches the 4-way handshake that was recorded. Thus, the Hash that will be produced from the password that the user will submit to the Captive Portal is compared. Therefore, we choose the second option, cowpatty verification.</p>
<p align="center"><img width="734" alt="image" src="https://user-images.githubusercontent.com/120057560/211578866-2539177b-dc06-4966-a361-5e46f0b36d9c.png"></p>
<p align="center">Image 1.5</p>

<p> </p>
<p align="center">
</p>
<p align="center">Image 1.6</p>
