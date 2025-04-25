FROM python:3.10-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

WORKDIR /app

COPY . /app

# Upgrade pip
RUN pip install --no-cache-dir --upgrade pip

# Install dependencies one-by-one (isolated installs help prevent hash mismatch issues)
RUN pip install --no-cache-dir torch==2.5.1
RUN pip install --no-cache-dir torchvision==0.20.1
RUN pip install --no-cache-dir numpy==1.26.4
RUN pip install --no-cache-dir pandas==2.2.3
RUN pip install --no-cache-dir Pillow==11.0.0
RUN pip install --no-cache-dir matplotlib==3.9.2
RUN pip install --no-cache-dir plotly==6.0.0
RUN pip install --no-cache-dir scikit-learn==1.6.1
RUN pip install --no-cache-dir tqdm>=4.66.5
RUN pip install --no-cache-dir streamlit==1.43.1

EXPOSE 8501

CMD ["streamlit", "run", "app.py"]
