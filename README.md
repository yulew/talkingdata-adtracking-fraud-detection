# Kaggle Competition -- talkingdata-adtracking-fraud-detection 
（https://www.kaggle.com/c/talkingdata-adtracking-fraud-detection）

Forcasting whether a user will download the APP after the user clicks on the advertisement. A user can fraudulently clicks on an AD just for making money. A black list can be created to block these users accordingly. 



## Dataset Outlook


Features:

IP: Which region or country a user is located is relevant to whether he or she fraudulently clicks on the AD. 

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

is_attributed: Target Value



