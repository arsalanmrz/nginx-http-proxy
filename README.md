### nginx-http-proxy

#### Commands (for instance : ubuntu os)
- first update your os's packages : `sudo apt update`
- install nginx on your server : `sudo apt install nginx`
- enable nginx service : `sudo systemctl enable nginx`
- start nginx service : `sudo systemctl start nginx`
- try this command : `sudo nano /etc/nginx/sites-available/test.conf` (like test.conf that I put it down for you)
- for save above file and exit the nano editor : press---> `ctrl+o` , `ctrl+m` , `ctrl+x`
- after that you should add this `test.conf` to your sites-enable nginx directory , so try this command : 
      `sudo ln -s /etc/nginx/sites-available/test.conf /etc/nginx/sites-enabled/`
- after all you should restart the nginx : `sudo systemctl restart nginx`
- finally , if you put `proxy.mirbozorgi.com` in your browser , you can see the facebook's home.
- If you wanna have https (https://proxy.mirbozorgi.com):
    - `sudo apt update`
    - `sudo snap install core; sudo snap refresh core`
    - `sudo snap install --classic certbot`
    - `sudo ln -s /snap/bin/certbot /usr/bin/certbot`
    - `sudo certbot --nginx` (it will aks you some question , answer them with your personal data.)
    - `sudo certbot renew --dry-run` (cerbot is free and  your https will expire within 3 months,  with this,you run the automate cron for renew the SSL/TLS)

-  `https://proxy.mirbozorgi.com` is now available



#### Sample for test.conf
``` js
server {
    server_name  proxy.mirbozorgi.com;
    listen      80;


    access_log /var/log/nginx/proxy_mirbozorgi_com_access.log;
    error_log /var/log/nginx/proxy_mirbozorgi_com_error.log;

    location / {
        proxy_pass       https://facebook.com;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
   }



```