---
layout: post
title: Traffic Analysis and Privacy Assessment of Android Applications
date: 2024-10-15
categories: [Project, AI]
tags: [project, privacy, application, cybersecurity, network, compliance-assessment, cookie, data-security]
---


# Traffic Analysis and Privacy Assessment of Android Applications


## Objective
This project involved analyzing network traffic and assessing privacy practices of Android applications using **mitmproxy** (mitmweb) to capture and inspect network communications. The goal was to identify privacy concerns and evaluate tracking behaviors in Android apps, specifically assessing how user data is transmitted and identifying any security weaknesses.

### Skills Demonstrated
- **Network Traffic Analysis**: Captured and analyzed HTTP/S traffic from Android apps to understand data flow and identify sensitive information leaks.
- **Privacy and Compliance Assessment**: Evaluated app data handling against privacy policies, detecting any inconsistencies or transparency gaps.
- **Session and Cookie Analysis**: Investigated session handling and cookie attributes to understand session management and data tracking practices.
- **Location Data Security**: Assessed apps' permissions and examined the exposure of precise location data, raising potential privacy risks.
- **Tool Proficiency in mitmproxy and HTTP/S Packet Inspection**: Used `mitmweb` to inspect and document HTTP/S requests for detailed analysis of app traffic.

### Tools Used
<div>
    <img src="https://img.shields.io/badge/-mitmproxy-4CAF50?style=for-the-badge&logo=mitmproxy&logoColor=white" />
    <img src="https://img.shields.io/badge/-Python-3776AB?style=for-the-badge&logo=Python&logoColor=white" />
    <img src="https://img.shields.io/badge/-Android%20Emulator-3DDC84?style=for-the-badge&logo=Android&logoColor=white" />
    <img src="https://img.shields.io/badge/-Chrome-4285F4?style=for-the-badge&logo=GoogleChrome&logoColor=white" />
</div>


## Steps

### Part 1: Setting Up mitmproxy
1. **Install and Configure mitmproxy**: Installed `mitmproxy` and set up network routing on an Android emulator to capture traffic.
2. **Configuration on Android Emulator**: Configured the emulator’s proxy settings to route through `mitmproxy`, enabling interception of app traffic.

<img width="452" alt="image" src="https://github.com/user-attachments/assets/19a1faac-f478-4125-9727-14b6a5dc970d">

Figure 1: Traffic filtered for HTTP requests to http://admin.appnext.com/configuration.aspx.

### Part 2: Traffic Analysis on **YogaForDiabeties**
1. **Identified Sensitive Data**: Captured HTTP requests to detect sensitive data, including `id`, `adsid`, and device identifiers sent to `appnext.com`.
2. **Cookie Inspection**: Examined session cookies, such as `ASP.NET_SessionId`, to determine if cookies persisted beyond sessions, which could impact user privacy.
3. **IMEI Exposure**: Detected the app transmitting the device’s IMEI to `airpush.com`, a significant privacy concern as this identifier uniquely links to the user’s device.
4. **Ad Tracking Flags**: Analyzed the `adOpt` flag, identifying whether the app opted in or out of ad tracking.

<img width="452" alt="image" src="https://github.com/user-attachments/assets/bc8ba044-d028-4bae-8e25-eca93a7c6f98">

Figure 2: Filtered traffic showing POST requests from YogaForDiabities.

#### Part 3: Traffic Analysis on **MobInCube**
1. **Location Data Collection**: Captured precise latitude and longitude data being sent to `stats.mobincube.com` along with carrier and device model information.
2. **Policy Compliance Check**: Compared the app’s privacy policy against captured traffic data, noting missing disclosures on specific data practices.

<img width="452" alt="image" src="https://github.com/user-attachments/assets/e82a398b-6bf7-4174-8dd4-4aaf40009f37">

Figure 3: HTTP request showing the phone model and carrier name for MobInCube.


## Conclusion
This project provided hands-on experience in using **mitmproxy** to assess network security and data privacy for Android applications. By analyzing traffic, I identified sensitive information being transmitted without adequate user control, highlighting potential privacy risks. This project exemplifies skills crucial for a SOC Analyst role, such as network traffic analysis, session management, and privacy compliance assessment, contributing to a secure user experience.

