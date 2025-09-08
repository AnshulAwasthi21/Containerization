FROM ubuntu

WORKDIR /app

COPY /requirements.txt /app/
COPY /devops /app/

RUN apt-get update && apt-get install -y python3 python3-pip python3-venv

# Create a virtual environment 
RUN python3 -m venv /opt/venv

# Make sure we use virtual env's python and pip
ENV PATH="/opt/venv/bin:$PATH"

# Install dependencies inside the virtual environment
RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 8000

CMD ["python3", "manage.py", "runserver", "0.0.0.0:8000"]