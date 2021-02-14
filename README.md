# talkingdata-adtracking-fraud-detection 
https://www.kaggle.com/c/talkingdata-adtracking-fraud-detection
(In this Kaggle competition, we won the bronze metal, ranking top 8%) 

The competition aims at forecasting whether a user will download the mobile phone application after the user clicks on an advertisement (AD). A user may repeatedly click on an AD but will never download the APP, which causes the AD's client to lose extra money. Accordingly, the long-term goal is to create a blacklist that will block these fraudulent users.
The goal of the competition is quite simple though:  a user with the following features, predicting whether a user will download the APP.


## Insights of the Datasets

### Features

Features have been preprocessed in this Kaggle competition. The preprocessed features include:   

Target feature:  
**is_attributed**: If the user indeed downloads the APP after he or she clicks on the AD, the value is 1, otherwise is 0. 

Input features:  
**IP**: IP of a user who clicks on an AD,   
**APP**: APP ID for marketing purpose,   
**device**: the mobile phone device type ID (e.g., iphone 6 plus, iphone 7, huawei mate 7, etc.),   
**OS**: the operating system ID of the phone,   
**channel**: the channel ID of mobile ad publisher,  
**click_time**: the UTC time when the user clicks on the AD,   
**attributed_time**: If a user indeed downloads the APP, the timestamp when he or she downloads the APP, otherwise null.


<!--- IP: Which region or country a user is located is relevant to whether he or she fraudulently clicks on the AD. 
(a). Fraud user can clicks on a same AD for many times but using same IP. 
(b). However, a family or people in the same company can share a same IP, which means a same ip can contain regular user and fraud user. 
BY group by Device, OS, channel etc can further differentiate that. 
APP: (Can be used group by IP) app id for marketing 
Device: device type id of user mobile phone (e.g., iphone 6 plus, iphone 7, huawei mate 7, etc.) 
OS: (Can be used group by IP) os version id of user mobile phone 
Channel: channel id of mobile ad publisher 
click_time: 
(a). A regular user and a fraud user varies in terms of when they click on AD.
(b). Durations of click_time of a same IP can make a prediction. attributed_time:
is_attributed: Target Value -->

### Insights

1. A user's IP address will usually not change. However, many different Internet users may share the same IP. <!--- These users may --> For example, many different devices may use an external IP address for a company or a public shared network; also, 2G mobile phone network providers cannot provide unique IPs for individuals. As such, the same IP does not necessarily mean the same person. Additional information, such as "device" and "OS" can further differentiate different users.  
<!--- Therefore, "IP" can be group by with "device" and "OS" -->

2. A fraudulent user will repeatedly click on the AD many times. At such, collecting information of frequency of a user can help forecast whether this user is a fraudulent user.

In conclusions:  
We can create features through grouping by features IP, device and OS and count frequencies:
(a). freq_IP_device_OS
(b). 
