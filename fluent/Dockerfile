FROM fluent/fluentd:stable-onbuild
MAINTAINER h-mineta <h-mineta@0nyx.net>

WORKDIR /fluent

USER root

RUN set -x \
    && apk upgrade --update \
    && apk add \
        bash \
    && apk add --virtual .build-deps \
        build-base \
        ruby-dev \
	&& echo 'gem: --no-document' >> ~/.gemrc \
    && fluent-gem install \
        fluent-plugin-forest \
        fluent-plugin-elasticsearch \
        fluent-plugin-multiprocess \
        fluent-plugin-snmptrap \
	&& cd / \
	&& apk del --purge .build-deps \
    && fluent-gem sources --clear-all \
	&& rm -rf /tmp/* \
	&& rm -rf /var/cache/apk/*

EXPOSE 24224 162
CMD fluentd -c /fluentd/etc/fluent.conf
