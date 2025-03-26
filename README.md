# phishingcampaign
Phishing Campaign using GoPhish

Watch GoPhish Demo:

https://drive.google.com/file/d/18czLunTIWuOTnMvzPk47J5c_Xwx03ZVw/view?usp=sharing


Tools / Technologies needed:

VPS (Virtual Private Server) of your choice. Digital Ocean will be used for this guide. 


SMTP Relay of your choice. Mailgun will be used for this guide.

Setting up VPS and installing GoPhish:
Go through the sign-up process for the VPS of your choice. Once done, launch your VPS Console. 

Run the following commands in this order:
apt install wget
apt install unzip
wget https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip
unzip gophish-v0.12.1-linux-64bit.zip
nano config.json

Configure the json file to this:

![Screenshot 2025-03-26 at 1 36 57 PM](https://github.com/user-attachments/assets/c5c8e524-9383-4b80-ad20-5b357976c8c2)




chmod +x gophish (permits file to be executable)
./gophish 

It will then run this:

gophish@gophish.dev:~/src/github.com/gophish/gophish$ ./gophish
 time="2020-06-30T08:04:33-05:00" level=warning msg="No contact address has been configured."
 time="2020-06-30T08:04:33-05:00" level=warning msg="Please consider adding a contact_address entry in your config.json"
 time="2020-06-30T08:04:33-05:00" level=info msg="Please login with the username admin and the password 1178f855283d03d3"
 time="2020-06-30T08:04:33-05:00" level=info msg="Starting phishing server at http://0.0.0.0:80"
 time="2020-06-30T08:04:33-05:00" level=info msg="Starting IMAP monitor manager"
 time="2020-06-30T08:04:33-05:00" level=info msg="Starting admin server at https://127.0.0.1:3333"
 time="2020-06-30T08:04:33-05:00" level=info msg="Background Worker Started Successfully - Waiting for Campaigns"
 time="2020-06-30T08:04:33-05:00" level=info msg="Starting new IMAP monitor for user admin"

Login using admin and the password that gets generated for you. 


![Screenshot 2025-03-26 at 1 37 29 PM](https://github.com/user-attachments/assets/49952f6a-460a-4b7d-855c-447a8f968deb)

















Once you log in, create as many user accounts as you want under “User Management”. 

******IF YOU DO NOT WISH TO SPOOF YOU CAN STOP HERE AND START SENDING PHISHING EMAILS FROM YOUR EMAIL, ALTHOUGH THIS WILL NOT GIVE YOU THE REAL WORLD SCENARIO********

USE THE FOLLOWING SENDER PROFILE SETTINGS:

*****IF YOU WISH TO SPOOF PROCEED WITH THE GUIDE********

Use this source for landing pages and email templates:
https://github.com/FreeZeroDays/GoPhish-Templates

Feel Free to create your own. 



FOR THE PASSWORD YOU WILL NEED TO CREATE AN “APP PASSWORD” WITHIN YOUR GMAIL. TO DO THIS FOLLOW THESE STEPS:
GMAIL > MANAGE YOUR GOOGLE ACCOUNT > SEARCH “APP PASSWORDS” > CREATE APP NAME > NAME IT GOPHISH > COPY THE GENERATED APP PASSWORD 

—----------------------------------------------------------------------------------------------------------------------------------------

How to Spoof with GoPhish:

When using GoPhish, you'll need to set up a sending domain to send emails from. This domain will appear in the "From" address of your phishing emails and should look as realistic as possible to improve the success of your simulation.

In real-world phishing attacks, bad actors often create domains that closely mimic trusted organizations to trick users. To simulate this effectively, we recommend following naming conventions that resemble legitimate communication channels.

Here are some examples you can model your domain after:

@mail.alerts.org
@security.alerts.net
@notifications.security-alert.com

Using domains like these makes your simulations more authentic and helps train users to recognize subtle signs of phishing. Domains like these help make your simulations more authentic and train users to catch subtle red flags.

You can register domains through services like Namecheap, Google Domains, or GoDaddy.

Choose a domain name that fits your use case and aligns with your campaign goals.
After buying your domain, you’ll need to configure DNS records to verify it and send emails successfully. This usually includes setting A, CNAME, and MX records. Proper setup ensures your GoPhish campaigns are both deliverable and realistic.
A Record - Points your domain to your VPS
CNAME - Directs domain to another domain (your SMTP relay service)
MX - Tells the internet where to deliver emails. 
TXT - Used for email security and authentication (SPF, DMARC, DKIM)
If you're using a third-party service like Mailgun to send emails, they’ll provide the exact DNS records you need to add. These usually include CNAME and TXT records for domain verification and email authentication. Mailgun handles the sending infrastructure, which means you won’t need to manually configure an SMTP server on your own. Once records are added to your domain you can verify on your mail relay service. It is important to note that this is specific to Mailgun and we are unsure whether other third party SMTP relay services will provide this automatically or it needs to be set up manually.If so, we recommend leveraging Google / chatGPT to accomplish this part. 
Once this is set up you can send a test email via GoPhish under “Sending Profiles”

The password is set up under “SMTP Credentials” within your SMTP Relay Service.

![Screenshot 2025-03-26 at 1 37 48 PM](https://github.com/user-attachments/assets/9a538b73-38f7-4dc4-85f1-4e4ec24f1a73)


Email Templates:

Use the following resource for email templates: 

https://github.com/FreeZeroDays/GoPhish-Templates or leverage chatGPT to achieve your desired template. 

Navigate to Landing pages and click +new page then fill out the form like the example below. 
Copy and Paste your HTML code. 
We recommend capturing submitted data and passwords. You can also add a “redirect to” once the user is done entering their credentials. 


![Screenshot 2025-03-26 at 1 39 15 PM](https://github.com/user-attachments/assets/6853dca3-74a6-4de9-9ca5-512d8ddcb1a4)



Email Templates:

Navigate to Email Templates and click +New Template. Fill out the form like the example below:

The Envelope Sender and the SMTP From need to match. We used noreply@micrsoftsecurity.com (spoofed email) 

Paste your HTML Code. Again we recommend using a combination of this https://github.com/FreeZeroDays/GoPhish-Templates with chatGPT to achieve your phishing campaign goals. 


![Screenshot 2025-03-26 at 1 39 23 PM](https://github.com/user-attachments/assets/89a31e17-3f2c-4433-8d0f-f93f112b3a23)


Users And Groups:

To create a new group, navigate to Users and Groups and click + New Group. Enter a name for the group, then add each user by providing their name, email, and position. Click + Add after entering each user. Once all users have been added, click Save Changes. Your group is now ready to be used in campaigns.


![Screenshot 2025-03-26 at 1 39 30 PM](https://github.com/user-attachments/assets/f4e03b5c-0b02-4147-bb41-1e750184a1eb)



Campaigns:

Navigate to Campaigns. Click on +New Campaigns.Create a Name, choose an Email Template, choose a Landing Page. For URL use your VPS IP Address. Modify launch date to your liking. Choose desired Sending Profile and Groups.  Launch Campaign!!!!


![Uploading Screenshot 2025-03-26 at 1.39.41 PM.png…]()


Demo:

https://drive.google.com/file/d/18czLunTIWuOTnMvzPk47J5c_Xwx03ZVw/view?usp=sharing
