# cr_proxy_pass
a web browser based on chromium to work with nginx proxy_pass to access resources behind firewall

## Feature
1. VPN-free
2. Web resource access auditable
3. PPcode

## Google Play
[![Get it on Google Play][2]][1]

  [1]: https://play.google.com/store/apps/details?id=com.github.wuruxu.cr_proxy_pass
  [2]: https://developer.android.com/images/brand/en_generic_rgb_wo_60.png

## 1.PP Setting
![PP Setting](/pp_settings.png)

## 2. PPcode
PPcode is a string split by ";" and startsWith "ppcode:" such as
```
ppcode:*;https://mynginx.org/cr_proxy/;u0007
```
![PPcode copy](/ppcode_copy.png)
User can share the PPcode to other friends    
PP Web Browser will detect PPcode from clipboard when startup

## 3. Config nginx backend
```
        location /cr_proxy {
            gzip on;
            proxy_pass_request_headers on;
            proxy_ssl_server_name on;
            proxy_ssl_name $proxy_host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_buffering on;
            proxy_redirect off;
            proxy_pass $http_ppurl;
        }
```
## 4. How to test your nginx config
```
curl -v -H "ppurl:https://gg.yourcompany.com/test_url" https://mynginx.org/cr_proxy/
```
If curl get the response from  "https://gg.yourcompany.com/test_url",  all is okay
