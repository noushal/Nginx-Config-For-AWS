# Domain-Purchase-and-Config-for-Hostinger

## 1. Create an Account in Hostinger
   - Create an account using - https://auth.hostinger.com/login
   - go to **Gmail** and verify your Hostinger account
## 2. Purchasing an Domain
   - In the **Find your domain** there is an input box, search for your desired domain ex. example.com
   - **NB**: if you need domain in low price take domain with **.tech** and apply the coupon code **GRABDOMAIN**
## 3. Config Domain
   - After completing payment click on the **Domains** then click on **Domain portfolio**
   - Select your domain and Then in the left side click on **DNS / Nameservers**
   - fill out the input boxes there that are below
     
     Type = A

     Name = site-name (replace **site-name** with your website name)

     Points to = 0.0.0.0 (Your Instance ip address from AWS)

     **NB**: You can only get the ip of instance after the 2nd step

   - Then Click **Add Record**

   - If you want to add **www** as DNS to your domain then replace **site-name** with **www.site-name**
