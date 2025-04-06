## Notes from Lab Enviroment

A website is accessible at http://target.ine.local. Perform reconnaissance and capture the following flags.

- Flag 1: This tells search engines what to and what not to avoid.
- Flag 2: What website is running on the target, and what is its version?
- Flag 3: Directory browsing might reveal where files are stored.
- Flag 4: An overlooked backup file in the webroot can be problematic if it reveals sensitive configuration details.
- Flag 5: Certain files may reveal something interesting when mirrored.
### Tools
Firefox
Curl
HTTrack

### Note
In this lab, the flag will follow the format: FLAG1{MD5Hash} OR FL@G1{MD5Hash}. For example, FLAG1{0f4d0db3668dd58cabb9eb409657eaa8}. You need to submit only the MD5 hash string, excluding the braces. For instance: 0f4d0db3668dd58cabb9eb409657eaa8.


## Flag 1

This tells search engines what to and what not to avoid.

![[Pasted image 20250406222937.png]]

## Flag II

What website is running on the target, and what is its version?

```bash
┌──(root㉿INE)-[~/websites]
└─# curl -s http://target.ine.local | grep generator
<meta name="generator" content="WordPress 6.5.3 - FL@G2{25817159773f4c8e80e9093181c85ee5}" />

```

Here, I took help of ChatGPT and Got this 


### Check the Meta Generator Tag in the HTML

Most WordPress sites include a meta tag in the `<head>` that shows the version.

```bash
curl -s https://example.com | grep -i "generator"`
```


## Flag 3

Directory browsing might reveal where files are stored.



## Flag 4

An overlooked backup file in the webroot can be problematic if it reveals sensitive configuration details.

### **Solution**
So, I ran wpscan on this website as it is running wordpress site & I got this

