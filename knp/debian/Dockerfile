FROM debian:buster as builder

ENV DEBIAN_FRONTEND=noninteractive
ENV LANG=C.UTF-8
ARG INSTALL_PATH=/usr/local

WORKDIR /workdir

# ビルドツールのインストール
RUN apt-get update -q \
	&& apt-get install -qy \
        git \
        g++ \
		libtool \
        make \
        unzip \
        wget \
        zlib1g-dev

# KNPのソースをダウンロード
RUN git clone https://github.com/ku-nlp/knp.git \
    && cd knp \
    && ./autogen.sh

WORKDIR /workdir/knp

# knpの辞書をダウンロード
RUN wget http://lotus.kuee.kyoto-u.ac.jp/nl-resource/knp/dict/latest/knp-dict-latest-bin.zip \
    && unzip knp-dict-latest-bin.zip \
    && cp -ars `pwd`/dict-bin/* ./dict

# knpをビルド
RUN ./configure --prefix=${INSTALL_PATH} \
    && make -j $(nproc) \
    && make install

FROM debian:buster-slim
COPY --from=builder /usr/local/ /usr/local/

CMD [ "knp" ]