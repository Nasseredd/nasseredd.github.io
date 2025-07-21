---
title: "How I Fixed My Grid'5000 Connection Problem in VS Code on Windows"
permalink: /blog/hpc-and-cloud/vscode-g5k-windows
author_profile: true
---

If you're on a Windows machine and struggling to connect to Grid'5000 using VS Code + SSH, you're on the right place.

I assume you've already set up your SSH configuration file at ```C:\Users\nmonir\.ssh\config``` with content similar to the following: 

```shell
Host g5k
User nmonir
HostName access.grid5000.fr
ForwardAgent no

Host *.g5k
User nmonir
ProxyCommand ssh g5k -W "$(basename %h .g5k):%p"
ForwardAgent no
```

This setup works well on Linux or macOS, but it fails on Windows due to differences in how shell commands are parsed.

When you try to connect using VS Code's Remote-SSH extension, you may see an error like this:

```
channel 0: open failed: connect failed: Name or service not known
stdio forwarding failed
Connection closed by UNKNOWN port 65535
``` 

This is a clear sign that something is wrong with the SSH forwarding or proxy configuration.

Why this happens on Windows? To understand the issue, recall how Grid'5000 access works: you first connect to the main frontend via: ```ssh nmonir@access.grid5000.fr```. Then, from there, you connect to a specific site (e.g., Nancy): ```ssh nancy.g5k```. The line in your SSH config starting from ```Host *.g5k``` with the ```ProxyCommand``` is meant to automate this two-step process, allowing you to directly reach any site from your local machine. However, this trick relies on shell substitution: ```ProxyCommand ssh g5k -W "$(basename %h .g5k):%p"```. 

This uses Unix-style command substitution (```$(...)```) which PowerShell and Windows CMD do not support. As a result, the wildcard host entries and dynamic substitution silently fail on Windows.

To make things work on Windows, you should explicitly define the remote site you're trying to reach. Replace the wildcard rule with a hardcoded one for the site you need. For example, if you're trying to reach the Nancy site:

```shell
Host nancy.g5k
User nmonir
HostName nancy
ProxyCommand ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null nmonir@access.grid5000.fr -W nancy:22
```

This version avoids shell substitution entirely, making it compatible with OpenSSH on Windows.

Now, let's test the SSH connection in PowerShell. Open your terminal (PowerShell is fine) and run: ```ssh nancy.g5k```. If this connects successfully and logs you into the remote Nancy frontend, then you're good to go. 

Once SSH works in PowerShell, return to VS Code and reconnect as you tried previously: 

1. Open the Command Palette (```Ctrl + Shift + P```)
2. Choose ```Remote-SSH: Connect to Host...```
3. Select ```nancy.g5k```

VS Code should now be able to connect, install its remote server, and give you access to a terminal and file explorer on Grid'5000.