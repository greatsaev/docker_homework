FROM python:alpine3.15 as builder
WORKDIR /usr/app
RUN python -m venv /usr/app/venv
ENV PATH="/usr/app/venv/bin:$PATH"
COPY requirements.txt .
RUN apk add --update --no-cache curl g++ gcc libxslt-dev && pip install -r requirements.txt

FROM python:alpine3.15
RUN apk add --update --no-cache curl
RUN addgroup --system app && adduser -S -G app app
WORKDIR /usr/app
COPY --from=builder /usr/app/venv ./venv
COPY . .
USER app
ENV PATH="/usr/app/venv/bin:$PATH"
ENTRYPOINT ["/usr/app/app.sh"]
HEALTHCHECK --interval=60s --timeout=30s --start-period=15s --retries=3 CMD curl --fail http://localhost:8000/api/v1/lib/author/ || exit 1

