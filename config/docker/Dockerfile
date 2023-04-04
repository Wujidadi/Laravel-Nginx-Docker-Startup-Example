FROM wujidadi/nginx-php:2.4

ARG user=user

RUN touch /root/.zsh_history;\
    touch /home/${user}/.zsh_history && chown ${user}:${user} /home/${user}/.zsh_history;\
    apt-get update && apt-get upgrade -y;\
    apt-get upgrade -y nodejs;\
    npm install -g npm;\
    apt-get autoremove -y;\
    apt-get clean;\
    rm -rf /var/lib/apt/lists/*

CMD ["/bin/bash", "-c", "cron start; supervisord -c /etc/supervisor/conf.d/supervisord.conf; nginx -g 'daemon off"]
