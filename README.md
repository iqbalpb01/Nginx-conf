# Nginx-conf

server {
        root /var/www/html;
        index index.php;
        server_name kochi.dev;

        location / {
               try_files $uri $uri/ /index.php$is_args$args;
        }

        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
        }

        location ~ /\.ht {
                deny all;
        }

    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/kochi.dev/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/kochi.dev/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

}
server {
    if ($host = kochi.dev) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


        listen 80;
        server_name kochi.dev;
    return 404; # managed by Certbot


}

