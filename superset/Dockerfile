FROM apache/superset
RUN pip install psycopg2-binary
RUN superset fab create-admin \
    --username admin \
    --firstname Superset \
    --lastname Admin \
    --email admin@superset.com \
    --password admin
RUN superset db upgrade
RUN superset init
COPY exports /exports
ARG DB_STRING
RUN superset set-database-uri -d speed_test -u $DB_STRING
RUN superset import-dashboards -p /exports/dashboard_export_20220927T184233.zip
CMD superset run -h 0.0.0.0 -p 8088 --with-threads --reload --debugger
