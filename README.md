# Lab-6-Building-intuition-for-DNS
In this home lab, I will ping, configure, and flush the DNS for the client-1 VM environment I set up in previous labs. I will also comment under the screenshots my findings/observations.


A-Record Exercise
1.	Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin)
2.	Connect/log into Client-1 as an admin (mydomain\jane_admin)
3.	From Client-1 try to ping “mainframe” notice that it fails
4.	Nslookup “mainframe” notice that it fails (no DNS record)

![image](https://github.com/user-attachments/assets/1c142881-9e70-42ce-8eff-9a44ad570fdd)

 
5.	Create a DNS A-record on DC-1 for “mainframe” and have it point to DC-1’s Private IP address

![image](https://github.com/user-attachments/assets/2a167ea5-4e95-4b05-98af-346192aeebd8)

 
6.	Go back to Client-1 and try to ping it. Observe that it works
 
![image](https://github.com/user-attachments/assets/7cc3cbb4-7ce7-4a2c-91fc-87efb828b0ca)


Local DNS Cache Exercise
7.	Go back to DC-1 and change mainframe’s record address to 8.8.8.8

![image](https://github.com/user-attachments/assets/84296ff6-b388-4fd4-aae8-14f2ec3cfabb)

 
8.	Go back to Client-1 and ping “mainframe” again. Observe that it still pings the old address

![image](https://github.com/user-attachments/assets/50a09d29-f37e-4b96-8512-bc0e4d5085b8)

 
9.	Observe the local dns cache (ipconfig /displaydns)

![image](https://github.com/user-attachments/assets/2e2aa513-b23d-4bac-acb1-448b33c41fca)

 
10.	Flush the DNS cache (ipconfig /flushdns).
11.	Observe that the cache is empty (ipconfig /displaydns)
12.	Attempt to ping “mainframe” again. Observe the address of the new record is showing up

![image](https://github.com/user-attachments/assets/a244e852-42db-4855-8b8f-9443b6525104)

 
Here you can see that after flushing the DNS the new private IP address (8.8.8.8) now appears instead of the initial port forwarded 10.0.0.4 we had assigned.

CNAME Record Exercise
13.	Go back to DC-1 and create a CNAME record that points the host “search” to www.google.com

![image](https://github.com/user-attachments/assets/1dc60c25-e8ab-426f-a912-dc93a6302de4)

 
14.	Go back to Client-1 and attempt to ping “search”, observe the results of the CNAME record
15.	On Client-1, nslookup “search”, observe the results of the CNAME record
 
![image](https://github.com/user-attachments/assets/74727f38-0d83-4b5a-aa4d-f8decfa3e16b)

The order of operations go from Local DNS Cache > Local Host File > DNS server.
