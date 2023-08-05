# Hidden

## Description

Find the flag hidden in the picture

Author : Leong
Points: 150

## Solution

For some reason, the jpg file isn't openable. Using strings command:

AMD EPYC 7551 32-Core Processor                 (with SSE4.2)
Linux 5.15.0-1035-oracle
Dumpcap (Wireshark) 3.2.3 (Git v3.2.3 packaged as 3.2.3-1)
ens3
Linux 5.15.0-1035-oracle
GET /escape.png HTTP/1.1
Host: escape.leong.kr
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0

Change file format to pcap, and analyse gives an [image](./Hidden.md)! 

https://apacket-files.s3.us-west-2.amazonaws.com/0de1de4d-57a9-493f-9fa8-e31625e49bdf.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAILZALZZ2EYXHBOWQ%2F20230805%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230805T024246Z&X-Amz-Expires=900&X-Amz-SignedHeaders=host&X-Amz-Signature=e285c2cd1b9c84134e88c188c06916f76f11d368979fbc679d5c206426f5129e

After a little bit of photoshop magic [flag](./Hidden_Flag.png) was revealed
Flag - ESCAPE{H1dD3n_!n_7he_P1ctur3_1N_TeXt}