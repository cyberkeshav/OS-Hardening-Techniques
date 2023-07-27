<h1>OS Hardening Techniques</h1>

<h2>Description</h2>

In this task, I was asked to review the following scenario and document the incident in detail:

You are a cybersecurity analyst for yummyrecipesforme.com, a website that sells recipes and cookbooks. A disgruntled baker has decided to publish the website’s best-selling recipes for the public to access for free. 

The baker executed a brute force attack to gain access to the web host. They repeatedly entered several known default passwords for the administrative account until they correctly guessed the right one. After they obtained the login credentials, they were able to access the admin panel and change the website’s source code. They embedded a javascript function in the source code that prompted visitors to download and run a file upon visiting the website. After running the downloaded file, the customers are redirected to a fake version of the website where the seller’s recipes are now available for free.

Several hours after the attack, multiple customers emailed yummyrecipesforme’s helpdesk. They complained that the company’s website had prompted them to download a file to update their browsers. The customers claimed that, after running the file, the address of the website changed and their personal computers began running more slowly. 

In response to this incident, the website owner tries to log in to the admin panel but is unable to, so they reach out to the website hosting provider. You and other cybersecurity analysts are tasked with investigating this security event.

To address the incident, you create a sandbox environment to observe the suspicious website behavior. You run the network protocol analyzer tcpdump, then type in the URL for the website, yummyrecipesforme.com. As soon as the website loads, you are prompted to download an executable file to update your browser. You accept the download and allow the file to run. You then observe that your browser redirects you to a different URL, greatrecipesforme.com, which is designed to look like the original site. However, the recipes your company sells are now posted for free on the new website.  

The logs show the following process:
1.	The browser requests a DNS resolution of the yummyrecipesforme.com URL.
2.	The DNS replies with the correct IP address. 
3.	The browser initiates an HTTP request for the webpage.
4.	The browser initiates the download of the malware.
5.	The browser requests another DNS resolution for greatrecipesforme.com.
6.	The DNS server responds with the new IP address.
7.	The browser initiates an HTTP request to the new IP address.
A senior analyst confirms that the website was compromised. The analyst checks the source code for the website. They notice that javascript code had been added to prompt website visitors to download an executable file. Analysis of the downloaded file found a script that redirects the visitors’ browsers from yummyrecipesforme.com to greatrecipesforme.com. 
The cybersecurity team reports that the web server was impacted by a brute force attack. The disgruntled baker was able to guess the password easily because the admin password was still set to the default password. Additionally, there were no controls in place to prevent a brute force attack. 
Your job is to document the incident in detail, including identifying the network protocols used to establish the connection between the user and the website.  You should also recommend a security action to take to prevent brute force attacks in the future.

The report should be split into the following 3 sections:
Section 1: Identify the network protocol involved in the incident
Section 2: Document the incident
Section 3: Recommend one remediation for brute force attacks


<br />


<h2>Resources Used</h2>

- <b>DNS-HTTP-traffic-log</b> 


<h2>Identify the network protocol involved in the incident</h2>

The protocol affected in the incident is Hypertext Transfer Protocol (HTTP). By utilizing tcpdump and accessing the yummyrecipesforme.com website to investigate the issue, a DNS & HTTP traffic log file was generated, which provided the evidence necessary to arrive at this conclusion. The malicious file was observed being delivered to users' computers through the HTTP protocol at the application layer.

<h2>Document the incident</h2>

Multiple customers reported encountering a suspicious scenario on the website, where they were prompted to download a file to update their browsers. Following this download, their personal computers experienced decreased performance. Moreover, the website owner faced an issue with being unable to access their web server account.

To investigate the matter, I employed a sandbox environment, enabling me to examine the website safely without affecting the company's network. By utilizing tcpdump, I captured the network and protocol traffic packets generated during interactions with the website. I, in an attempt to replicate the customers' experience, downloaded and executed the file from the website. Consequently, the browser redirected me to a fraudulent website (greatrecipesforme.com) that bore a striking resemblance to the genuine site (yummyrecipesforme.com).

Upon reviewing the tcpdump log, it was observed that the browser initially requested the IP address for the yummyrecipesforme.com website. Once the HTTP protocol established a connection with the website, I initiated the download of the file, leading to a sudden shift in network traffic. Subsequently, the browser requested a new IP resolution for the greatrecipesforme.com URL, and the network traffic was rerouted accordingly.

Further investigation, led by the senior cybersecurity professional, entailed analyzing the source code of both websites and the downloaded file. As a result, it was discovered that the website had been manipulated by an attacker to incorporate code that tricked users into downloading a malicious file disguised as a browser update. Additionally, due to the website owner being locked out of their administrator account, the team believes that the attacker gained unauthorized access using a brute force attack and subsequently changed the admin password. The execution of the malicious file ultimately compromised the computers of end users.


<h2>Recommend one remediation for brute force attacks</h2

To enhance protection against brute force attacks, the team should plan to devise a security measure involving two-factor authentication (2FA). This plan entails an extra layer of verification for users, requiring them to validate their identity by confirming a one-time password (OTP) sent to either their email or phone. Upon successfully providing their login credentials and the OTP, users will be granted access to the system. The implementation of 2FA ensures that malicious actors attempting brute force attacks are unlikely to gain unauthorized access, as it necessitates an additional level of authorization.
