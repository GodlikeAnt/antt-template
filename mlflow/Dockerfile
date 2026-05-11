# Minimal MLflow tracking server image.
#
# Why a separate image: the apache/airflow base image is hostile to root
# pip installs (the official guidance is `USER airflow` + `pip --user`),
# so packages installed for the airflow scheduler are not on root's
# PYTHONPATH. The mlflow server needs to read/write the mlruns volume,
# which is simpler when running as root with a clean Python environment.
FROM python:3.11-slim

RUN pip install --no-cache-dir mlflow==2.18.0

EXPOSE 5000

CMD ["mlflow", "server", \
     "--host", "0.0.0.0", \
     "--port", "5000", \
     "--backend-store-uri", "sqlite:////mlruns/mlflow.db", \
     "--default-artifact-root", "/mlruns/artifacts"]
