𝐈𝐧𝐬𝐭𝐫𝐮𝐦𝐞𝐧𝐭𝐚𝐭𝐢𝐨𝐧 :

* Instrumentation refers to the process of adding monitoring capabilities to our applications, systems, or services.

* This involves embedding/Writting code or using tools to collect metrics, logs, or traces that provide insights into how the system is performing.

𝐏𝐮𝐫𝐩𝐨𝐬𝐞 𝐨𝐟 𝐈𝐧𝐬𝐭𝐫𝐮𝐦𝐞𝐧𝐭𝐚𝐭𝐢𝐨𝐧:

* 𝑽𝒊𝒔𝒊𝒃𝒊𝒍𝒊𝒕𝒚 : It helps you gain visibility into the internal state of your applications and infrastructure.

* 𝑴𝒆𝒕𝒓𝒊𝒄𝒔 𝑪𝒐𝒍𝒍𝒆𝒄𝒕𝒊𝒐𝒏: By collecting key metrics like CPU usage, memory consumption, request rates, error rates, etc., you can understand the health and performance of your system.

* 𝐓𝐫𝐨𝐮𝐛𝐥𝐞𝐬𝐡𝐨𝐨𝐭𝐢𝐧𝐠 : When something goes wrong, instrumentation allows you to diagnose the issue quickly by providing detailed insights.

𝐓𝐲𝐩𝐞𝐬 𝐨𝐟 𝐌𝐞𝐭𝐫𝐢𝐜𝐬 𝐢𝐧 𝐏𝐫𝐨𝐦𝐞𝐭𝐡𝐞𝐮𝐬 :

1. Counter

2. Gauge

3. Histogram

4. Summary

**Project Objectives :

* 𝐈𝐦𝐩𝐥𝐞𝐦𝐞𝐧𝐭 𝐂𝐮𝐬𝐭𝐨𝐦 𝐌𝐞𝐭𝐫𝐢𝐜𝐬 𝐢𝐧 𝐍𝐨𝐝𝐞.𝐣𝐬 𝐀𝐩𝐩𝐥𝐢𝐜𝐚𝐭𝐢𝐨𝐧: Use the prom-client library to write and expose custom metrics in the Node.js application.

* 𝗦𝗲𝘁 𝗨𝗽 𝗔𝗹𝗲𝗿𝘁𝘀 𝗶𝗻 𝗔𝗹𝗲𝗿𝘁𝗺𝗮𝗻𝗮𝗴𝗲𝗿 : Configure Alertmanager to send email notifications if a container crashes more than two times.

* * 𝐀𝐫𝐜𝐡𝐢𝐭𝐞𝐜𝐭𝐮𝐫𝐞 :
 
    ![image](https://github.com/user-attachments/assets/db9664f7-f00a-46c6-a6a9-c1fa69e41f8c)


𝗦𝘁𝗲𝗽𝘀 :

1. 𝐖𝐫𝐢𝐭𝐞 𝐂𝐮𝐬𝐭𝐨𝐦 𝐌𝐞𝐭𝐫𝐢𝐜𝐬
 
2. 𝐝𝐨𝐜𝐤𝐞𝐫𝐢𝐳𝐞 & 𝐩𝐮𝐬𝐡 𝐢𝐭 𝐭𝐨 𝐭𝐡𝐞 𝐫𝐞𝐠𝐢𝐬𝐭𝐫𝐲

3. 𝐀𝐩𝐩𝐥𝐲 𝐭𝐡𝐞 𝐊𝐮𝐛𝐞𝐫𝐧𝐞𝐭𝐞𝐬 𝐦𝐚𝐧𝐢𝐟𝐞𝐬𝐭
 
4. 𝐓𝐞𝐬𝐭 𝐚𝐥𝐥 𝐭𝐡𝐞 𝐞𝐧𝐝𝐩𝐨𝐢𝐧𝐭𝐬 : Open a browser and get the LoadBalancer DNS name & hit the DNS name with following routes to test the application.

* /healthy

* /serverError

* /notFound

* /logs
  
* /example
  
* /metrics

* /call-service-b

5. 𝐂𝐨𝐧𝐟𝐢𝐠𝐮𝐫𝐞 𝐀𝐥𝐞𝐫𝐭𝐦𝐚𝐧𝐚𝐠𝐞𝐫

6. 𝐓𝐞𝐬𝐭𝐢𝐧𝐠 𝐀𝐥𝐞𝐫𝐭𝐬

Finally, To test the alerting system, manually crash the container more than 2 times to trigger an alert (email notification)

-> To crash the application container, hit the following endpoint

* <<LOAD_BALANCER_DNS_NAME>>/crash

* You should receive an email once the application container has restarted at least 3 times. ✅

![Screenshot 2025-03-22 191816](https://github.com/user-attachments/assets/3f31d62e-72c9-41ce-bf94-38162f8e0ce7)


![Screenshot 2025-03-22 191902](https://github.com/user-attachments/assets/d8db414e-42f9-4a43-b7e8-9487f24bd52d)



![Screenshot 2025-03-22 192006](https://github.com/user-attachments/assets/9339fa52-b505-4f0e-aeb0-e2ac2a60139e)


![Screenshot 2025-03-22 192212](https://github.com/user-attachments/assets/9c53b1f6-3ca3-45f6-b7ad-e4b74398c030)
