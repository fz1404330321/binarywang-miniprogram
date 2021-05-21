# binarywang-miniprogram
微信相关

# maven镜像
   <mirror>
        <id>alimaven</id>
        <mirrorOf>central</mirrorOf>
        <name>aliyun maven</name>
        <url>http://maven.aliyun.com/nexus/content/repositories/central/</url>
      </mirror>
      
      <mirror>  
      <id>alimaven</id>  
      <name>aliyun maven</name>  
      <url>https://maven.aliyun.com/repository/public/</url>  
      <mirrorOf>central</mirrorOf>          
    </mirror>
    <mirror>
      <id>repo2</id>
      <mirrorOf>central</mirrorOf>
      <name>Human Readable Name for this Mirror.</name>
      <url>http://repo2.maven.org/maven2/</url>
    </mirror>
    <mirror>
      <id>ui</id>
      <mirrorOf>central</mirrorOf>
      <name>Human Readable Name for this Mirror.</name>
      <url>http://uk.maven.org/maven2/</url>
    </mirror>


# nginx配置

server {
        server_name *.soleasyenergy.com;
        listen 80;
        rewrite ^ https://$http_host$request_uri? permanent;
}

server {
        listen       443;
        server_name ~^(?<subdomain>.+).soleasyenergy.com$;
        root         /usr/share/nginx/html/$subdomain/;
        ssl on;
        ssl_certificate 1_soleasyenergy.com_bundle.crt;
        ssl_certificate_key 2_soleasyenergy.com.key;
        ssl_session_cache shared:SSL:1m;
        ssl_session_timeout  10m;
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:HIGH:!aNULL:!MD5:!RC4:!DHE;
        ssl_prefer_server_ciphers on;
    
        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
            try_files $uri $uri/ /index.html;
        }

        error_page 404 /404.html;
            location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
}
