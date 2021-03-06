# VTK ElevationBandsWithGlyphs Python example
# https://lorensen.github.io/VTKExamples/site/Python/Visualization/ElevationBandsWithGlyphs/

# docker build -t vtk .
# docker run --runtime=nvidia -v /tmp:/tmp -ti --rm vtk
# gimp /tmp/ElevationBandsWithGlyphs.png

FROM nvidia/opengl:1.0-glvnd-devel-ubuntu14.04

ENV NVIDIA_REQUIRE_DRIVER "driver>=390"

RUN apt-get update && apt-get install -y --no-install-recommends \
        ca-certificates \
        git \
        cmake3 \
        make \
        g++ \
        curl \
        python-dev \
        python2.7 && \
    rm -rf /var/lib/apt/lists/*

RUN git clone --depth=1 --branch=v8.1.0 https://gitlab.kitware.com/vtk/vtk.git && \
    mkdir vtk/build && cd vtk/build && \
    cmake .. -DVTK_RENDERING_BACKEND=OpenGL2 -DVTK_OPENGL_HAS_EGL=ON -DVTK_USE_X=OFF -DBUILD_TESTING=OFF -DVTK_WRAP_PYTHON=ON && \
    make -j"$(nproc)" install && \
    cd / && rm -rf /vtk

ENV PYTHONPATH /usr/local/lib/python2.7/site-packages

RUN curl -fsSL https://github.com/lorensen/VTKWikiExamplesTarballs/raw/master/ElevationBandsWithGlyphs.tar -O && \
    tar -xf ElevationBandsWithGlyphs.tar && rm ElevationBandsWithGlyphs.tar && cd ElevationBandsWithGlyphs && \
    sed -i 's/800, 800/3840, 2160/' ElevationBandsWithGlyphs.py && \
    sed -i 's;# WritePNG(\(.*\),;WritePNG(\1, "/tmp/ElevationBandsWithGlyphs.png");' ElevationBandsWithGlyphs.py

CMD python ElevationBandsWithGlyphs/ElevationBandsWithGlyphs.py
