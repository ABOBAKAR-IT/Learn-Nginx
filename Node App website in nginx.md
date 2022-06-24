# 1) go to /etc/nginx/sites-available 
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
server  

{ 
        listen   80; 
        server_name node.abobakar.me; 
 
        location /{ 
              #  proxy_set_header X-Real-IP $remote_addr; 
              #  proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for; 
              #  proxy_set_header Host $host; 
              #  proxy_set_header X-NginX-Proxy true; 
                proxy_pass http://localhost:5000/; 
              #  proxy_redirect http://localhost:5000/ https://$server_name/; 
        } 
}

 ```


# 2 now create soft link in /etc/nginx/sites-enabled 

create soft link
```
sudo ln -s /etc/nginx/sites-available/abobakar.me /etc/nginx/sites-enabled/
```
# 3 Check nginx service
```
sudo nginx -t
```
# 4 Restart nginx service
```
  sudo systemctl restart nginx
  ```
  OR 
  ```
  sudo service nginx restart
  ```
  # Now your site available for every one