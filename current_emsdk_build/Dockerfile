FROM ubuntu:latest

LABEL description="Build with Current and Emscripten"

RUN apt-get update -y

RUN apt-get install -y build-essential curl iputils-ping git python3 vim

# Ran `git clone https://github.com/emscripten-core/emsdk.git` in `deps`.
# HEAD at `060b48f0c69827f95c8433ee965656babf953e82`, Dec 26 2021.
COPY deps /deps

RUN (cd /deps/emsdk; ./emsdk install latest)
RUN (cd /deps/emsdk; ./emsdk activate latest)
ENV PATH="${PATH}:/deps/emsdk:/deps/emsdk/node/14.15.5_64bit/bin:/deps/emsdk/upstream/emscripten"

ENV CPLUSPLUS=g++
ENV NDEBUG=1

CMD ["echo", "-e", "Success! To use, run:\n\ndocker run -v \"$PWD\":\"$PWD\" --workdir \"$PWD\" -p 8800:8800 -it dimakorolev/current_emsdk_build:latest bash"]
