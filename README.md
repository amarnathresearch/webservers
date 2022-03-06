# webservers NGINX
@ Copyright aicopia.in

sudo apt update
sudo systemctl status nginx

sudo apt install nginx
sudo systemctl status nginx

cd /etc/nginx/conf.d/

sudo nano amar.local.conf

######################################
server{
	listen 8000 default_server;
	index index.html;
	server_name amar.local;
	root /var/www/amar.local;
}
######################################
sudo nginx -t

cd /var/www/
sudo mkdir amar.local
cd amar.local

sudo nano index.html

######################################
listining to port 8000
######################################

sudo systemctl restart nginx


cd /etc/nginx/conf.d/

sudo nano amar1.local.conf

######################################
server{
	listen 9000 default_server;
	index index.html;
	server_name amar1.local;
	root /var/www/amar1.local;
}
######################################
sudo nginx -t

cd /var/www/
sudo mkdir amar1.local
cd amar1.local

sudo nano index.html

######################################
listining to port 9000
######################################

sudo systemctl restart nginx


cd /etc/nginx/sites-available

sudo cp default default.bak

sudo nano default

############################
# comment all and add the following

upstream backup{
	server public_ip:8000; #change the public_ip
	server public_ip:9000; #change the public_ip
}

server {
	listen 80;
	location / {
		proxy_server http://backup
	}
}
##########################

sudo nginx -t
sudo systemctl restart nginx



