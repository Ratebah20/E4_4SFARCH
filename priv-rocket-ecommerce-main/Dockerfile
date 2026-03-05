FROM python:3.11-slim

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN apt-get update && apt-get install -y \
    ca-certificates curl gnupg nodejs npm \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY requirements.txt .
RUN pip install --upgrade pip && pip install --no-cache-dir -r requirements.txt

COPY . .

RUN npm i && npm run build
RUN python manage.py collectstatic --no-input

CMD ["gunicorn", "--config", "gunicorn-cfg.py", "core.wsgi"]