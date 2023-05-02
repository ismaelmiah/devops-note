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

from container: `tcpdump icmp`

from host: `ping 172.17.0.2`

![ICMP packets](/Assets/Images/solution_10.png "ICMP packets")