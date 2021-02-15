# talkingdata-adtracking-fraud-detection 
https://www.kaggle.com/c/talkingdata-adtracking-fraud-detection
(In this Kaggle competition, we won bronze metal, ranking in the top 8%.) 

The competition aims at forecasting whether a user will download the mobile phone application (APP) after this user clicks on an advertisement (AD) of the APP. A user may repeatedly click on an AD but will never download the APP, which causes the AD's client to lose extra money. Accordingly, the long-term goal is to create a blacklist that will block these fraudulent users.
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
We can create features via grouping by features IP, device and OS and count frequencies:<br>
(a). freq_IP_device_OS: per group of IP-device-OS, (i) what is the total clicks, (ii) what is the total downloads, (iii) what is the ratio of downloads to all clicks. To be more specific: <br>
(i)   ip-device-os-clicks :         After grouping IP-device-OS, the click frequencies of the corresponding group <br>
(ii)  ip-device-os-downloads:       After grouping IP-device-OS, the total downloads of the corresponding group  <br>
(iii) ip-device-os-downloads-ratio: After grouping IP-device-OS, the ratio of the clicks that result in downloading to all clicks of the corresponding group <br>

(b). Convert the "yyyy-mm-dd hh:mm:ss" to "hour" (e.g. 2017-11-06 16:37:01 --> **16**), then we shall engineer features such as: <br>
(i)   hour-clicks:          on a specific hour (such as hour 16), the total clicks that all occur on that hour, <br>
(ii)  hour-downloads:	      on a specific hour,                   the total clicks that all occur on that hour and they download the APP afterwards, <br>
(iii) hour-downloads-ratio: on a specific hour,                   the ratio of the clicks that result in downloading to all clicks. <br>

These three new created features better represent timestamp feature. After that, the features "click_time", "attributed_time" ("yyyy-mm-dd hh:mm:ss") and "hour" can be removed if we later put them in the random forests or gradient boost to train. 

## XGBoost
### What is XGBoost?
A random forest or a gradient boosting is a set of decision trees. XGBoost is an implementation of gradient boosted decision trees that are widely used in Kaggle competitions due to its good speed and performance. <br>
A decision tree relies on finding a splitting point on each feature but can cause overfitting. A random forest or a gradient boosting can reduce the overfitting by introducing many decision trees.

### Engineering Features
When simply performing a regression method, like XGBoost, the original features IP, APP, device, OS and channel are almost meaningless categorical features. Therefore, we must convert these features to more meaningful representations. The previous section discusses how some new features can be created.

IP, APP, device, OS, channel, click_time can be converted to: <br>
**ip-device-os-clicks, ip-device-os-downloads, ip-device-os-downloads-ratio, app-clicks, app-downloads, app-ratio, channel-clicks, channel-downloads, channel-ratio, hour-clicks, hour-downloads and hour-downloads-ratio**.

### XGBoost Technique Issues:
After theses features are created, we splitted the new engineered training data over 100 parts and saved it into storage with 17.3 GB. 
Depending on the RAM of your machine, you can load them all at once or iteratively load them.

adtrackingfraud-xgboost.ipynb describes a program that loads each bit of training data and feeds them into XGBoost and trains them one by one. Parameters can be tuned by Grid Search or Random Search. To see which set of parameters is better, we shall just train a small set of data and check the cross-valiation results. Once a set of parameters is confirmed, then we can train all data.


