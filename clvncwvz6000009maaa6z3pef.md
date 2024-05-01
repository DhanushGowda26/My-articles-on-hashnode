---
title: "Nginx Fundmentals"
seoTitle: "Nginx Fundmentals"
datePublished: Wed May 01 2024 05:08:30 GMT+0000 (Coordinated Universal Time)
cuid: clvncwvz6000009maaa6z3pef
slug: nginx-fundmentals-1
tags: server, nodejs, devops, load-balancing

---

### Variables

```nginx
events {
    # Event settings can go here if needed
}

http {
    # Include mime types for content type determination
    include mime.types;
    # Define the server block
    server {
        listen 80;  # Listen on port 80
        server_name 54.226.209.32;  # Replace with your server IP or domain
        # Serve static files directly from /var/www/demo/
        location /inspect {
          return 200 "$host\n$uri\n$args"; 
        }
    }
}
```

$host gives the ip adress

$uri is path or uniform resource identifier

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714277349994/a98ae39b-cb9c-4083-9c5e-6db80d1daa4d.png align="center")

here $args is not present as we have not queried

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714277415641/e1633791-5961-4363-956d-8829ede8365f.png align="center")

so now after queried even $args is displayed

```nginx
events {
    # Event settings can go here if needed
}

http {
    # Include mime types for content type determination
    include mime.types;
    # Define the server block
    server {
        listen 80;  # Listen on port 80
        server_name 54.226.209.32;  # Replace with your server IP or domain
        # Serve static files directly from /var/www/demo/
        location /inspect {
          return 200 "City : $arg_city"; 
        }
    }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714277832237/e2d03461-0943-45ab-be49-81acd5e6bd96.png align="center")

here,in http://54.226.209.32/inspect?<mark>city</mark>\=Bengaluru should match with $arg\_<mark>city</mark>

```nginx
events {
    # Event settings can go here if needed
}

http {
    # Include mime types for content type determination
    include mime.types;
    # Define the server block
    server {
        listen 80;  # Listen on port 80
        server_name 54.226.209.32;  # Replace with your server IP or domain

        if ( $arg_server != "nginx" ) {
          return 401 "incorrect API key";
          }
    }
 }
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714280059216/f52598db-cf61-4686-95d2-b142289ddd6d.png align="center")

Here, the variable is not case sensitive, but the variable value is.

```nginx
events {
    # Event settings can go here if needed
}

http {
    # Include mime types for content type determination
    include mime.types;
    # Define the server block
    server {
        listen 80;  # Listen on port 80
        server_name 54.226.209.32;  # Replace with your server IP or domain

        set $weekend "No";

        if ( $date_local ~* "Saturday|Sunday" ) {
                set $weekend "Yes";
                }
        location /weekend {
          return 200 $weekend;
        }
    }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714280907302/6fc088a0-326e-4908-8337-b4957b29afe6.png align="center")

### Rewrites and Redirects

```nginx
events {
    # Event settings can go here if needed
}

http {
    # Include mime types for content type determination
    include mime.types;
    # Define the server block
    server {
        listen 80;  # Listen on port 80
        server_name 54.226.209.32;  # Replace with your server IP or domain
        root /var/www/demo;    
    }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714281453646/0186a8c2-d999-4ccf-863e-f65e0b9e5c87.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714281507427/8320a920-5889-4724-8441-20d54444fc48.png align="center")

Nginx is directly serving the requested file based on the `root` directive specified in the `server` block.

http://54.226.209.32/UbuntuCoF.svg this gave the above output but if in case I need same output for http://54.226.209.32/logo

```nginx
events {
    # Event settings can go here if needed
}

http {
    # Include mime types for content type determination
    include mime.types;
    # Define the server block
    server {
        listen 80;  # Listen on port 80
        server_name 54.226.209.32;  # Replace with your server IP or domain
        root /var/www/demo;
        location /logo {
          return 307 /UbuntuCoF.svg;
        }
    }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714282921734/9faca293-a40b-4809-8feb-9c4c938c9069.png align="center")

here http://54.226.209.32/logo is redirected to http://54.226.209.32/UbuntuCoF.svg\\

here we are <mark>redirecting</mark> but <mark>rewrites mutate the URI internally</mark>.

Replace the 307 status code with 200 to address any questions on your mind and enhance your learning process.

```nginx
events {
    # Event settings can go here if needed
}
http {
    # Include mime types for content type determination
    include mime.types;

    # Define the server block
    server {
        listen 80;  # Listen on port 80
        server_name 54.226.209.32;  # Replace with your server IP or domain
        root /var/www/demo;
        rewrite ^/user/\w+ /greet;
        # Handle requests to /greet
        location /greet {
            return 200 "hello welcome";
        }
    }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714284536666/05e0fe6d-7522-434c-9d93-55003dcff992.png align="center")

here we are rewriting, means nginx will internally rewrite http://54.226.209.32/user/ram this to http://54.226.209.32/greet

```nginx
events {
}
http {
    # Include mime types for content type determination
    include mime.types;

    # Define the server block
    server {
        listen 80;  # Listen on port 80
        server_name 54.226.209.32;  # Replace with your server IP or domain

        # Root directory for static HTML files
        root /var/www/demo;

        rewrite ^/user/(\w+) /greet/$1;

        # Handle requests to /greet
        location /greet {
            # Return a response including the captured value from the rewrite
            return 200 "hello welcome";
        }
        location = /greet/ram {
                return 200 "hello ram";
        }
    }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714288236287/1e4ef4ce-6f69-4ea7-90e6-b9fbe4a77113.png align="center")

```nginx
events {
}
http {
    # Include mime types for content type determination
    include mime.types;

    # Define the server block
    server {
        listen 80;  # Listen on port 80
        server_name 54.226.209.32;  # Replace with your server IP or domain

        # Root directory for static HTML files
        root /var/www/demo;
  
        rewrite ^/user/(\w+) /greet/$1;   
        rewrite ^/greet/ram /UbuntuCoF.svg;

#here, both rewrite coveys same if url is http://54.226.209.32/greet/ram/ but what they serve is diffrent in this case /UbuntuCoF.svg will be served

        # Handle requests to /greet
        location /greet {
            return 200 "hello welcome";
        }
        location = /greet/ram {
                return 200 "hello ram";
        }
    }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714289233393/be617490-40ba-4a7e-843d-3e42b04550ce.png align="center")

So, to serve the first one, which is /greet/$1, you need to use a flag called *last* so that Nginx won't rewrite a second time and it will be skipped.

```nginx
events {
}
http {
    # Include mime types for content type determination
    include mime.types;

    # Define the server block
    server {
        listen 80;  # Listen on port 80
        server_name 54.226.209.32;  # Replace with your server IP or domain

        # Root directory for static HTML files
        root /var/www/demo;
  
        rewrite ^/user/(\w+) /greet/$1 last;   
        rewrite ^/greet/ram /UbuntuCoF.svg;

#here, both rewrite coveys same if url is http://54.226.209.32/greet/ram/ but what they serve is diffrent in this case /UbuntuCoF.svg will be served

        # Handle requests to /greet
        location /greet {
            return 200 "hello welcome";
        }
        location = /greet/ram {
                return 200 "hello ram";
        }
    }
}

```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714289442726/c6c9832d-f9f9-4ceb-9500-a6e9d7342a39.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714289831898/cf249ba9-f0a9-46cd-b761-be9bacbba772.png align="center")

You can comment on why the above output for http://54.226.209.32/user/Ram is different in this case.

### Try Files and Named Locations

```nginx
events {
}
http {
    # Include mime types for content type determination
    include mime.types;

    # Define the server block
    server {
        listen 80;  # Listen on port 80
        server_name 54.226.209.32;  # Replace with your server IP or domain

        # Root directory for static HTML files
        root /var/www/demo;
      try_files /cat.png /greet;
        location /greet {
            return 200 "hello try files!";
        }
      
    }
}
```

Here, it will look for cat.png under /var/www/demo. If not found, it will proceed to the next, which is /greet. This will be rewritten and served. Additionally, the URL path is not compulsory; it will serve regardless of the URL path.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714290732412/769d22f2-da9d-42b7-9e0b-e183543d38a1.png align="center")

here it is fetching /greet even if it is not present under root directory because it is present as location and this happens if it is only the last argument.

```nginx
http {
    # Include mime types for content type determination
    include mime.types;

    # Define the server block
    server {
        listen 80;  # Listen on port 80
        server_name 54.226.209.32;  # Replace with your server IP or domain

        # Root directory for static HTML files
        root /var/www/demo;

        # Handle requests for any URI
        location / {
            # Use try_files to check for the requested URI, then fall back to other URIs
            try_files $uri /cat.png /greet @sorry;
        }

        # Handle requests to @sorry
#@sorry is called as named location
        location @sorry {
            # Return a custom 404 response
            return 404 "sorry could not found";
        }

        # Handle requests to /greet
        location /greet {
            # Return a custom response
            return 200 "hello try files!";
        }
    }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714291651313/4b13f6b5-4be2-489d-abe3-a2f69514f7e9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714291750255/b7724c54-56b9-4df5-8cb6-c3325a0af63a.png align="center")

Even though /greet is listed as a location, it is not being served. The location block is only served if it is the last argument.

**Thank you**