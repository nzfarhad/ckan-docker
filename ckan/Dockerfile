FROM ckan/ckan-base:2.10.3

# Copy i18n files to CKAN Image
COPY setup/ckan.mo /srv/app/src/ckan/ckan/i18n/en_GB/LC_MESSAGES/ckan.mo
COPY setup/ckan.po /srv/app/src/ckan/ckan/i18n/en_GB/LC_MESSAGES/ckan.po
COPY setup/en_GB.js /srv/app/src/ckan/ckan/public/base/i18n/en_GB.js

# Install any extensions needed by your CKAN instance
# See Dockerfile.dev for more details and examples
# Install arttheme
RUN  pip3 install -e git+https://github.com/nzfarhad/ckanext-atrtheme.git#egg=ckanext-atrtheme

### XLoader ###
# RUN pip3 install -e 'git+https://github.com/ckan/ckanext-xloader.git@master#egg=ckanext-xloader' && \ 
#     pip3 install -r ${APP_DIR}/src/ckanext-xloader/requirements.txt && \
#     pip3 install -U requests[security]


### Pages ###
RUN  pip3 install -e git+https://github.com/ckan/ckanext-pages.git#egg=ckanext-pages

#RUN python3 ckan -c /srv/app/ckan.ini jobs worker

# Copy custom initialization scripts
COPY docker-entrypoint.d/* /docker-entrypoint.d/

# Apply any patches needed to CKAN core or any of the built extensions (not the
# runtime mounted ones)
COPY patches ${APP_DIR}/patches

RUN for d in $APP_DIR/patches/*; do \
        if [ -d $d ]; then \
            for f in `ls $d/*.patch | sort -g`; do \
                cd $SRC_DIR/`basename "$d"` && echo "$0: Applying patch $f to $SRC_DIR/`basename $d`"; patch -p1 < "$f" ; \
            done ; \
        fi ; \
    done
