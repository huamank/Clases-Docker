# usa imagen de python
FROM python:3.9-slim

# Crea directorio de trabajo
WORKDIR /app

COPY requirements.txt ./

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]

