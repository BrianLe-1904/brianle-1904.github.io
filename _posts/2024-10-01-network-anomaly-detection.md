---
layout: post
title: Network Anomaly Detection Using Entropy for Attack Diagnostics
date: 2024-10-01
categories: [Project, AI]
tags: [project, attack, privacy, application, cybersecurity, network, compliance-assessment, cookie, data-security]
---

# Network Anomaly Detection Using Entropy for Attack Diagnostics

This task involved the analysis of a server-log dataset, which included information about two attacks that occurred between 8:00 am and noon on the same day. The goal was to identify the precise date and time of these attacks, along with the methodology used by the threat actors to conduct these malicious activities. In addition, two articles discussed the use of entropy estimation and similarity detection to help identify anomalies from the attacks.


### Tools Used

- **Pandas (Python Library)**: Used for data loading, manipulation, and preprocessing to analyze server log data.
- **Entropy Calculation Scripts**: Scripts applied to measure entropy levels in network traffic, identifying deviations from normal traffic patterns to detect potential attacks.
- **Matplotlib and Seaborn**: Visualization tools employed to graphically represent traffic patterns, aiding in the detection of irregularities during attack periods.

### Skills Learned

- **Data Analysis and Preprocessing**: Developed proficiency in cleaning and preparing datasets, including merging date and time fields, creating calculated fields, and filtering logs for specific time windows.
- **Entropy-Based Anomaly Detection**: Applied entropy as a detection metric, contrasting baseline traffic entropy with anomaly periods to identify suspicious activity, an essential skill for network security monitoring.
- **Attack Analysis and Threat Hunting**: Gained experience in identifying attack patterns, such as DDoS and flooding attacks, by isolating high-volume requests from specific IPs and analyzing unusual traffic patterns.
- **Visualization and Diagramming**: Enhanced ability to use diagrams to represent SOC components and workflows, an essential skill for documenting and communicating the overall system structure.


## Steps

### DATA ANALYSIS AND PREPROCESSING
The analysis process started by loading the dataset from the server-log.txt file using the Pandas library. The file revealed crucial features or attributes of a server log capturing traffic during the time two attacks occurred: Start-Date, Start-Time, Duration, Service, Source-Port, Destination-Port, Source-IP, and Distination-IP. The target features in this dataset were ‘Service’, ‘Source-IP’, and ‘Distination-IP’. Initially, the dataset was preprocessed by merging and converting ‘Start-Date’ and ‘Start-Time’ to a datetime format, along with extracting ‘Hour’, ‘Minute’, and ‘Second’ for filtration and analysis. Additionally, the feature ‘Duration’ was also processed into a ‘Duration-secs’ column by extracting the last two digits as seconds.

![img-description](https://github.com/user-attachments/assets/78ea2334-e27c-4dcb-b3e8-3127df090296)
_Data reprocessing code_


### ATTACK ANALYSIS
As two attacks were reported to have occurred sometime between 8:00 am and noon on the same day, the server log during this time was extracted and saved as the attacks_df DataFrame for further analysis of the attacks or any potential anomalies. The timestamp of the attacks was indicated by the ‘Start-Time’ column in the format YYYY-MM-DD HH:MM:SS, which allowed us to identify the precise date and time of the attacks.

![img-description](https://github.com/user-attachments/assets/f7d78ef4-a8c1-44ab-b271-c972731bb5eb)
_ Server-log filtration code according to the attack period._

After isolating the server logs that contained the attacks, the target features including ‘Service’, ‘Source-IP’, and ‘Distination-IP’ were carefully considered to identify any unusual values, such as suspicious services from the ‘Service’ column. Then, any suspicious activities from source and destination IP addresses were investigated. First, we combined the ‘Source-IP’ and ‘Distination-IP’ columns to form an ‘IP-Pair’ column, which indicated the traffic between IP addresses, along with the occurrence time of this traffic. As the traffic varied, only the IP pairs that appeared more often than the threshold value were captured, and the threshold value could be adjusted if needed to precisely identify the attacks.

![img-description](https://github.com/user-attachments/assets/6b3c9a2f-4111-411f-90de-ea872bcd92d2)
_Suspicious Activities Detection code._

![img-description](https://github.com/user-attachments/assets/d74aade7-aba8-41d5-92a7-85384191930b)
![img-description](https://github.com/user-attachments/assets/909e05a1-81b4-495a-bc13-ab4531a1edd2)
![img-description](https://github.com/user-attachments/assets/52eb5357-865b-42b2-b537-6bcdb3bd4cf4)
_Output of Suspicious Activities Detection code._

### ATTACK DETECTION AND RESULT
From the collected output, we can identify that the attack methodology conducted by the threat actor was a Flooding attack, which involved sending a large number of HTTP requests from a single source IP to different target IPs on port 80 with a duration of 01 sec, likely aiming to overwhelm the web servers or exploit vulnerabilities in the web applications running on those servers. This could have been a distributed denial-of-service (DDoS) attack or an attempt to find and exploit web application vulnerabilities. From the results above, there were 2 dominant source IPs, which were 172.016.113.084 and 172.016.117.111, that sent enormous requests to different target IPs starting at 2014-06-03 08:17:02 and 2014-06-03 08:50:31, respectively. Therefore, the precise date and time of the attacks are:

**Attack 1**: 03/06/2014 at 08:17:02

**Attack 2**: 03/06/2014 at 08:50:31

In the context of the two attacks identified in the dataset, the difference in entropy between normal and abnormal network traffic could serve as a powerful tool in detecting anomalies stemming from these attacks. The following code demonstrates an example of using entropy to help detect anomalies from network traffic. In this example, we assume that the baseline entropy for normal network traffic is 3.5 with a threshold of 0.5. By calculating the current entropy of suspicious networks as found from the previous section and comparing it with the baseline entropy, we could identify whether or not there are anomalies revealed during the attacks.

![img-description](https://github.com/user-attachments/assets/b2970236-34b1-4dae-90a7-e523d62a1268)
_Example of using Entropy for Anomaly Detection code._

### CONCLUSION
In conclusion, the analysis of the server log has successfully identified two attacks carried out on the same day. The methodology used by the attackers was a Flooding attack, where a large number of HTTP requests were sent from single source IPs to different target IPs, possibly with the intent to overwhelm the servers or exploit vulnerabilities in the web applications they were running. The precise date and time of these attacks were also determined. Furthermore, the use of entropy, as suggested by existing literature, proved to be a potent tool in identifying anomalies in network traffic. In the future, this method could be utilized to detect and prevent similar attacks, thereby enhancing the security of our network systems.