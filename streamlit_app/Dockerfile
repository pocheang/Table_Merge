FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    gcc \
    python3 \
    python3-pip \
    python3-setuptools \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && pip3 install --no-cache-dir --upgrade pip \
    && useradd --no-log-init --system --create-home appuser

WORKDIR /app

COPY requirements.txt /app/
COPY app_v0.1.py /app/
COPY merge /app/merge/
COPY path /app/path/
COPY .streamlit /app/.streamlit/

RUN pip3 install --no-cache-dir -r requirements.txt \
    && chown -R appuser:appuser /app

USER appuser

EXPOSE 8501

ENTRYPOINT ["streamlit", "run"]

CMD ["app_v0.1.py", "--server.address=0.0.0.0"]