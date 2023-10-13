# Typical Linux bugs fixed
Step by step guide to typical linux bugs 

## Cannot run sudo apt update due to error

So I realised I had this error due to the fact that I couldn't open code, it looks like it has been deleted
![image](https://github.com/debbie-israel/linux-bugs-fixed/assets/56561804/16b34634-ee0f-492c-8eff-294e257c57f9)

Consecuently I run sudo apt update but couldn't run it as well
![image](https://github.com/debbie-israel/linux-bugs-fixed/assets/56561804/d6ec6064-d095-4f02-b2d6-3f05ec3c529a)

Malformed entrt in list file /etc/apt/source.list

Upfront, the /etc/apt/source.list is a configuration file for Linux's Advance Packaging Tool, that holds URLs and other information for remote repositories from where software packages and applications are installed. Same goes with files inside /etc/apt/sources.list.d/.

In my case I found this error:

```
E: Malformed entry 1 in list file /etc/apt/source.list.d/hashicorp.list (Component)
E: The list of sources cannot be read.
```

Consecuently I opened the configuration file /etc/apt/source.list.d/hashicorp.list to see what component is causing the error

```
$ cat  /etc/apt/source.list.d/hashicorp.list
deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com  main
```

Even though I modified the Component or the Suite a couple of times it gave always the same error.
The error was finally solved by updating the config list: 

```
$ sudo su
# rm /etc/apt/source.list.d/hashicorp.list
# apt update
# apt upgrade
```

<br>
![image](https://github.com/debbie-israel/linux-bugs-fixed/assets/56561804/a29e9684-60fc-41a6-b4dc-ed4c333ea040)
<br>

Hope this helps if you find a similar error! 
Credits: https://stackoverflow.com/questions/42410134/how-to-fix-e-the-list-of-sources-could-not-be-read-could-not-be-read-error/74236593#74236593?newreg=720f947bdb0247c087d1d0af115f7336

After this I was able to run : 

```
# su - <my user>
$ sudo apt update
$ sudo apt install software-properties-common apt-transport-https wget -y
$ wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
$ sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
$ sudo apt install code
```
And have vscode back again!!
