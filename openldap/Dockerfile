FROM centos:7

ARG CONF_PATH

RUN yum install -y wget libtool-ltdl libtool-ltdl-devel cyrus-sasl-devel \
	&& yum group install -y "Development Tools"

# install ldap
RUN cd ~ && wget ftp://ftp.openldap.org/pub/OpenLDAP/openldap-release/openldap-2.4.46.tgz \
	&& tar xfz openldap-2.4.46.tgz \
	&& cd openldap-2.4.46 \
	&& ./configure --prefix=/usr/local/openldap --with-cyrus-sasl --enable-ldap=yes --enable-cleartext --enable-rewrite --enable-syslog --enable-modules --with-tls --enable-overlays --enable-bdb=no --enable-hdb=no \
	&& make depend \
	&& make \
	&& make install


# set config
COPY ./${CONF_PATH}/slapd.conf /usr/local/openldap/etc/openldap/slapd.conf
COPY ./${CONF_PATH}/ldap.conf /usr/local/openldap/etc/openldap/ldap.conf
COPY ./${CONF_PATH}/init.ldif ~/init.ldif

RUN mkdir /var/openldap-data && /usr/local/openldap/libexec/slapd -h "ldap:///"

ARG LDAP_USER
ARG LDAP_PASS

RUN /usr/local/openldap/bin/ldapadd -x -D "${LDAP_USER}" -w ${LDAP_PASS} -f init.ldif