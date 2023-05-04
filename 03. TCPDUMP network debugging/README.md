### Run a nginx container with
`sudo docker run -d -p 80:80 --hostname inside-docker --name nginx nginx`

#### Open shell inside that docker container with
`sudo docker exec -it nginx bash`

#### Install TCPDUMP inside the container
`apt-get update apt-get upgrade -y apt-get install tcpdump -y`

#### We will communicate from the host to this container to test out our commands
### 1. Draw the IP Header with detailed bits
![IP Header](/Assets/images/ip-header.png "IP Header")

### 2. What is TCPDUMP?
```TCPDUMP is a tool for analyzing network```
### 3. How to get the HTTPS traffic?
`tcpdump -nnSX port 443`

from container: `tcpdump -nnSX port 443`

from host: `curl https://www.devismael.com`
### 4. For everything on a interface, what is the command?
`tcpdump -i <interface name>`

from container: `tcpdump -i eth0`
from host: `curl localhost`
![Traffic by interface](/Assets/images/solution_04.png "Traffic by interface")
### 5. Write the command to find traffic by IP
`tcpdump host <ip address>`

from container: `tcpdump host 172.17.0.1`

from host: `curl localhost`
### 6. Share the filtering by source and destination?
`tcpdump src <ip address>`

`tcpdump dst <ip address>`

from container: `tcpdump src 172.17.0.1`

from host: `curl localhost`
![Traffice by destination](/Assets/images/solution_06_01.png)

from container: `tcpdump dst 172.17.0.1`

form host: `curl localhost`

![Traffic by destination](/Assets/images/solution_06_02.png "Traffic by destination")

### 7. How to find packets by network?
`tcpdump net <network range>`

from container: `tcpdump net 172.17.0.0/24`

from host: `curl localhost`
![Traffice by network](/Assets/images/solution_07.png "Traffic by network")

### 8. How to see packet contents with hex output?
`add **-X** flag`

from container: `tcpdump dst 172.17.0.1 -X`

from host: `curl localhost`

![Content as hex](/Assets/images/solution_08.png "Content as hex")

### 9. How to find a specific port traffic, write the command
`tcpdump port <port number>`

`tcpdump src port <port number>`

`tcpdump dst port <port number>`

from container: `tcpdump port 80`

from host: `curl localhost`

![Filter by port](/Assets/Images/solution_09.png "Filter by port")

### 10. Show traffic of one protocol command
`tcpdump <protocol>`

from container: 
        
    tcpdump icmp

from host: 

    ping 172.17.0.2

![ICMP packets](/Assets/Images/solution_10.png "ICMP packets")

### 11. Write the command showing only IP6 traffic

    tcpdump ip6
### 12. Write the command for finding traffic using port range.
`tcpdump portrange <port range>`

From Container

    tcpdump portrange 70-330
From Host

    curl localhost:80
![filter by port range](/Assets/Images/solution_12.png "filter by port range")

### 13. What are PCAP (PEE-cap) files?
PCAP or PEE-cap files are files that contains captured packets. These files can be used by many network analysis tools.

### 14. How are PCAP files processed and why is it so?
The PCAP files are processed by many softwares. They are stored captured packets in binary format.

### 15. Which switch is used to write the PCAP file called capture_file?
the `-w` switch

`tcpdump -w <filename>`

### 16. What is the command for reading/writing capture to a file?

Writing: `tcpdump -w <filename>`

Reading: `tcpdump -r <filename>`

From Container
    
    tcpdump -w capture_file

From Host
    
    curl localhost

![write to file](/Assets/Images/solution_16.png "write to file")

### 17. Which switch is needed to read the PCAP files?
The `-r` switch
### 18. What is the tcpdump command while reading in a file?

Writing: `tcpdump -r <filename>`

From Container

    tcpdump -r capture_file

From Host

    curl localhost

![read from file](/Assets/Images/solution_18.png "read from file")

### 19. Which switch is used for the ethernet header?

The `-XX` flag

### 20. What is line-readable output? How is it notified?

The line readable output is used to view as the packets are being saved or to send output to other command through piping

### 21. What does `-q` imply?
It it used to make the output less informative.

From Container: 

    tcpdump -q -i eth0

From Host: 

    curl localhost

![less output](/Assets/Images/solution_21.png "less output")

### 22. What does the tweak `-t` work?

Gives human readable timestamps.

### 23. What does `-tttt` show?

It gives the maximum human readable timestamp output

From Container: 

    tcpdump -q -tttt -i eth0

From Host: 

    curl localhost

![show full timestamp](/Assets/Images/solution_23.png "show full timestamp")


### 24. To listen on the eth0 interface which one is used?

The `-i eth0` flag

### 25. Purpose for `-vv`?

It is used for maximum verbose output.

### 26. Purpose for `-c`?
By providing a number after it, we can limit the captured packets.

From Container: 

    tcpdump -q -tttt -i eth0 -c 1

From Host: 

    curl localhost

![show full timestamp](/Assets/Images/solution_26.png "show full timestamp")

### 27. Why `-s` is used?
It is used to define the snaplength.
The `-s0` is used to get everything
### 28. What does -S, -e, -E imply?
The `-S` is used to print absolute sequence number.

The `-e` is used to print the ethernet header.

The `-E` is used to decrypt IPSEC traffic by providing encryption key.

### 29. How to show the raw output view?

    tcpdump -ttnnvvS

From Container: 

    tcpdump -ttnnvvS -i eth0

From Host: 

    curl localhost

![show raw output](/Assets/Images/solution_29.png "show full timestamp")

### 30. If a specific IP and destined course are given then which tweak is used?
The `and` or `&&` should be used

From Container:

    tcpdump src 172.17.0.1 and dst 172.17.0.2

From Host:

    curl localhost

![combine command with and](/Assets//Images/solution_30.png "combine command with and")
