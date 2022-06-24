# 1) Copy Static web site in /var/www/ directory

like directory name is `abobakar.me`

# 2) go to /etc/nginx/sites-available 
 create a file name like `abobakar.me` \
 ```
 sudo touch abobakar.me
 ```
 open file in text editer
 ```
 sudo vim abobakar.me
 ```
 OR 
 ```
 sudo nano abobakar.me
 ```
 write some configuration code in this file
 ```
server {
       listen 80;
       listen [::]:80;

       server_name abobakar.me;

       root /var/www/abobakar.me;
       index index.html;

      location / {
               try_files $uri $uri/ =404;
      }
}

 ```
 `server_name` is a domain name \
 `root` contain the static file location

# 3 now create soft link in /etc/nginx/sites-enabled 

create soft link
```
sudo ln -s /etc/nginx/sites-available/abobakar.me /etc/nginx/sites-enabled/
```
# 4 Check nginx service
```
sudo nginx -t
```
# 5 Restart nginx service
```
  sudo systemctl restart nginx
  ```
  OR 
  ```
  sudo service nginx restart
  ```
  # Now your site available for every one