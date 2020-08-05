 
FROM mysql:5

ARG USER_ID
ARG GROUP_ID

RUN if [ ${USER_ID:-0} -ne 0 ] && [ ${GROUP_ID:-0} -ne 0 ]; then \
    userdel -f mysql &&\
    if getent group mysql ; then groupdel mysql; fi && \
    groupadd -g ${GROUP_ID} mysql && \
    useradd -l -u ${USER_ID} -g mysql mysql && \
    install -d -m 0755 -o mysql -g mysql /home/mysql && \
    chown --changes --silent --no-dereference --recursive \
          --from=999:999 ${USER_ID}:${GROUP_ID} \
        /home/mysql \
        /var/lib/mysql \
    ;fi

USER mysql