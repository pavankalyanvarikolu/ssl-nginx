Use ubuntu 20.04
apt update && apt install -y nginx
sudo apt update && sudo apt install certbot python3-certbot-nginx

sudo mkdir -p /var/www/pavanvarikolu.online/html
sudo chown -R $USER:$USER /var/www/pavanvarikolu.online/html
sudo chmod -R 755 /var/www/pavanvarikolu.online
nano /var/www/pavanvarikolu.online/html/index.html
<html>
    <head>
        <title>Welcome to pavanvarikolu.online!</title>
    </head>
    <body>
        <h1>Success! The pavanvarikolu.online server block is working!</h1>
    </body>
</html>

sudo nano /etc/nginx/sites-available/pavanvarikolu.online
server {
        listen 80;
        listen [::]:80;

        root /var/www/pavanvarikolu.online/html;
        index index.html index.htm index.nginx-debian.html;

        server_name pavanvarikolu.online www.pavanvarikolu.online;

        location / {
                try_files $uri $uri/ =404;
        }
}

sudo ln -s /etc/nginx/sites-available/pavanvarikolu.online /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx

sudo certbot certonly \
  --agree-tos \
  --email p.kalyanvarikolu@gmail.com \
  --manual \
  --preferred-challenges=dns \
  -d *.pavanvarikolu.online \
  --server https://acme-v02.api.letsencrypt.org/directory
  
 If we need to get individual ssl certs we can perform following:
 certbot --nginx# ssl-nginx
