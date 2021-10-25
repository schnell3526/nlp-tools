FROM alpine:3.14 as builder

ARG JPP_VERSION=2.0.0-rc3
ARG JPP_PATH=/usr/local

ENV PATH=${JPP_PATH}/bin:$PATH
ENV LANG=C.UTF-8

RUN apk update \
	&& apk add \
    libexecinfo-dev \
    g++ \
    make \
    cmake \
    wget \
	&& ln -s /usr/include/linux/sysctl.h /usr/include/sys/sysctl.h


# ソースをダウンロード
RUN wget "https://github.com/ku-nlp/jumanpp/releases/download/v${JPP_VERSION}/jumanpp-${JPP_VERSION}.tar.xz" \
	&& tar xvf "jumanpp-${JPP_VERSION}.tar.xz"

# ソースをビルドしてインストール
RUN cd "jumanpp-${JPP_VERSION}" \
	&& mkdir build \
	&& cd build \
	&& cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=${JPP_PATH} \
	&& make -j "$(nproc)" \
	&& make install


FROM alpine:3.14
COPY --from=builder /usr/local/bin /usr/local/bin
COPY --from=builder /usr/local/libexec /usr/local/libexec

RUN apk --no-cache add libstdc++

CMD [ "jumanpp" ]