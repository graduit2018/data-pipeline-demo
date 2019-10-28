FROM sgrio/java:jdk_8_ubuntu

RUN apt-get update && \
    apt-get install -y zip wget nano supervisor python3-pip && \
    apt-get -y clean && \
    rm -rf /var/lib/apt/lists/*

RUN wget https://archive.apache.org/dist/spark/spark-2.4.3/spark-2.4.3-bin-hadoop2.7.tgz && \
    tar -xzf spark-2.4.3-bin-hadoop2.7.tgz && \
    mv spark-2.4.3-bin-hadoop2.7 /spark && \
    rm spark-2.4.3-bin-hadoop2.7.tgz && \
    wget -P /spark/jars/ https://repo1.maven.org/maven2/org/apache/spark/spark-streaming-kafka-0-8-assembly_2.11/2.4.3/spark-streaming-kafka-0-8-assembly_2.11-2.4.3.jar

RUN pip3 --no-cache-dir install jupyterlab && \
    pip3 --no-cache-dir install pyspark && \
    pip3 --no-cache-dir install redis

ENV SPARK_HOME=/spark \
    PYSPARK_PYTHON=/usr/bin/python3

COPY start-master.sh start-worker.sh /
COPY jupyter_notebook_config.py /root/.jupyter/
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
