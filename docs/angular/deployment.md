---
title: Angular Deployment
tags:
  - Angular
  - Deployment
---

## Simple Deployment

1. Build the application

    ```node
    ng build
    ```

2. Copy the `/dist` folder to the server

3. Configure the server to redirect requests for missing files to index.html.

    * Nginx
    Add `try_files` in the config
    ```
    server {
        listen 80;
        server_name angular.zhaobg.com;
        root /xxx/xxx/; # angular dist

        location / {
            try_files $uri $uri/ /index.html;
        }
    }
    ```