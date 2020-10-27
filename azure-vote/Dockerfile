FROM tiangolo/uwsgi-nginx-flask:python3.8
RUN pip install redis
RUN pip install opentelemetry-api
RUN pip install opentelemetry-sdk
RUN pip install opentelemetry-exporter-otlp
RUN pip install opentelemetry-instrumentation
RUN pip install opentelemetry-instrumentation-flask
RUN pip install opentelemetry-instrumentation-redis
ADD /azure-vote /app
