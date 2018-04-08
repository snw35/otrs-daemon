FROM alpine:3.7

RUN apk --no-cache --update add \
    perl \
    perl-dbi \
    perl-archive-zip \
    perl-crypt-eksblowfish \
    perl-crypt-ssleay \
    perl-date-format \
    perl-datetime \
    perl-dbi \
    perl-dbd-mysql \
    perl-dbd-pg \
    perl-encode-hanextra \
    perl-io-socket-ssl \
    perl-json \
    perl-lwp-useragent-determined \
    perl-mail-imapclient \
    perl-net-dns \
    perl-ldap \
    perl-template-toolkit \
    perl-xml-libxml \
    perl-xml-libxslt \
    perl-xml-parser \
    perl-yaml-libyaml \
    perl-text-csv_xs \
    mini-sendmail

RUN adduser -u 5000 -S otrs \
    && echo '*/5 * * * * /opt/otrs/bin/otrs.Daemon.pl start' > /etc/crontabs/otrs \
    && chmod 0600 /etc/crontabs/otrs

CMD ["crond", "-f"]
