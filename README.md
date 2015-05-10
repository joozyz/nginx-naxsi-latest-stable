# nginx-naxsi-latest-stable
Latest Nginx Stable Build with Naxsi, Spdy, Pagespeed, SSL and IPv6 enabled

This Version is built for Debian (Wheezy and Jessie)

Built from source..

You need to install following packages:
apt-get install build-essential zlib1g-dev libpcre3 libpcre3-dev unzip automake autoconf libtool pkg-config checkinstall

Create a folder like nginxbuild:

mkdir nginxbuild && cd nginxbuild

Download the required files into it:

wget http://nginx.org/download/nginx-x.x.xx.tar.gz ## Replace nginx-x.x.xx.tar.gz with current stable version
wget http://naxsi.googlecode.com/files/naxsi-x.xx.tar.gz ## Same here just replace the x.xx with the latest version
tar xvzf nginx-x.x.xx.tar.gz
tar xvzf naxsi-x.xx.tar.gz

NPS_VERSION=1.9.32.3 ## current Stable version
wget https://github.com/pagespeed/ngx_pagespeed/archive/release-${NPS_VERSION}-beta.zip
unzip release-${NPS_VERSION}-beta.zip
cd ngx_pagespeed-release-${NPS_VERSION}-beta/
wget https://dl.google.com/dl/page-speed/psol/${NPS_VERSION}.tar.gz
tar -xzvf ${NPS_VERSION}.tar.gz

cd nginx-x.x.xx/
./configure --add-module=../naxsi-core-0.49/naxsi_src/ --add-module=../ngx_pagespeed-release-1.9.32.3-beta/ --prefix=/usr/share/nginx --sbin-path=/usr/sbin/nginx --conf-path=/etc/nginx/nginx.conf --pid-path=/var/run/nginx.pid --lock-path=/var/lock/nginx.lock --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/access.log --user=www-data --group=www-data --with-ipv6 --with-http_ssl_module --with-http_spdy_module --with-http_stub_status_module --with-http_gzip_static_module --with-file-aio --with-openssl=../openssl-1.0.2a
make
make install

Create .Deb Package with "checkinstall"

Thats it! enjoy :)



