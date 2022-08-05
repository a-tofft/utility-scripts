
# Utility Scripts 
A collection of simple bash scripts I keep in my ~/scripts folder for easy access and to make my life a bit easier by automating certain tasks or executing commands hard to remember. 

# Setup 
```bash
git clone https://github.com/a-tofft/utility-scripts.git ~/scripts && cd scripts
export PATH="$(pwd):$PATH"
```
Add following command to bash/zsh/fish config file to make export permanent: 
```bash
export PATH="$HOME/scripts:$PATH"
```

# Scripts 


## video-dl
 - Loops through a textfile containing video urls and attempts to download them all, even if internet is disconnected/interrupted.
 - Successfully downloaded videos are removed from playlist 
 - Can be run as a cronjob, if you want to download any video, just add it to the playlist file.
 - Default location for downloads is `~/Downloads/`
 - Dependencies: `youtube-dl`, `svtplay-dl`

**Usage:**
```bash 
video-dl playlist
```

**playlist**
```
https://www.svtplay.se/video/35926941/rapport/rapport-4-aug-19-30-7?id=8vyvM65
https://www.youtube.com/watch?v=MSak5dvDJTk% 
```


## extract 
 - Useful tool that will extract contents of any type of compressed files. 

**Usage:**
```bash 
extract <file.xz>
```


## ssh-extract
 - Tool that can quickly get output of a command from multiple hosts
 - Dependencies: `sshpass`

**Usage:**
```bash
ssh-extract <hosts_file> <command> <password> >> <output_file>
ssh-extract hosts.txt "uptime" password123 >> hosts-output.txt
```

**hosts.txt**
```
admin@rtr1.example.net
admin@rtr2.example.net
admin@rtr3.example.net 
```

## traffic-debugger
 - Tool intended to execute a traffic command followed by a tcpdump.
 - Will prettyify the output and is useful to quickly check negotiated TCP flags etc without starting up wireshark. 
 - Dependencies: `tcpdump`


### Traceroute

```bash 
sudo traffic-debugger \
    "traceroute 8.8.8.8" \
    "sudo tcpdump host -U 8.8.8.8 -vv" \

```

### Ping

**Check MTU of path and check who dropped it:** 
```bash 
traffic-debugger \
    "ping -M do -s 2000 8.8.8.8 -c 5" \
    "sudo tcpdump icmp -vv" \

```

### Telnet


**Check TCP Handshake parameters quickly:** 
```bash 
traffic-debugger \
    "telnet google.com 80" \
    "sudo tcpdump host -U google.com -vvv" \

```

## npp 
 - Quickly creates a new python project with desired files and adds a remote git origin.
 - Dependencies: `git`

**Usage:**
```bash
npp <project_name> <git_remote_origin>
npp my_project git@github.com:a-tofft/my_project.git
```

## host-overview 
 - Displays a system overview of a linux host, useful when logging into a new server
 - Dependencies: `netstat`, `curl`

**Usage:**
```bash
# Run without sudo 
host-overview

# Run commands as sudo (recommended for full output)
host-overview sudo 
```