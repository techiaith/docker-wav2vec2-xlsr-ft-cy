FROM techiaith/wav2vec2-xlsr-ft-cy-device

# gosod YouTube downloader
RUN wget https://yt-dl.org/downloads/latest/youtube-dl -O /usr/local/bin/youtube-dl \
 && chmod a+rx /usr/local/bin/youtube-dl

#
ARG MODEL_VERSION
ARG WAV2VEC2_MODEL_NAME

#
ENV MODEL_VERSION=${MODEL_VERSION}
ENV WAV2VEC2_MODEL_NAME=${WAV2VEC2_MODEL_NAME}

# Set the locale
RUN locale-gen cy_GB.UTF-8
ENV LANG cy_GB.UTF-8
ENV LANGUAGE cy_GB:en
ENV LC_ALL cy_GB.UTF-8

# Install local Python files and dependencies..
RUN mkdir -p /wav2vec2

WORKDIR /wav2vec2

COPY python/requirements.txt /wav2vec2/
RUN pip3 install -r requirements.txt 

ENV PATH="${PATH}:/wav2vec2"
ENV PYTHONPATH "${PYTHONPATH}:/wav2vec2"

# install ctc-decode
RUN git clone --recursive https://github.com/parlance/ctcdecode.git /tmp/ctcdecode \
 && cd /tmp/ctcdecode && pip3 install .

COPY python /wav2vec2/
COPY speech.wav /wav2vec2/

