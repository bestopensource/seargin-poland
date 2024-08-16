FROM ubuntu:18.04
 
# Zaktualizuj pakiety i zainstaluj wymagane zależności
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    git \
    curl

WORKDIR /app
 
COPY . /app
 
RUN pip3 install --no-cache-dir -r requirements.txt
 
CMD ["python3", "app.py"]
