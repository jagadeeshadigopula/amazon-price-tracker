# amazon-price-tracker
Import requests from bs4 
import BeautifulSoup 
import smtplib 
import time frommail = ‘@gmail.com’
passwd = ‘dbxnbknpiqbsosoi’ 
tomail = ‘@hotmail.com’ URL = ‘https://www.amazon.com/Apple-MacBook-13-inch-Storage-Keyboard/dp/B0881ZF6WP/ref=sr_1_1?dchild=1&amp;keywords=mac+pro&amp;sr=8-
1’
headers = {“User-Agent”: ‘Mozilla/5.0 (Macintosh; Intel Mac OS X 9.10; rv:69.0) Gecko/20100101Firefox/68.0’}
def analyze_price(): app = requests.get(URL,headers=headers) scrapper = BeautifulSoup(app.content, ‘html.parser’)
print(scrapper.prettify())
title =scrapper.find(id=”productTitle”).get_text() price =
scrapper.find(id=”priceblock_ourprice”).get_text() 
StrToFloat_price =float(price[1:6].replace(‘,’ , ‘.’)) 
if(StrToFloat_price &lt; 1.600):
send_notification()
print(StrToFloat_price)
print(title.strip()) def send_notification(): server = smtplib.SMTP(‘smtp.gmail.com’, 587)
server.ehlo() server.starttls() server.ehlo() server.login(frommail, passwd) subject = ‘Low price found!’
body = ‘Here is the Amazon item link: \n\n’ + URL msg = ‘Subject: {}\n\n{}’.format(subject, body)
server.sendmail(frommail, tomail, msg) print(‘Notification has been sent successfully’) server.quit()
while True: analyze_price() time.sleep(60*60*24)
