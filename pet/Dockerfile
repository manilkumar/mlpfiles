FROM centos:latest

ARG DEBIAN_FRONTEND=noninteractive

#RUN rm -vf /var/lib/apt/lists/* && apt-get clean

RUN yum -y update 
RUN yum -y install unzip wget libXext libXt-devel libXmu libstdc++6

RUN mkdir /mcr-install && \
    cd /mcr-install && \
    wget http://www.mathworks.com/supportfiles/downloads/R2015b/deployment_files/R2015b/installers/glnxa64/MCR_R2015b_glnxa64_installer.zip && \
    cd /mcr-install && \
    unzip -q MCR_R2015b_glnxa64_installer.zip && \
    ./install -mode silent -agreeToLicense yes

ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/MATLAB/MATLAB_Runtime/v90/runtime/glnxa64:/usr/local/MATLAB/MATLAB_Runtime/v90/bin/glnxa64:/usr/local/MATLAB/MATLAB_Runtime/v90/sys/os/glnxa64

ENV XAPPLRESDIR usr/local/MATLAB/MATLAB_Runtime/v90/X11/app-defaults

ENV MCR_CACHE_VERBOSE=true
ENV MCR_CACHE_ROOT=/tmp

RUN rm -rf mcr-install
RUN mkdir /data

COPY . /data

VOLUME /data

WORKDIR /data

ENTRYPOINT ["./entrypoint.sh"]



