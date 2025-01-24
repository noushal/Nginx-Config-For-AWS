# NGINX-Configuration-For-AWS

## 1. Create Free AWS Account
Create free AWS Account at https://aws.amazon.com/

## 2. Buy Domain From Hostinger (if you didnt have one)

[Hostinger Guide](./Hostinger.md/)

## 2. Create and Lauch an EC2 instance

1. **Navigate to EC2**:
   - Click on the **Instances**, Then click **Launch Instance**.

2. **Fill Out All**:
   - Give a name for the **Instance**.
   - In **Application and OS Images** Click on **Ubuntu**.
   - Click on **Create new key pair** and give a name for it, Then click **Create key pair**.
   - Now in the **Network settings**, Check the boxes **Allow SSH traffic from**, **Allow HTTPS traffic from the internet** and **Allow HTTP traffic from the internet**.
   - In the **Configure storage** Increase the value from 8 to 30 and click **Launch Instance**.

## 3. Connect to the Instance

1. **Get the Public IPv4 DNS**
   - Click on the **Instance** you created.
   - Copy the **Public IPv4 DNS**.

1. **In Windows**
   - Open CMD(Command Prompt) by searching or by the shortcut key **Windows Key + K** Then Click **K**.
   - Now Type the commands Below.
   ```
   cd Downloads (Navigate to the folder where your SSH key is downloaded)

   ssh -i "example.pem" ubuntu@Your-Public-IPv4-DNS (change the example.pem to your own pem file name and change the ip to your ip that you have copied earlier)
   ```

2. **In Linux**
   - Open Terminal by the shortcut key **Ctrl + Alt + T**.
   - Now Type the commands Below.
   ```
   cd Downloads (Navigate to the folder where your SSH key is downloaded)

   ssh -i "example.pem" ubuntu@Your-Public-IPv4-DNS (change the example.pem to your own pem file name and change the ip to your ip that you have copied earlier)
   ```

3. **In Mac**
   - Open Spotlight by the shortcut key **Command + Space** Then Search for terminal then click **Enter**.
   - Now Type the commands Below.
   ```
   cd Downloads (Navigate to the folder where your SSH key is downloaded)

   ssh -i "example.pem" ubuntu@Your-Public-IPv4-DNS (change the example.pem to your own pem file name and change the ip to your ip that you have copied earlier)
   ```


## 4. Install Node and NPM
```
sudo apt update

sudo apt install curl

curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -

sudo apt install -y nodejs

node -v (Can be used to check if the Node is installed properly)

```

## 5. Clone your project from Github
```
git clone https://github.com/<github-username>/<your-repository-name>.git

cd your-repository-name

npm install

#If you have an env file then type this and add the content in the env file here
nano .env
```

## 6. Install dependencies
```
sudo npm i pm2 -g
pm2 start index.js (Put your main js file name)

# Other pm2 commands
pm2 show app
pm2 status
pm2 restart app
pm2 stop app
pm2 logs (Show logs)
pm2 flush (Clear logs)

# To make sure app starts when reboot
pm2 startup ubuntu
```

## 7. Setup Firewall
```
sudo ufw enable
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https

# Other Firewall Commands
sudo ufw status (for getting the current status of firewall)
```

## 8. Install NGINX and configure
```
sudo apt install nginx

sudo nano /etc/nginx/sites-available/default
```
Not recommended to edit the default file you can create dedicated file for your site configuration(eg: mysite) 
Add the following to the location part of the server block
```
server {
    server_name yourdomain.com www.yourdomain.com;

    location / {
        proxy_pass http://localhost:3000; #whatever port your app runs on
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```
```
#make a symbolic copy of the config file
sudo ln /etc/nginx/sites-available/your-file-name /etc/nginx/sites-enabled

# Check NGINX config
sudo nginx -t

# Restart NGINX
sudo nginx -s reload
```

## 9. Add SSL with LetsEncrypt
```
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install python3-certbot-nginx
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com

# Only valid for 90 days, run this after 90 days to renew the SSL certificate
certbot renew --dry-run
```
