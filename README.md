
**[error] 86013#86013:** *213 upstream timed out (110: Connection timed out) while reading response header from upstream, client: 1.2.3.4, server: demo.com, request: "POST /api/v2/get?forData=true HTTP/1.1", upstream: "fastcgi://unix:/var/run/php/php7.4-fpm.sock", host: "demo.com"

### You may receive a response such as this when running Nginx and php-fpm after a fixed amount of time (default = 60s).

## Connection timed out

You can change the time Nginx waits for the FastCGI backend, by changing the fastcgi_read_timeout parameter in the general nginx.conf.
```
http {
    ...
    fastcgi_read_timeout 600s;
    proxy_read_timeout 360000;
    proxy_connect_timeout 60000s;
    proxy_send_timeout 3000;
    send_timeout 3000;    
    ...
}
```
## Connection reset by peer

With these errors, it may be any of the following PHP parameters in the php.ini that is causing the PHP process to end abruptly, thus causing Nginx to get a “reset” from its peer (in this case, the php-fpm backend).

```
;;;;;;;;;;;;;;;;;;;
; Resource Limits ;
;;;;;;;;;;;;;;;;;;;

max_execution_time = 12000
max_input_time = 12000
memory_limit = 8192M      
```

[LINK]: https://ma.ttias.be/nginx-and-php-fpm-upstream-timed-out-failed-110-connection-timed-out-or-reset-by-peer-while-reading/

[LINK]: https://talk.plesk.com/threads/upstream-timed-out-110-connection-timed-out-while-reading-response-header-from-upstream.367272/
