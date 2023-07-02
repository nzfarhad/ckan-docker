FROM ckan/ckan-base:2.10.1
#FROM ckan/ckan-base:2.9.9

# Copy i18n files to CKAN Image
COPY setup/ckan.mo /srv/app/src/ckan/ckan/i18n/en_GB/LC_MESSAGES/ckan.mo
COPY setup/ckan.po /srv/app/src/ckan/ckan/i18n/en_GB/LC_MESSAGES/ckan.po
COPY setup/en_GB.js /srv/app/src/ckan/ckan/public/base/i18n/en_GB.js

# Set up environment variables
ENV APP_DIR=/srv/app
ENV TZ=UTC
RUN echo ${TZ} > /etc/timezone

# Make sure both files are not exactly the same
RUN if ! [ /usr/share/zoneinfo/${TZ} -ef /etc/localtime ]; then \
        cp /usr/share/zoneinfo/${TZ} /etc/localtime ;\
    fi ;

# Install arttheme
RUN  pip3 install -e git+https://github.com/nzfarhad/ckanext-atrtheme.git#egg=ckanext-atrtheme