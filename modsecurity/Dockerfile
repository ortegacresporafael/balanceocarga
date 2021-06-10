FROM nginx:latest


RUN apt-get update && apt-get install -y apt-utils autoconf automake build-essential git libcurl4-openssl-dev libgeoip-dev liblmdb-dev libpcre++-dev libtool libxml2-dev libyajl-dev pkgconf wget zlib1g-dev
    
    RUN git clone --depth 1 -b v3/master --single-branch https://github.com/SpiderLabs/ModSecurity \
    && cd ModSecurity \
    && git submodule init \
    && git submodule update \
    && ./build.sh \
    && ./configure \
    && make \
    && make install \
    && cd ..
    RUN git clone --depth 1 https://github.com/SpiderLabs/ModSecurity-nginx.git
    RUN wget http://nginx.org/download/nginx-1.21.0.tar.gz \
    && tar zxvf nginx-1.21.0.tar.gz \
    && cd nginx-1.21.0 \
    && ./configure --with-compat --add-dynamic-module=../ModSecurity-nginx \
    && make modules \
    && cp objs/ngx_http_modsecurity_module.so /etc/nginx/modules \
    && cd .. \
    && mkdir /etc/nginx/modsec
    RUN wget -P /etc/nginx/modsec/ https://raw.githubusercontent.com/SpiderLabs/ModSecurity/v3/master/modsecurity.conf-recommended
    RUN mv /etc/nginx/modsec/modsecurity.conf-recommended /etc/nginx/modsec/modsecurity.conf
    RUN cp ModSecurity/unicode.mapping /etc/nginx/modsec
    RUN sed -i 's/SecRuleEngine DetectionOnly/SecRuleEngine On/' /etc/nginx/modsec/modsecurity.conf
   
    

    
    
