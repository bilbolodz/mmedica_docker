FROM postgres:9.5.4

ENV LC_ALL pl_PL.CP1250
ENV LANG pl_PL.CP1250
ENV TZ 'Europe/Warsaw'

RUN apt-get update && apt-get install -y unzip tzdata && echo $TZ > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata && \
    apt-get clean

RUN echo "pl_PL.CP1250 CP1250" >> /etc/locale.gen && echo "pl_PL.UTF-8 UTF-8" >> /etc/locale.gen && \
    echo "LANGUAGE=pl_PL.CP1250" >> /etc/default/locale && \
	echo "LC_ALL=pl_PL.CP1250" >> /etc/default/locale && \
	locale-gen && dpkg-reconfigure --frontend=noninteractive locales && update-locale LANG=pl_PL.CP1250

COPY timezone.tgz /timezone.tgz
COPY PostgreSQL-9.5-Linux.zip /tmp

COPY docker-entrypoint.sh /docker-entrypoint.sh

RUN chmod 775 docker-entrypoint.sh && ln -s /usr/share/postgresql/9.5 /usr/lib/postgresql/9.5/share && unzip /tmp/PostgreSQL-9.5-Linux.zip -d /tmp/ && rm /tmp/PostgreSQL-9.5-Linux.zip && \
	mv /tmp/libpq.so.5.8 /usr/lib/x86_64-linux-gnu && mv /tmp/libpqwalreceiver.so /usr/lib/postgresql/9.5/lib && rm /usr/lib/x86_64-linux-gnu/libpq.so.5 && \
	ln -s /usr/lib/x86_64-linux-gnu/libpq.so.5.8 libpq.so.5 && ldconfig && mv -f /tmp/postgres.bki /usr/share/postgresql/9.5/postgres.bki && chmod 755 /tmp/* && \
	mv -f /tmp/initdb /usr/lib/postgresql/9.5/bin/initdb && mv -f /tmp/pg_ctl /usr/lib/postgresql/9.5/bin/pg_ctl && mv -f /tmp/pg_dump /usr/lib/postgresql/9.5/bin/pg_dump && \
	mv -f /tmp/pg_restore /usr/lib/postgresql/9.5/bin/pg_restore && mv -f /tmp/postgres /usr/lib/postgresql/9.5/bin/postgres && tar xf /timezone.tgz -C /usr/lib/postgresql/9.5/share/ && rm /timezone.tgz
