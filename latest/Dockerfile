FROM ubuntu
USER root

RUN apt-get update && apt-get install -y git && \
    git clone https://github.com/grizmin/rtorrent-rutorrent-shared.git a && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y rtorrent unzip unrar mediainfo git curl php-fpm php-cli php-geoip php-mbstring php-zip nginx wget ffmpeg supervisor \
    php-xml libarchive-zip-perl libjson-perl libxml-libxml-perl irssi sox python3-pip python2 sudo && \
    pip install cloudscraper && \ 
    rm -rf /var/lib/apt/lists/* && \
    cp ./a/rutorrent-*.nginx /root/ && \
    mkdir -p /var/www && cd /var/www && \
    git clone https://github.com/Novik/ruTorrent.git rutorrent && \
    rm -rf ./rutorrent/.git* && cd / && \
    cp ./a/config.php /var/www/rutorrent/conf/ && \
    cp ./a/startup-rtorrent.sh ./a/startup-nginx.sh ./a/startup-php.sh ./a/startup-irssi.sh ./a/.rtorrent.rc /root/ && \
    cp ./a/supervisord.conf /etc/supervisor/conf.d/ && \
    sed -i 's/\/var\/log/\/downloads\/\.log/g' /etc/nginx/nginx.conf && \
    echo "rutorrent ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    echo "rtorrent user:";  sudo su - rtorrent && \
    mkdir -p ~/bin ~/.local && \
    git clone "https://github.com/pyroscope/pyrocore.git" ~/.local/pyroscope && \
    ~/.local/pyroscope/update-to-head.sh && \
    PATH=$PATH:/home/rtorrent/bin && \
    pyroadmin --version && \
    echo "HORRAY!"


EXPOSE 83 446 50515 5000
VOLUME /downloads

CMD ["supervisord"]
