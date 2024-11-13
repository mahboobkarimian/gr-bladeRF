FROM nuand/gnuradio-bladerf:latest
ENV DEBIAN_FRONTEND=noninteractive
RUN sudo apt-get update 
RUN sudo apt-get install libncurses5-dev -y
WORKDIR /home/blade/
RUN git clone https://github.com/Nuand/bladeRF.git
RUN mkdir -p /home/blade/bladeRF/build
WORKDIR /home/blade/bladeRF/build
RUN cmake .. && make -j
RUN sudo make install
RUN sudo ldconfig
WORKDIR /home/blade/
RUN rm -rfd gr-bladeRF
RUN git clone https://github.com/Nuand/gr-bladeRF.git
RUN mkdir -p /home/blade/gr-bladeRF/build
WORKDIR /home/blade/gr-bladeRF/build
RUN cmake .. && make -j
RUN sudo make install
RUN sudo ldconfig
WORKDIR /home/blade/
RUN rm -rfd gr-bladeRF bladeRF
COPY ./keyboard /etc/default/keyboard
RUN sudo echo 'debconf debconf/frontend select Noninteractive' | sudo debconf-set-selections
RUN sudo echo keyboard-configuration keyboard-configuration/layout select 'English (US)' | sudo debconf-set-selections
RUN sudo echo keyboard-configuration keyboard-configuration/layoutcode select 'us' | sudo debconf-set-selections 
RUN sudo echo "resolvconf resolvconf/linkify-resolvconf boolean false" | sudo debconf-set-selections
RUN sudo apt-get install -y keyboard-configuration
RUN sudo apt-get install -y qtcreator libxrender1 gdb
RUN sudo apt-get install -y fonts-ubuntu
RUN sudo apt install -y python3-pygccxml
CMD ["/usr/bin/qtcreator"]
