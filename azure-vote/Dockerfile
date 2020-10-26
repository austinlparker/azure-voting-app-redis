FROM tiangolo/uwsgi-nginx-flask:python3.6
RUN pip install redis
RUN pip install opentelemetry-api
RUN pip install opentelemetry-launcher
RUN pip install opentelemetry-instrumentation
RUN pip install opentelemetry-instrumentation-wsgi
RUN pip install opentelemetry-instrumentation-redis
ADD /azure-vote /app
