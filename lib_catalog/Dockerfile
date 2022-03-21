FROM python:alpine3.15
WORKDIR /app
COPY requirements.txt .
RUN apk add --update --no-cache curl g++ gcc libxslt-dev && pip install -r requirements.txt
COPY . .
ENTRYPOINT ["/app/app.sh"]

