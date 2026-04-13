FROM python:3.12-alpine3.20

WORKDIR /app

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

COPY app.py /app/app.py

EXPOSE 8080

USER appuser

CMD ["python", "app.py"]
