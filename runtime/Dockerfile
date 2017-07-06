FROM continuumio/anaconda

RUN cp /etc/apt/sources.list /etc/apt/sources.list.backup

RUN echo "deb http://mirrors.aliyun.com/debian/ jessie main non-free contrib" > /etc/apt/sources.list

RUN echo "deb http://mirrors.aliyun.com/debian/ jessie-proposed-updates main non-free contrib" >> /etc/apt/sources.list

RUN echo "deb-src http://mirrors.aliyun.com/debian/ jessie main non-free contrib" >> /etc/apt/sources.list

RUN echo "deb-src http://mirrors.aliyun.com/debian/ jessie-proposed-updates main non-free contrib" >> /etc/apt/sources.list

RUN apt-get update

RUN apt-get install gcc -y;
RUN apt-get install vim -y;
RUN apt-get install make -y;

# 设置运行环境版本
ENV RUNTIME_VERSION 1.0
# 设置Ta_lib版本
ENV TA_LIB_VERSION 0.4.0
# 设置workDir
ENV WORKDIR /usr/local/runtime
# 设置TalibHome
ENV TA_LIB_HOME /usr/local/talib
# 设置动态链接库路径
ENV LD_LIBRARY_PATH ${LD_LIBRARY_PATH}:/usr/local/lib
# 设置编译库路径
ENV LIBRARY_PATH ${LIBRARY_PATH}:${TA_LIB_HOME}/include/ta-lib
# 设置编译库路径
ENV C_INCLUDE_PATH ${TA_LIB_HOME}/include
# 工作路径
WORKDIR ${WORKDIR}

RUN wget -O talib.tar.gz "https://nchc.dl.sourceforge.net/project/ta-lib/ta-lib/${TA_LIB_VERSION}/ta-lib-${TA_LIB_VERSION}-src.tar.gz";

RUN echo ${TA_LIB_HOME}/lib > /etc/ld.so.conf.d/talib.conf

RUN ldconfig

RUN mkdir src && tar -xvf talib.tar.gz -C src; \
    \
    mkdir src && tar -zxvf talib.tar.gz -C src; \
    \
    cd src/ta-lib; \
    \
    ./configure; \
    \
    make && make install
    \
RUN pip install ta-lib -i https://mirrors.aliyun.com/pypi/simple/;

RUN cd ${WORKDIR}