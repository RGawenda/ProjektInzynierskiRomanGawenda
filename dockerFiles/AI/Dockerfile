FROM python:3.9.18-slim-bookworm AS builder 

WORKDIR /app
ENV PATH="/opt/venv/bin:$PATH"
COPY ./AIMineralIdentificationService/requirements.txt .
RUN apt-get update && apt-get upgrade -y &&\
    python -m venv /opt/venv && \
    pip3 install --upgrade pip && \
    pip3 install -r /app/requirements.txt

FROM python:3.9.18-slim-bookworm AS runner

COPY --from=builder /opt/venv /opt/venv
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PATH="/opt/venv/bin:$PATH"

WORKDIR /app
RUN apt-get update && apt-get upgrade -y && \
    addgroup --system py &&\
    adduser --system py --ingroup py
    

COPY ./AIMineralIdentificationService /app
RUN chown -R py:py /app
USER py

CMD [ "python",  "./ImageRecognitionService.py" ]
