# NVIDIA GameWorks Graphics Samples
# https://github.com/NVIDIAGameWorks/GraphicsSamples

# docker build -t graphics-samples .
# xhost +si:localuser:root
# docker run --runtime=nvidia -ti --rm -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix graphics-samples

FROM nvidia/opengl:1.0-glvnd-devel-centos7

ENV NVIDIA_DRIVER_CAPABILITIES ${NVIDIA_DRIVER_CAPABILITIES},display

RUN yum install -y \
        git \
	gcc-c++ \
	make \
	libXinerama-devel \
	libXext-devel \
	libXrandr-devel \
	libXi-devel \
	libXcursor-devel \
	libXxf86vm-devel \
	vulkan-devel && \
    rm -rf /var/cache/yum/*

RUN git clone https://github.com/NVIDIAGameWorks/GraphicsSamples.git /opt/demos && \
    cd /opt/demos && \
    git checkout e82e141516ca86961fd151cc944730fe0be29dea && \
    cd /opt/demos/samples/build/linux64 && make -j"$(nproc)" release && \
    rm -rf /opt/demos/samples/build/linux64

WORKDIR /opt/demos/samples/bin/linux64

CMD ./ThreadedRenderingGL
