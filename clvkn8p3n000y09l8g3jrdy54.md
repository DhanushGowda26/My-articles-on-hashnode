---
title: "Nginx Fundmentals"
seoTitle: "Nginx Configuration"
seoDescription: "Nginx is a versatile web server that offers various capabilities beyond being a reverse proxy, such as load balancing, SSL/TLS termination, and caching."
datePublished: Mon Apr 29 2024 07:34:18 GMT+0000 (Coordinated Universal Time)
cuid: clvkn8p3n000y09l8g3jrdy54
slug: nginx-fundmentals
tags: web-servers, devops, nginx-configuration-guide

---

Nginx is a versatile web server that offers various capabilities beyond being a reverse proxy, such as load balancing, SSL/TLS termination, and caching. It can serve as an API gateway, providing advanced routing, filtering, and security features. Nginx supports content compression, media streaming, and WebSockets proxying, making it suitable for a wide range of applications. Additionally, Nginx can act as a content delivery network (CDN) and a web application firewall (WAF), helping optimize performance and enhance security for web applications and services. Its flexibility and performance make it a popular choice for many use cases.

### Nginx Conf

```nginx
http {                      # this is called as context
    include mime.types;     # this is directive
    server {                # child context under parent http context
        listen 80;          # need to mention on which port you need to listen
        server_name ip/domain; # specify server where application is running
        root /path/to/project/folder; # specify project folder in server 
}
}
```

here, whatever under /var/www/demo will be served, by default it picks only index.html

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714198034048/23e42c06-3cdb-4c45-b394-90ca3530a65e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714198062655/325fcfce-efd3-4781-96eb-4b868bb244b7.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714198147647/b419ac02-9781-4caa-a931-bc294f1ffda3.png align="center")

```nginx
http {                      
    include mime.types;    
    server {                
        listen 80;          
        server_name ip/domain; 
        root /var/www/demo; 

        location /new {                   #prefix match
          return 200 "hi i am from new";  # 200 is response code
         }
        
        location = /new {                   #exact match
          return 200 "hi i am from new exact match";
         }       
        location ~* /new[0-9] {                   #REGX match
          return 200 "hi i am from new REGX match";
          }
         location ^~ /New {                   #prefential prefix match
          return 200 "hi i am from new prefential prefix match";
          }
        location  /fruits {                   #here it will look for fruits folder under /var/www/demo/ and will serve index.html
          root /var/www/demo/
          }
        location  /veg {                   #here it will server index.html of fruits folder if path is veg
          alias /var/www/demo/fruits
          }
         location /crops {
                root /var/www/demo;
                try_files /crops/crops.html /index/html =404; #by default it will server index.html to server other, use try_files
                                                              #if crops.html not present it will server /var/www/demo/index.html
                                                                # if index.html not present it will give 404 error
        }

}
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714198856789/652ee5cf-eda5-4be2-b5e8-2e315a5d5659.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714198871496/b7ef525e-a149-42aa-a8a8-2f41ad31ac4d.png align="center")

Prefix match will load its content anything that starts with "new"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714199496852/c53d75bf-4409-45b5-89aa-b1b5ddc3e32c.png align="center")

here, the url is [http://54.226.209.32/new1234/random](http://54.226.209.32/new1234/random) but it stll provides response as it matches "new"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714200599720/9b88495b-7a25-4a17-b409-5e908c08665a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714200646518/d345593f-1dd2-4004-95e8-06101b06c5ee.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714200672290/1a7d2f42-77fb-4b53-9f50-830e2479747a.png align="center")

here we get error, when the path is apart from "new" unlike in prefix match

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714201017629/6cb72ac0-e209-4f57-af59-69815b3d93ff.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714201157309/9373f59c-7610-4efc-834a-3e7884417a03.png align="center")

here the only condition is "new" followed by any number.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714204430207/87a58a25-c39e-40f2-9ecc-d1e70d569e79.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714204453559/9ac09927-1210-484d-8172-9b27d3649fee.png align="center")

Exact match &gt; Prefential prefix &gt; REGX match &gt; Prefix match is the order of priority

here, Prefential prefix is same as Prefix match but it has got higher priority over REGX match.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714203891161/f2ae431f-2f74-48be-b6a5-58b9bc18db0d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714203908918/1ac9bd0d-a415-49d4-8958-c1792bb03a10.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714206024404/4883db9e-7204-489a-91f1-f1913007597f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714206064466/4625497d-8865-46f9-9810-0c7dde702632.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714211927347/71c45f62-beef-4fdc-9c20-49ea17a43588.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714211952159/459fad33-735c-4d88-abe4-bb5f0bb754a1.png align="center")

simillar to alias there is rewrite, but they have diffrent purpose and operate at diffrent levels within nginx conf.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714213895320/b3c1b323-21d1-47dd-8e99-61a783aecc45.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714213916436/3bad0089-aef7-4ca3-9ca6-97de9c3888cf.png align="center")

### Load Balancer

```nginx
events {
    # Event settings can go here if needed
}

http {
    # Include mime types for content type determination
    include mime.types;

    # Define the upstream group (backend servers) for load balancing
    upstream backendserver {
        server 54.226.209.32:1111;  # Docker container running on port 1111
        server 54.226.209.32:4444;  # Docker container running on port 4444
    }

    # Define the server block
    server {
        listen 80;  # Listen on port 80
        server_name 54.226.209.32;  # Replace with your server IP or domain
     location / {
           # Handle requests for load balancing
            proxy_pass http://backendserver;
            proxy_set_header Host $host;      # Set the host header
            proxy_set_header X-Real-IP $remote_addr;  # Forward the client's IP address
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
    }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714216071446/b1ff037f-966e-4ff4-9edc-eb557a629445.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714219590321/28ac5a5d-d52f-4c38-98db-9b9b6c8274b9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714219609510/7c7718d3-3355-4a97-9288-317954e562d2.png align="center")

**Thank you**