FROM jupyter/pyspark-notebook:spark-3.0.1

USER root

# Install cron
RUN apt-get update && apt-get install -y cron

# Copy the cron jobs file
COPY crontab /etc/cron.d/spark-cron

# Give execution rights on the cron job
RUN chmod 0644 /etc/cron.d/spark-cron

# Apply cron job
RUN crontab /etc/cron.d/spark-cron

# Create the log file to be able to run tail
RUN touch /var/log/cron.log

# Copy the scripts
COPY work /home/jovyan/work

# Install kafka-python
RUN pip install kafka-python

# Start cron and then start the main process
CMD cron && tail -f /var/log/cron.log
