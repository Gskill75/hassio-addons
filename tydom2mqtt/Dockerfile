FROM python:3.11-alpine3.22

# tydom2mqtt release built from https://github.com/Gskill75/tydom2mqtt
ARG TYDOM2MQTT_REF=3.7.0-gskill75.3

LABEL org.opencontainers.image.description="Deltadore Tydom to MQTT Bridge"

WORKDIR /app

RUN wget -qO- "https://github.com/Gskill75/tydom2mqtt/archive/refs/tags/${TYDOM2MQTT_REF}.tar.gz" \
    | tar -xz -C /tmp \
    && cp -r "/tmp/tydom2mqtt-${TYDOM2MQTT_REF}/app/." /app/ \
    && rm -rf "/tmp/tydom2mqtt-${TYDOM2MQTT_REF}" \
    && pip3 install --no-cache-dir -r requirements.txt

EXPOSE 8080

HEALTHCHECK --interval=30s --timeout=10s --start-period=60s --retries=3 \
    CMD python /app/healthcheck.py

CMD [ "python", "-u", "main.py" ]
