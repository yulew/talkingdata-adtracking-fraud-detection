# Kaggle Competition -- talkingdata-adtracking-fraud-detection 
（https://www.kaggle.com/c/talkingdata-adtracking-fraud-detection）

Forecasting whether a user will download the mobile phone application after the user clicks on this APP's advertisement (AD). A user may fraudulently click on an AD but won't download the APP, and that causes the AD's client to lose extra money. Accordingly, a black list can be created to block these fraudulent clicking users. 



## Insights of the Datasets

Features have been preprocessed. Now available features include the **IP** of a user who commits a click on an AD, which **APP**'s advertisement this user clicks, the cellphone **device** type ID (e.g., iphone 6 plus, iphone 7, huawei mate 7, etc.), the operating system (**OS**) of the phone, the **channel** ID of mobile ad publisher and the **click_time** which means when the user clicks on the AD. 

The target value is **is_attributed**, which mean if the user download the APP after he or she clicks on the AD, the value is 1, otherwise is 0. If a user's is_attributed is 1, the **download_time** is also provided as extra information.

<!--- IP: Which region or country a user is located is relevant to whether he or she fraudulently clicks on the AD. 
(a). Fraud user can clicks on a same AD for many times but using same IP. 
(b). However, a family or people in the same company can share a same IP, which means a same ip can contain regular user and fraud user. 
BY group by Device, OS, channel etc can further differentiate that. 
APP: (Can be used group by IP) app id for marketing 
Device: device type id of user mobile phone (e.g., iphone 6 plus, iphone 7, huawei mate 7, etc.) 
OS: (Can be used group by IP) os version id of user mobile phone 
Channel: channel id of mobile ad publisher 
click_time: 
(a). A regular user and a fraud user varys in terms of when they click on AD.
(b). Durations of click_time of a same IP can make a prediction. attributed_time:
is_attributed: Target Value -->


