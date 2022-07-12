FROM python:3.8-bullseye

ENV TZ=Asia/Shanghai
WORKDIR /app

# install proj's dependencies
RUN apt update && \
    apt install -y libgeos-dev wget cmake sqlite3 curl && \
    apt-get install -y libcurl4-openssl-dev

# install proj 8.0.0
RUN wget https://download.osgeo.org/proj/proj-8.0.0.tar.gz && \
    tar -xf proj-8.0.0.tar.gz && cd proj-8.0.0 && \
    mkdir build && cd build && \
    cmake .. && \
    cmake --build . && \
    cmake --build . --target install && \
    ctest && \
    cp ./bin/* /bin && \
    cd .. && rm -rf /app/proj-8.0.0 /app/proj-8.0.0.tar.gz

# install cartopy==0.20.0
RUN pip install --upgrade pip wheel setuptools && \
    pip install --upgrade pyshp && pip install shapely --no-binary shapely && \
    pip install cartopy==0.20.0 && \
    rm -rf $(pip cache dir)

CMD ["bash"]