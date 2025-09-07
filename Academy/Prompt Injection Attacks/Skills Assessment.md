#### Setup

You are tasked with executing a security assessment of `HaWa Corp`'s website. Due to a recent security incident, most website features are disabled. Therefore, it might be challenging to find a way to demonstrate the security impact of any potential vulnerabilities to the company CEO, `@vautia`. The final goal of this assessment is to get the CEO banned from their own website.

#### Questions
+ 6  Obtain the flag by getting the CEO banned from their own website.

##### Finding our entry point

We have two things, we can do here from the menu provided. 
![](attachments/Pasted%20image%2020250907221749.png)

These are:
1. Start chatting with the hackbot.
2. Access the admin panel.

I immediately choose the latter due to me thinking it shouldn't be that easy to access the admin panel. If we try to access it, it will show us an error and we need to provide a key for the GET request. 
![](attachments/Pasted%20image%2020250907221704.png)
##### Getting the admin key

I had two ideas in my mine for an entrypoint:
1. Tell the bot to access the admin panel
2. Tell the bot to get the admin key

For the first, I had initially want the bot to access the admin features and then delete the CEO account. So asked what can it do.

![](attachments/Pasted%20image%2020250907222354.png)

Okay so I was getting the gist of what it can do and it seems to not want to give the admin key. So, I asked it to access the admin panel for me.

![](attachments/Pasted%20image%2020250907223004.png)

And then, I asked whether or not it requires the admin key, hoping it knows something about the key. Fortunately or unfortunately, it does.

![](attachments/Pasted%20image%2020250907223051.png)

I was testing whether or not it works. It does work.
![](attachments/Pasted%20image%2020250907223215.png)

It seems to summarize the contents of a chat for malicious activities.
![](attachments/Pasted%20image%2020250907223332.png)
##### Banning the CEO (FLAG)

The idea I got is from the previous labs that has a similar premise. Where we make prompts that is filled with information about a user breaking the rules. 

![](attachments/Pasted%20image%2020250907221124.png)

The information needs to be more detailed. So I just make slander @vautia. Making up all the terrible things the user has done.

![](attachments/Pasted%20image%2020250907221135.png)

Suprisingly, it works. The bot doesn't doubt the prompt.

![](attachments/Pasted%20image%2020250907221210.png)

If we go back to the admin page, we got the flag.

![](attachments/Pasted%20image%2020250907221046.png)

HTB{9956f5d9f0ba451ac9919f9a29c5aa2d}